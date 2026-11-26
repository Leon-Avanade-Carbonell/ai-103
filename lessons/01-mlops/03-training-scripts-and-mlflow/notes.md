# Run training scripts and track models with MLflow in Azure Machine Learning

- Module ID: M03
- Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/
- Curriculum verified: 2026-10-28
- Exam objectives: D2 orchestrate model training.

## Overview and learning goals

Planned source goals: convert notebooks to scripts, test in a terminal, run parameterized command jobs, use MLflow in jobs, and review metrics, parameters, artifacts, and models.

Concept explanations below are based on the linked Microsoft Learn units; tutor additions are labeled. All examples are illustrative: no code, terminal command, Azure job, scheduler, logging, or workspace query was executed. No SDK/CLI package versions or authentication setup were tested. Source fetch dates are historical records, not new verification from this prose cleanup.

## Notes by Microsoft Learn unit

### M03-U01 — Introduction
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/1-introduction

Source fetched: 2026-11-04; page updated 2026-08-27.

#### From interactive experimentation to repeatable training

Use notebooks to experiment and scripts for repeatable, scalable training. An Azure Machine Learning **command job** runs the script with configured data, environment, and compute.

| Role | Responsibility |
| --- | --- |
| Notebook | Explore data and develop training code interactively. |
| Training script | Execute data-processing and model-training logic. |
| Command job | Define and run that script with configured inputs, environment, and compute. |
| MLflow | Track parameters, metrics, and artifacts for run comparison and next-step decisions. |

Tutor clarification: a job defines **how to run**; a scheduler or automation workflow decides **when to submit**. Submission alone does not create weekly recurrence. No scheduling API or configuration is covered here.

MLflow records what its logging captures. It does not train or schedule the model, and tracking alone does not establish production readiness. Evaluation and deployment remain separate steps.

#### Worked workflow illustration

Tutor example: develop a classifier in a notebook → move training into `train.py` → use weekly automation to submit a command job with updated data. The script trains; MLflow records settings, results, and files for run comparison.

This introduction is conceptual; executable examples appear in later units. No JavaScript counterpart has been established.

[Optional quiz history](quizzes.md)

### M03-U02 — Convert a notebook to a script
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/2-convert-notebook-script

Source fetched: 2026-11-05; page updated 2026-08-27.

#### Remove all nonessential code

Prepare a script for automation by removing nonessential code, refactoring into functions, and testing in a terminal. You can also write a script directly without starting in a notebook.

Remove unused exploration such as `df.head()` or `df.describe()`. Keep required loading, preprocessing, and useful operator output such as `print()` statements. Unnecessary execution adds compute time and cost.

#### Refactor your code into functions

Small functions make code easier to read, maintain, and test one responsibility at a time. The source separates CSV reading from train/test splitting.

Tutor example: separate loading from removing rows with missing targets. This illustrates structure, not a complete training script.

```python
import pandas as pd

def load_data(path):
    return pd.read_csv(path)

def prepare_data(df):
    return df.dropna(subset=["target"])

def main():
    df = load_data("training.csv")
    df = prepare_data(df)
    print(f"Prepared {len(df)} rows")

if __name__ == "__main__":
    main()
```

Requires Python 3, pandas, and an accessible `training.csv` with a `target` column; the unit specifies no package version. Expected: load the CSV, drop rows without a target, and print the remaining count. The tutor-added `__main__` guard runs `main()` on direct execution, but not when importing functions for testing.

The target is the answer to predict. `dropna(subset=["target"])` removes rows missing that value, not rows with any missing feature. Correct cleaning does not prove better model performance.

Tutor isolation task: give `prepare_data()` an in-memory table with features 10, 20, 30 and targets 1, missing, 0. It should retain rows one and three. This isolates preparation from file paths and training, making failures easier to locate.

#### Test your script

Run the script in a terminal before automating it. In Azure ML studio, use save-and-run on the Notebooks page or open a compute instance's Terminal through the Compute page.

```text
python train.py
```

Requires Python, the script's dependencies and data, and an available compute instance if using its terminal. Expected: local script execution with output and errors visible. This Python command does not submit an Azure job, schedule recurrence, or register a model.

Tutor troubleshooting: a fresh script process does not inherit notebook variables. Include all imports and initialization steps. Passing a preparation test does not validate file loading.

| Error | Likely issue in these illustrations |
| --- | --- |
| `NameError` for `df` | Variable was not initialized before use, potentially hidden by retained notebook state. |
| `FileNotFoundError` | Missing file or wrong path during CSV loading. |
| `KeyError` for `target` | Required column absent during preparation. |

An in-memory preparation test bypasses loading, so it cannot expose an incorrect CSV path.

### M03-U03 — Run a script as a command job
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/3-run-script-command-job

Source fetched: 2026-11-05; page updated 2026-08-27.

#### Configure and submit a command job

The script contains training logic. Python SDK v2's `command` function configures how Azure ML runs it; submission is a separate step.

| Setting | Responsibility |
| --- | --- |
| `code` | Folder containing the script and supporting files. |
| `command` | Command to execute, such as `python train.py`. |
| `environment` | Software dependencies required for execution. |
| `compute` | Compute target that executes the workload. |
| `display_name` | Human-readable label for an individual job. |
| `experiment_name` | Groups related runs under an experiment. |

Tutor decision example: to run the same `./src/train.py` on larger compute, change `compute`. Keep `environment`, `experiment_name`, `code`, and `command` if dependencies, grouping, and workload are unchanged. A distinct `display_name` helps you find the run but is not required for identity.

Environment supplies software; compute supplies execution resources. Larger compute does not fix a missing Python package.

Official submission example:

```python
# job has already been configured with azure.ai.ml.command(...)
returned_job = ml_client.create_or_update(job)
```

Requires SDK v2 (`azure-ai-ml`), an authenticated workspace `ml_client`, and accessible compute/environment resources. Expected: submit the job, not confirm training success. The source uses a legacy curated environment whose availability and suitability remain unverified; no runnable environment selection is provided here.

#### Inspect runs and separate execution from recurrence

Review jobs in Azure ML studio: `experiment_name` groups runs, and `display_name` helps locate one. Inspect the command, compute, environment, and recorded inputs and outputs.

Tutor clarification: `job = command(...)` configures the job; `ml_client.create_or_update(job)` submits it. Recurring submissions need a scheduler or automation trigger. A pipeline defines a workflow but also needs a trigger to start it.

Recorded job settings do not calculate model-quality metrics. See M03-U05 for metric logging.

### M03-U04 — Use parameters in a command job
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/4-use-parameters-command-job

Source fetched: 2026-11-05; page updated 2026-08-27.

#### Working with script arguments

Parameters let you reuse a script with different data or hyperparameters. Define arguments, types, and defaults with Python's `argparse`.

Tutor argument-parsing example:

```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument("--training_data", type=str)
args = parser.parse_args()
print(args.training_data)
```

Requires Python 3; `argparse` is built in. Running `python train.py --training_data diabetes.csv` should print `diabetes.csv`.

**Supply a value → parse it → use it.** For CSV loading, use `pd.read_csv(args.training_data)` rather than a hard-coded filename. This requires pandas imported as `pd` and an accessible CSV; parsing alone does not change the loading path.

Tutor hyperparameter fragment:

```python
parser.add_argument("--max_iter", type=int, default=100)
```

Add this declaration before `parse_args()`. The default is `100`; `--max_iter 200` overrides it. Training must use `args.max_iter` for the value to matter. This is a fragment, not complete training code.

#### Passing arguments to a script

Supply arguments in the terminal or the job's `command` setting. Tutor dataset-switching example:

```text
python train.py --training_data january.csv
python train.py --training_data february.csv
```

Once the script parses and uses the argument, change the filename value. The same pattern in an SDK v2 job configuration is:

```python
command="python train.py --training_data february.csv"
```

This configuration fragment requires `azure-ai-ml` SDK v2, an authenticated workspace client for submission, suitable compute/environment, and accessible script/data. It does not submit a job. The source's legacy environment remains unverified, as noted in M03-U03.

A filename argument does not upload or validate data. Paths must resolve separately in local and remote contexts. After submission, inspect the specified input/output parameters. Parameterization itself does not schedule jobs or measure model quality.

### M03-U05 — Track metrics with MLflow
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/5-track-metrics

Source fetched: 2026-11-05; page updated 2026-08-27.

#### Understand MLflow

MLflow tracks parameters, metrics, and artifacts across training platforms. Azure ML associates logged information with the job run for inspection and comparison.

| Category | Meaning | Tutor illustration |
| --- | --- | --- |
| Parameter | Input setting used by a run | `max_iter = 200` |
| Metric | Numeric measured result | Cleaning duration in seconds |
| Artifact | Output file or object | A plot, image, or saved model |

Classify by meaning: a numeric training setting is still a parameter, not a metric.

#### Include MLflow in the environment

Include `mlflow` and `azureml-mlflow` in the environment that runs the script. Define/register that environment and reference it in the job.

Official Conda YAML excerpt:

```yaml
name: mlflow-env
channels:
  - conda-forge
dependencies:
  - python=3.10
  - pip
  - pip:
    - scikit-learn
    - mlflow
    - azureml-mlflow
```

This environment specification supplies training and MLflow packages for remote execution. Python 3.10 is the example's choice, not a universal requirement. Packages are unpinned; compatibility and registration remain untested. The YAML does not submit a job.

Tutor troubleshooting: if `import mlflow` works locally but fails remotely, check the job's environment first. Laptop installations do not change remote dependencies.

#### Enable autologging

`mlflow.autolog()` enables logging for supported libraries such as scikit-learn. Capture depends on the integration; add explicit logging for custom information.

Tutor logging fragment:

```python
import mlflow

mlflow.autolog()
mlflow.log_param("max_iter", 200)

# Suppose separate timing code measured this value:
training_seconds = 42.7
mlflow.log_metric("training_seconds", training_seconds)
```

Requires Python with `mlflow`, a supported scikit-learn integration for autologging, and `azureml-mlflow` for Azure ML jobs. Expected: log the supplied setting and duration, and enable supported capture when training occurs. This fragment neither trains nor times a model. Logging a parameter does not configure the estimator; training must use the setting too.

#### Log metrics with MLflow

Logging functions:

- `mlflow.log_param()` records a single key-value input parameter.
- `mlflow.log_metric()` records a single key-value metric whose value must be numeric.
- `mlflow.log_figure()` stores a Matplotlib figure as an artifact without first saving it to disk.
- `mlflow.log_image()` stores a NumPy or PIL image as an artifact without first saving it to disk.

Tutor decision example: use autologging for supported training information and `log_metric()` for data-cleaning duration. Measure the duration first; logging only records the number.

#### Submit the job

Submit the command job with the required environment. The script's logging determines what is retained. MLflow does not replace submission, training, or evaluation.

### M03-U06 — View metrics and evaluate models
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/6-view-metrics-evaluate-models

Source fetched: 2026-11-05; page updated 2026-08-27.

#### View the metrics in the Azure Machine Learning studio

After a job completes, open its experiment run in https://ml.azure.com. Both Azure ML and MLflow group runs into experiments.

| Information | Studio location described by the source |
| --- | --- |
| Logged input parameters, such as `max_iter` | **Details → Params** |
| Logged numeric metrics, such as measured training duration | **Metrics** |
| Logged plots | **Images** |
| Model assets available for registration and deployment | **Outputs + logs → models** |

Tutor clarification: category and viewing location are different questions. Plots are artifacts, but studio displays them under **Images**. A successful run does not prove model quality, and saved model files are not automatically registered or deployed.

#### Retrieve metrics with MLflow in a notebook

Use `get_experiment_by_name()` to find an experiment and `search_runs()` to compare existing runs. **Filter** selects eligible runs; **sort** ranks them; **`max_results`** limits the count. These queries do not launch training.

Adaptation of the source query:

```python
import mlflow

exp = mlflow.get_experiment_by_name("training-experiment")
runs = mlflow.search_runs(
    experiment_ids=[exp.experiment_id],
    filter_string="params.num_boost_round = '100'",
    order_by=["start_time DESC"],
    max_results=2,
)
```

Requires Python with MLflow, access to the workspace tracking service, and an existing `training-experiment`; Azure ML integration uses `azureml-mlflow`. Expected: at most two most recently started runs with logged `num_boost_round=100`. Experiment lookup must succeed before accessing its ID.

#### Worked comparison decision

Tutor task and solution: keep the parameter filter, but rank by logged `validation_loss` (lower is better). Replace the ordering clause with:

```python
order_by=["metrics.validation_loss ASC"]
```

Requires runs with that metric logged on comparable evaluation data. Ascending loss ranks lower values first; descending start time ranks newer runs, not better models. Sorting needs no formal primary-metric designation. Choose the relevant metric and direction, then assess quality and operational requirements before deployment.

Supplemental syntax source: [MLflow Search Runs — Ordering](https://mlflow.org/docs/latest/ml/search/search-runs/#3---ordering), fetched 2026-11-05, confirms metric sorting with `ASC` or `DESC`; this was API verification, not learner practice.

### M03-U07 — Exercise - Optimize model training in Azure Machine Learning
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/7-exercise

Website-only. Study independently using the source link. Excluded from tutor lessons, checks, reviews, completion, and TLDR readiness; no website confirmation is required.

### M03-U08 — Module assessment
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/8-knowledge-check

Website-only. Study independently using the source link. Excluded from tutor lessons, checks, reviews, completion, and TLDR readiness; no website confirmation is required.

### M03-U09 — Summary
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/9-summary

Website-only. Study independently using the source link. Excluded from tutor lessons, checks, reviews, completion, and TLDR readiness; no website confirmation is required.

<!-- Retain legacy section targets while consolidating scaffolding. -->
<a id="key-concepts-and-decision-points"></a>
<a id="python-examples"></a>
<a id="javascript-examples"></a>
<a id="azure-cli-commands"></a>
<a id="related-configuration-yaml-bicep-or-github-actions"></a>
<a id="worked-examples-and-practice"></a>
<a id="common-pitfalls-and-clarifications"></a>

## Remaining study and examples

Examples and pitfalls are beside their concepts above. Unresolved work from the earlier scaffolding remains pending:

- Full training execution; worked fragments do not demonstrate an end-to-end run. M03-U07 remains website-only.
- Additional job configuration and automation examples, where relevant.
- JavaScript and Azure CLI examples: relevance not yet assessed; supported examples and required versions/prerequisites remain pending.
- The former cross-unit key-concepts section was pending; whether any additional study was intended is unknown. Existing concepts remain under their units.

## Microsoft Learn search terms
- Azure Machine Learning command job parameters
- MLflow log metrics artifacts models Azure
- convert notebook training script Azure Machine Learning
