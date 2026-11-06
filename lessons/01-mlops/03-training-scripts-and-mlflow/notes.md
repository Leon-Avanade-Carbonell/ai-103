# Run training scripts and track models with MLflow in Azure Machine Learning

- Module ID: M03
- Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/
- Curriculum verified: 2026-10-28
- Exam objectives: D2 orchestrate model training.

## Overview and learning goals

Planned source goals: convert notebooks to scripts, test in a terminal, run parameterized command jobs, use MLflow in jobs, and review metrics, parameters, artifacts, and models.

## Notes by Microsoft Learn unit

### M03-U01 — Introduction
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/1-introduction

Source fetched: 2026-11-04; page updated 2026-08-27. Conceptual study only; no code, command job, scheduler, or MLflow logging was executed.

#### From interactive experimentation to repeatable training

Official source: production-oriented training code should be scalable, repeatable, and ready for automation. Notebooks are ideal for experimentation and development; scripts are a better fit for production workloads. In Azure Machine Learning, run a script as a **command job**, configuring inputs such as data and the compute environment.

| Role | Responsibility |
| --- | --- |
| Notebook | Explore data and develop training code interactively. |
| Training script | Execute data-processing and model-training logic. |
| Command job | Define and run that script with configured inputs, environment, and compute. |
| MLflow | Track parameters, metrics, and artifacts for run comparison and next-step decisions. |

Tutor clarification: a submitted command job does not automatically recur weekly. A scheduler or automation workflow supplies the recurring trigger and submits the job; the job then executes the script. Distinguish **when to submit** from **how the workload executes**. No scheduling API or executable configuration was introduced here.

MLflow records the evidence captured by configured logging, not automatically everything happening in a job. Tracking does not itself train the model, schedule execution, or guarantee production readiness. Moving code into a script makes reuse and automation easier, but model evaluation and deployment remain separate concerns. These distinctions support AI-300 D2 training orchestration and experiment comparison.

#### Worked workflow illustration

Tutor-created, not executed: develop a classifier in a notebook, move its training logic into `train.py`, and have weekly automation submit an Azure Machine Learning command job using updated input data. The script trains the model; MLflow preserves settings, measured results, and output files for comparison across runs. Manual submission today alone does not arrange a run next week.

The module's planned next topics are notebook-to-script conversion, terminal testing, command jobs and parameters, MLflow integration, and inspecting run outputs. No SDK/CLI versions or package prerequisites were tested in this conceptual introduction; relevant executable examples remain pending in later units. No JavaScript equivalent was assumed.

[Optional quiz history](quizzes.md)

### M03-U02 — Convert a notebook to a script
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/2-convert-notebook-script

Source fetched: 2026-11-05; page updated 2026-08-27. Conceptual study with illustrative examples; no code or terminal commands were executed.

#### Remove all nonessential code

Official source: prepare scripts for testing and automation by removing nonessential code, refactoring into functions, and testing in a terminal. Scripts can also be developed directly without starting in a notebook.

Remove exploratory statements such as unused `df.head()` previews or `df.describe()` summaries when they no longer serve the automated workflow. Retain required loading and preprocessing. Useful `print()` output can remain when operators inspect it; output is not inherently nonessential. Avoid unnecessary execution to reduce compute time and cost.

#### Refactor your code into functions

Official source: smaller functions improve readability, maintenance, and testing. Its example separates CSV reading from train/test splitting. Test one responsibility without unnecessarily executing the rest of the workflow.

Tutor-created illustration: separate loading from removing rows with missing target values. This demonstrates structure, not a complete training script.

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

Prerequisites: Python 3, pandas, an accessible `training.csv` with a `target` column. No specific package version was tested or required by the fetched unit. Not executed. Expected outcome: load the CSV, remove rows lacking a target, and print the remaining row count. The tutor-added `__main__` guard runs `main()` on direct execution without launching it when functions are imported for testing.

`dropna(subset=["target"])` removes rows missing that column's value, not all rows with a missing value anywhere. For supervised training, the target is the answer to predict. Cleaning correctness and model quality are distinct: passing this test does not demonstrate improved model performance.

Worked isolation task, tutor-created and not executed: supply `prepare_data()` an in-memory table whose feature values are 10, 20, 30 and targets are 1, missing, 0. Expected result: retain the first and third rows, with no missing targets. This tests preparation independently of CSV paths and training. A smaller input is faster, but the central advantage is pinpointing the faulty responsibility.

#### Test your script

Official source: run a script in a terminal before integrating it into production automation. Azure Machine Learning studio offers save-and-run from the Notebooks page or access to a compute instance's Terminal through the Compute page.

```text
python train.py
```

Requires a Python interpreter, the script's dependencies and data, and an available compute instance when using its terminal. Not executed. Expected outcome: direct script execution with print output and errors visible in the terminal. This is not an Azure CLI command and does not itself submit an Azure ML command job, establish recurrence, or register a model.

Tutor troubleshooting clarification: notebooks retain variables from earlier cells; a fresh script process does not inherit them. Ensure imports and initialization steps are present before use. A passing preparation test does not prove file loading works.

| Error | Likely issue in these illustrations |
| --- | --- |
| `NameError` for `df` | Variable was not initialized before use, potentially hidden by retained notebook state. |
| `FileNotFoundError` | Missing file or wrong path during CSV loading. |
| `KeyError` for `target` | Required column absent during preparation. |

An in-memory preparation test bypasses loading, so an incorrect CSV path cannot affect that test. These distinctions support AI-300 D2 repeatable training and troubleshooting; they do not constitute execution evidence.

### M03-U03 — Run a script as a command job
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/3-run-script-command-job

Source fetched: 2026-11-05; page updated 2026-08-27. Conceptual study only; no SDK code, Azure job, or scheduler was executed.

#### Configure and submit a command job

Official source: the training script contains the workload logic; use the Python SDK v2 `command` function to configure how Azure Machine Learning runs it, then submit the configured job.

| Setting | Responsibility |
| --- | --- |
| `code` | Folder containing the script and supporting files. |
| `command` | Command to execute, such as `python train.py`. |
| `environment` | Software dependencies required for execution. |
| `compute` | Compute target that executes the workload. |
| `display_name` | Human-readable label for an individual job. |
| `experiment_name` | Groups related runs under an experiment. |

Tutor-created worked configuration decision, not executed: run the same `./src/train.py` on a larger compute target while retaining dependencies and comparison grouping. Change `compute`, keep `environment` and `experiment_name`, and keep `code` and `command` when the workload is unchanged. A distinct `display_name` helps identify the run but is not required for job identity.

Environment and compute are different concerns: environment supplies software, while compute supplies execution resources. Increasing compute size does not fix a missing Python package.

Official submission example, not executed:

```python
# job has already been configured with azure.ai.ml.command(...)
returned_job = ml_client.create_or_update(job)
```

Prerequisites: Python SDK v2 (`azure-ai-ml`), an authenticated `ml_client` connected to the intended workspace, and accessible compute/environment resources. No specific SDK package version was tested. Expected outcome: submit the configured job for execution; this is not proof of successful training. The source's environment example uses a legacy curated environment name; availability and suitability were not verified, so no runnable environment selection is prescribed here.

#### Inspect runs and separate execution from recurrence

Official source: monitor and review jobs in Azure Machine Learning studio. Jobs with the same `experiment_name` are grouped together; a display name helps locate an individual run. Review the recorded command, compute, environment, and tracked inputs and outputs.

Tutor clarification: creating `job = command(...)` only configures a job. `ml_client.create_or_update(job)` submits it, but does not create a Monday schedule. A separate scheduler or automation workflow supplies recurring submissions. A pipeline can define a workflow, but still needs a schedule or another trigger to start it. No scheduling API or configuration was introduced or executed.

Tracking job configuration is not equivalent to calculating or logging every model-quality metric. MLflow metric logging is covered in M03-U05. These distinctions support AI-300 D2 training orchestration and comparison of runs.

### M03-U04 — Use parameters in a command job
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/4-use-parameters-command-job

Source fetched: 2026-11-05; page updated 2026-08-27. Conceptual study with illustrative examples; no script or Azure job was executed.

#### Working with script arguments

Official source: parameters make a script reusable with different datasets or hyperparameter values. Define expected arguments in the script with a library such as Python's `argparse`; specify types and defaults where appropriate.

Tutor-created simplified illustration, not executed:

```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument("--training_data", type=str)
args = parser.parse_args()
print(args.training_data)
```

Prerequisites: Python 3; `argparse` is in the standard library. No specific Python version was tested. With `python train.py --training_data diabetes.csv`, the expected printed value is `diabetes.csv`.

The complete connection is **command supplies a value → argument parser reads it → workload uses it**. For CSV loading, use `pd.read_csv(args.training_data)` rather than `pd.read_csv("diabetes.csv")`. This loading fragment additionally requires pandas (imported as `pd`) and an accessible CSV. Merely parsing a new filename does not change a hard-coded loading path.

Tutor hyperparameter illustration, not executed:

```python
parser.add_argument("--max_iter", type=int, default=100)
```

Without this argument the parsed value is `100`; `--max_iter 200` supplies `200`. Training code must consume `args.max_iter` for it to affect training. This declaration is added before `parse_args()`; it is not a complete training implementation.

#### Passing arguments to a script

Official source: supply values in the terminal command or in an Azure Machine Learning command job's `command` setting. Tutor-created dataset-switching example, not executed:

```text
python train.py --training_data january.csv
python train.py --training_data february.csv
```

Change the filename value, not the script, when the script already parses and uses the argument. The same pattern in a Python SDK v2 command-job configuration is:

```python
command="python train.py --training_data february.csv"
```

This is a configuration fragment, not job submission or a runnable full configuration. Requires `azure-ai-ml` SDK v2 for the enclosing job, an authenticated workspace client for submission, suitable compute/environment, and the script and data accessible at execution. No SDK package version was tested. The source's legacy curated environment was not verified for availability or suitability; no runnable environment choice is prescribed.

Passing a filename does not upload, create, or validate that file. Local terminal paths and remote job paths must each resolve in their respective execution context. Official source also notes reviewing specified input/output parameters after job submission; no such review was performed here. Parameterized execution supports AI-300 D2 reusable training orchestration; it does not itself schedule jobs or measure model quality.

### M03-U05 — Track metrics with MLflow
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/5-track-metrics

Source fetched: 2026-11-05; page updated 2026-08-27. Conceptual study with illustrative Python and an official YAML excerpt; nothing was executed.

#### Understand MLflow

Official source: MLflow is an open-source machine learning lifecycle platform that tracks parameters, metrics, and artifacts across training platforms. In Azure Machine Learning, logged information is associated with the job run for later inspection and comparison.

| Category | Meaning | Tutor illustration |
| --- | --- | --- |
| Parameter | Input setting used by a run | `max_iter = 200` |
| Metric | Numeric measured result | Cleaning duration in seconds |
| Artifact | Output file or object | A plot, image, or saved model |

Meaning determines the category: a numeric training setting remains a parameter, not a metric. These distinctions support AI-300 D2 tracking and comparing training runs.

#### Include MLflow in the environment

Official source: install both `mlflow` and `azureml-mlflow` on the compute executing the script. Include them in the job environment, define/register that environment, and reference it when submitting the command job.

Excerpt of the official Conda YAML example, not executed:

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

Python 3.10 is the source example's choice, not a universal requirement. Package versions are unpinned; compatibility and environment registration were not tested. Expected purpose: supply the training library and MLflow integration packages at remote execution. This is an environment specification, not a job submission command.

Tutor troubleshooting illustration: when `import mlflow` works locally but fails remotely, inspect the environment referenced by the job and its dependencies first. Installing packages on the laptop does not install them in the remote job environment.

#### Enable autologging

Official source: `mlflow.autolog()` enables automatic logging for supported ML libraries, including scikit-learn. What is captured depends on the library integration; autologging does not capture every custom fact about a workflow. Explicit custom logging can complement it.

Tutor-created fragment, not executed:

```python
import mlflow

mlflow.autolog()
mlflow.log_param("max_iter", 200)

# Suppose separate timing code measured this value:
training_seconds = 42.7
mlflow.log_metric("training_seconds", training_seconds)
```

Prerequisites: Python with `mlflow`; supported scikit-learn integration for automatic training capture, and `azureml-mlflow` in an Azure ML job environment. No package versions were tested. This fragment does not train a model or measure elapsed time. Expected logging intent: record the supplied setting and duration with the run, and enable supported automatic capture when training occurs. Recording a parameter does not configure the estimator; training code must also consume the setting.

#### Log metrics with MLflow

Official source logging functions:

- `mlflow.log_param()` records a single key-value input parameter.
- `mlflow.log_metric()` records a single key-value metric whose value must be numeric.
- `mlflow.log_figure()` stores a Matplotlib figure as an artifact without first saving it to disk.
- `mlflow.log_image()` stores a NumPy or PIL image as an artifact without first saving it to disk.

Tutor-created worked decision: use autologging for supported scikit-learn training information and explicit `log_metric()` for measured data-cleaning duration. The script must measure the duration first; the logging function only records the supplied number.

#### Submit the job

Official source: configure and submit the command job as usual, referencing the environment with the required packages. The script's configured logging determines the parameters, metrics, and artifacts retained with the run. MLflow does not replace job submission, training logic, or evaluation.

### M03-U06 — View metrics and evaluate models
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/6-view-metrics-evaluate-models

Source fetched: 2026-11-05; page updated 2026-08-27. Conceptual study with illustrative queries; no notebook query, training, or Azure workspace operation was executed.

#### View the metrics in the Azure Machine Learning studio

Official source: after a job completes, open its experiment run in https://ml.azure.com to inspect the logged information. Azure ML groups job runs into experiments; MLflow likewise uses experiments containing runs.

| Information | Studio location described by the source |
| --- | --- |
| Logged input parameters, such as `max_iter` | **Details → Params** |
| Logged numeric metrics, such as measured training duration | **Metrics** |
| Logged plots | **Images** |
| Model assets available for registration and deployment | **Outputs + logs → models** |

Tutor clarification: logging categories and viewing locations are related but different questions. A numeric input setting is still a parameter; a measured duration is a metric. Logged plots are artifacts, but the source directs readers to Images rather than the model-output folder to inspect them. Successful job execution does not establish model quality or deployment readiness. Saved model files are not automatically registered or deployed.

#### Retrieve metrics with MLflow in a notebook

Official source: MLflow can retrieve existing runs for flexible comparison. `get_experiment_by_name()` retrieves an experiment; `search_runs()` searches its run records. Filtering selects eligible runs, sorting orders them, and `max_results` limits the returned count. These operations do not launch training.

Illustrative adaptation of the source, not executed:

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

Prerequisites: Python with MLflow, access to the workspace's configured MLflow tracking service, and an existing experiment named `training-experiment`. Azure ML integration uses `azureml-mlflow` as covered in M03-U05. No package version or authentication setup was tested. Expected outcome: retrieve at most two most recently started runs in that experiment with the logged parameter `num_boost_round=100`. The example assumes experiment lookup succeeds before accessing its ID.

#### Worked comparison decision

Tutor-created exercise and solution, not executed: retain the parameter filter but rank eligible runs by a logged `validation_loss`, where lower is better. Replace the ordering clause with:

```python
order_by=["metrics.validation_loss ASC"]
```

This illustrative MLflow query fragment assumes the eligible runs logged the metric on comparable evaluation data. Ascending loss ranks lower values first; descending start time ranks newer runs first, not better models. No formal primary-metric designation is required merely to sort MLflow records. Choose a relevant evaluation criterion and its direction, then assess quality and operational requirements before deployment. These decisions support AI-300 D2 experiment comparison, not proof of production readiness.

Syntax verification: [MLflow Search Runs — Ordering](https://mlflow.org/docs/latest/ml/search/search-runs/#3---ordering), fetched 2026-11-05, confirms metric-column ordering with `ASC` or `DESC`. This supplemental API verification does not represent additional learner practice or executed code.

### M03-U07 — Exercise - Optimize model training in Azure Machine Learning
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/7-exercise

Pending exercise. Add the studied task and worked solution with execution context; label any equivalent substitute. Preserve learner outcomes in memory.

### M03-U08 — Module assessment
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/8-knowledge-check

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this closing unit; it is excluded from tutor completion, review scheduling, and TLDR readiness. No website confirmation is required.

### M03-U09 — Summary
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/9-summary

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this closing unit; it is excluded from tutor completion, review scheduling, and TLDR readiness. No website confirmation is required.

## Key concepts and decision points
Pending study.

## Python examples
See [M03-U02](#m03-u02--convert-a-notebook-to-a-script) for function-based preparation, [M03-U03](#m03-u03--run-a-script-as-a-command-job) for submission, [M03-U04](#m03-u04--use-parameters-in-a-command-job) for argument parsing, [M03-U05](#m03-u05--track-metrics-with-mlflow) for illustrative automatic/custom logging, and [M03-U06](#m03-u06--view-metrics-and-evaluate-models) for run filtering and sorting, all with prerequisites and execution context. Full training execution remains pending.

## JavaScript examples
Pending study. Use relevant supported examples only.

## Azure CLI commands
Pending study. Record CLI/extension prerequisites and expected outcomes.

## Related configuration: YAML, Bicep, or GitHub Actions
See [M03-U05](#m03-u05--track-metrics-with-mlflow) for the official Conda YAML excerpt, not executed. Job configuration and automation examples remain pending where relevant.

## Worked examples and practice
See [M03-U02](#m03-u02--convert-a-notebook-to-a-script) for the in-memory cleanup task and worked solution. Dedicated training exercise M03-U07 remains pending; no lab execution or equivalent full training exercise has been demonstrated.

## Common pitfalls and clarifications
- Exporting notebook cells alone does not establish script readiness: remove purposeless exploration, retain dependencies, refactor, and test.
- Small-function tests isolate responsibilities; passing one does not validate the whole workflow.
- A fresh terminal process does not inherit a notebook's variable state. See M03-U02 for error distinctions.
- Direct execution, command-job submission, and recurring automation are separate actions.

## Microsoft Learn search terms
- Azure Machine Learning command job parameters
- MLflow log metrics artifacts models Azure
- convert notebook training script Azure Machine Learning
