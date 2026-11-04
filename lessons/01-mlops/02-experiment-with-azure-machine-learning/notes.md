# Experiment with Azure Machine Learning

- Module ID: M02
- Source: https://learn.microsoft.com/en-us/training/modules/experiment-azure-machine-learning/
- Curriculum verified: 2026-10-28
- Exam objectives: D2 orchestrate training; responsible AI evaluation.

## Overview and learning goals

Planned source goals: prepare classification data for AutoML, configure experiments, evaluate/compare models, configure and use MLflow tracking in notebooks, and evaluate models with the Responsible AI dashboard.

## Notes by Microsoft Learn unit

### M02-U01 — Introduction
Source: https://learn.microsoft.com/en-us/training/modules/experiment-azure-machine-learning/1-introduction

Source fetched: 2026-10-29. The introduction frames experimentation as necessary because the best algorithm and preprocessing combination is rarely known beforehand.

#### Experimentation tools and workflow

Official source explanation:
- **AutoML** automatically searches algorithms and preprocessing configurations, running multiple training jobs in parallel.
- **Jupyter notebooks** provide an interactive environment for writing and iterating on custom training code.
- **MLflow** tracks experiment runs so results can be compared; tracking is different from automatically searching algorithms.

The module introduces three phases: explore algorithms and featurization with AutoML, continue custom experimentation in notebooks with MLflow tracking, then compare trained models using performance metrics and the Responsible AI dashboard. These are planned module activities, not evidence of practical execution.

Decision rule: use AutoML for automated exploration, notebooks for custom control, and MLflow for tracking and comparison. This supports AI-300 D2 training and experiment-comparison objectives.

Tutor clarification: notebooks are not inherently limited to small experiments; the execution compute determines capacity. Moving custom notebook code into AutoML is not a mandatory next step. Do not assume arbitrary custom preprocessing is an accepted AutoML configuration; supported featurization options need separate verification in the relevant unit.

Tutor illustration, not executed: for equipment-maintenance prediction, explore candidate approaches with AutoML, use a notebook when direct control over training or preprocessing code is needed, and track custom runs with MLflow. Compare model evidence rather than choosing solely by run order or authoring tool. No SDK, CLI, or configuration code was introduced or run in this conceptual introduction.

[Optional quiz history](quizzes.md)

### M02-U02 — Preprocess data and configure featurization
Source: https://learn.microsoft.com/en-us/training/modules/experiment-azure-machine-learning/2-preprocess-data-configure-featurization

Source fetched: 2026-10-29. Conceptual study only; no code or Azure jobs were run.

#### Data preparation and MLTable

Official source: this AutoML workflow uses an **MLTable data asset**, with data stored alongside an MLTable file that describes how to read it. A registered asset provides a reusable, versioned input reference. Registration alone does not guarantee that missing values, categories, or other data-quality issues have been handled. MLTable is about the table's loading definition and transformations, not merely naming conventions.

#### Automatic numeric scaling versus optional featurization

Official source: AutoML automatically applies scaling and normalization to numeric data to help prevent large-scale features from dominating training. Optional featurization is enabled by default and can be disabled or customized, including a specific feature's imputation method. Do not interpret disabling optional featurization as disabling all automatic numeric scaling.

| Transformation | Purpose | Illustrative use |
| --- | --- | --- |
| Missing-value imputation | Supply replacement values for missing entries | Fill missing ages using a chosen rule |
| Scaling/normalization | Adjust numeric magnitudes | Put age and annual income on more comparable scales |
| Categorical encoding | Represent categories numerically | Encode city names as indicators |
| Dropping high-cardinality features | Exclude some identifier-like inputs | Evaluate whether customer IDs should be dropped |
| Feature engineering | Derive useful inputs from existing columns | Extract month or other date parts from signup dates |

After the experiment, the source says you can review the applied scaling/normalization methods and receive notifications about detected issues such as missing values or class imbalance. Automated preprocessing is not a guarantee that the data has no remaining quality problems.

#### Worked transformation examples and pitfalls

Tutor-created illustrations, not executed; no SDK/CLI version dependency for these conceptual calculations:

- **Imputation:** with known ages 25 and 55, median imputation would replace a missing age with 40. This is an estimate, not recovery of the actual age. Zero would misleadingly equate unknown age with age zero.
- **Scaling:** illustrative min–max scaling is `(age - 25) / (55 - 25)`, mapping 25 to 0 and 55 to 1. Standardization instead subtracts the mean and divides by the standard deviation. These are conceptual examples, not a claim about AutoML's selected method. Scaling neither fills missing values nor gives every feature equal predictive importance.
- **Encoding:** one-hot indicators can represent London as `(City_London=1, City_Paris=0)` and Paris as `(0, 1)`. Arbitrary integer codes can imply an order or distance that nominal categories do not possess; inspect the encoding actually used rather than assuming this example is selected.
- **High cardinality:** cardinality is the number of distinct values. A unique customer ID often identifies a row rather than providing a pattern that generalizes to unseen customers. Uniqueness does not guarantee predictive value, and scaling cannot manufacture that meaning. Many distinct values are not by themselves a universal reason to remove a feature; consider its semantics.
- **Date features:** a signup date can yield month, year, and day-of-week features that expose seasonal patterns.

Practice task: for a table containing missing ages, city names, annual income, unique customer IDs, and signup dates, map each issue to a relevant transformation. Worked solution: impute missing ages; consider scaling numeric age/income; encode cities; evaluate dropping IDs; derive date parts. This supports D2 AutoML training decisions. Practical SDK configuration and execution remain future study.

### M02-U03 — Run an automated machine learning experiment
Source: https://learn.microsoft.com/en-us/training/modules/experiment-azure-machine-learning/3-run-job

Source fetched: 2026-10-29. Conceptual study and configuration interpretation only; no Python code or Azure jobs were executed.

#### Task, target, and algorithm selection

Official source: the task determines which algorithms AutoML can try. Classification candidates include logistic regression, decision trees, random forests, LightGBM, and others. AutoML explores algorithms and featurization combinations; choosing one algorithm upfront is not required. Algorithms can be blocked for suitability or organizational policy; training properties can also restrict the candidate subset and control whether ensemble models are allowed.

Tutor clarification: the target determines the task, not whether the inputs are numeric. Predicting a yes/no maintenance category is classification; predicting a maintenance cost is regression. Blocking a prohibited algorithm still allows exploration among the permitted candidates.

#### Configure the job and ranking criterion

Tutor-adapted illustration based on the official Python SDK v2 example:

```python
from azure.ai.ml import automl

classification_job = automl.classification(
    compute="aml-cluster",
    experiment_name="maintenance-automl",
    training_data=my_training_data_input,
    target_column_name="NeedsMaintenance",
    primary_metric="accuracy",
    n_cross_validations=5,
    enable_model_explainability=True,
)
```

Prerequisites: Azure Machine Learning Python SDK v2 (`azure-ai-ml`; no exact installed version verified), an existing workspace and compute named `aml-cluster`, and `my_training_data_input` referencing an MLTable data asset. Authentication and input creation are not shown. Expected result: a local classification-job configuration, not started training. Not executed.

Official source: `primary_metric` ranks trained models and determines AutoML's best candidate. Tutor illustration: with accuracy as the metric, a model achieving 90% ranks above one achieving 80%, even if it takes longer to train. Accuracy here is illustrative, not a universal maintenance-model recommendation. `n_cross_validations=5` specifies five-fold cross-validation; tutor explanation: rotate the held-out validation portion while training on the remaining portions.

#### Limits: overall experiment, individual trials, and concurrency

Official-source example, not executed; same SDK v2 job prerequisite:

```python
classification_job.set_limits(
    timeout_minutes=60,
    trial_timeout_minutes=20,
    max_trials=5,
    enable_early_termination=True,
)
```

| Setting | Purpose |
| --- | --- |
| `timeout_minutes` | Overall experiment time limit |
| `trial_timeout_minutes` | Individual candidate-trial time limit |
| `max_trials` | Maximum total number of trials |
| `enable_early_termination` | Allow stopping when the score is not improving in the short term |
| `max_concurrent_trials` | Maximum trials running simultaneously, subject to compute capacity |

These are limits, not guarantees of exact duration or completed-trial count. Parallel trials require available compute; the source relates parallel capacity to cluster nodes. Total trial count and concurrency are separate: at most 12 trials with at most 3 running simultaneously does not mean 36 trials.

Worked configuration task (tutor-created, not executed): permit at most 12 candidates and at most 10 minutes for each candidate. Solution: `max_trials=12` and `trial_timeout_minutes=10`. `timeout_minutes=10` would instead constrain the whole experiment.

#### Submit and monitor

Official-source code, not executed:

```python
returned_job = ml_client.jobs.create_or_update(classification_job)
print("Monitor your job at", returned_job.studio_url)
```

Prerequisites: an authenticated SDK v2 `MLClient` connected to the workspace, a valid configured job and MLTable input, compute availability, and sufficient access. Expected result: a submitted job and a studio monitoring link, not necessarily a completed model. Constructing the job or calling `set_limits()` alone does not start training; printing the URL does not submit it.

Workflow: configure task/data/target/metric → set limits and training options → submit → monitor in Azure Machine Learning studio. Supports AI-300 D2 AutoML training and job comparison. Practical execution and language/CLI/configuration examples remain future module work; no JavaScript equivalent was assumed.

### M02-U04 — Evaluate and compare models
Source: https://learn.microsoft.com/en-us/training/modules/experiment-azure-machine-learning/4-evaluate-compare-models

Source fetched: 2026-11-04. Conceptual study and illustrative comparisons only; no Azure experiment, code, or studio inspection was executed.

#### Inspect results and data guardrails

Official source: the experiment's **Overview** shows its input data asset and best-model summary; the **Models** tab lists trained candidates. With featurization enabled, classification guardrails cover class balancing detection, missing feature values imputation, and high-cardinality feature detection.

| Guardrail status | Meaning and action |
| --- | --- |
| Passed | No problem detected; no action required for that check. |
| Done | AutoML applied data changes; review those changes. |
| Alerted | An issue was detected but could not be fixed; review and address the data issue. |

Tutor clarification: Done is not a reason to ignore preprocessing, and Passed does not guarantee that the entire dataset is sound. For example, missing values marked Done warrant inspecting the replacements, while high cardinality marked Alerted warrants investigating the unresolved feature issue before deployment.

#### Ranking versus deployment suitability

Official source: candidates are sorted by the configured **primary metric**, with the best-performing candidate at the top. Edit the Models tab columns to show additional metrics for a broader comparison.

Tutor-created worked example, illustrative and not executed: an accuracy-ranked experiment produces A (94% accuracy, 180 ms prediction latency) and B (93%, 40 ms). A ranks first. Only B meets an application latency requirement of under 100 ms or under 50 ms; neither meets under 30 ms. Making a latency limit stricter does not change the accuracy ranking or speed up the models. Minimum acceptable accuracy was not specified, so latency eligibility alone does not establish full deployment suitability. These distinctions support AI-300 D2 job comparison and model evaluation.

#### Preprocessing labels and model explanations

Official source: **Algorithm name** can include preprocessing and the classifier. In `MaxAbsScaler, LightGBM`, MaxAbsScaler scales each feature by its maximum absolute value, and LightGBM is the classification algorithm.

Explanations can be requested for the best model during experiment configuration. To inspect another candidate, select it and choose **Explain model**. Explanations approximate interpretability by estimating features' relative importance for the target. Tutor clarification: importance is not proof of causation, production readiness, or sufficient evidence to remove other features.

The source positions AutoML as a starting point; notebooks allow further custom experimentation, such as custom features or approaches outside AutoML's search. Practical code, CLI, and configuration examples remain future module work; no JavaScript equivalent is assumed.

### M02-U05 — Configure MLflow for model tracking in notebooks
Source: https://learn.microsoft.com/en-us/training/modules/experiment-azure-machine-learning/5-model-tracking

Source fetched: 2026-11-04. Conceptual study and illustrative Python configuration only; no installation, authentication, training, or logging was executed.

#### What MLflow Tracking records

Official source: MLflow is an open-source library for tracking and managing experiments. MLflow Tracking records **parameters**, **metrics**, and **artifacts**, allowing comparison of notebook runs and AutoML results in the workspace.

| Type | Meaning | Tutor-created example |
| --- | --- | --- |
| Parameter | A setting used for training | Learning rate `0.01`, or 100 trees |
| Metric | A measured result | Validation accuracy `0.91` |
| Artifact | A saved file associated with the run | Confusion-matrix image or trained model file |

Tutor clarification: a notebook provides interactive control over experimentation; MLflow records what was tried and the resulting evidence. Tracking does not itself perform AutoML's automated algorithm search. Recording the configuration alongside results and files helps distinguish runs when settings change.

#### Managed compute instance versus local notebook

Official source: a notebook running on an Azure Machine Learning managed **compute instance** has MLflow already configured. Verify the `mlflow` and `azureml-mlflow` packages if needed. `mlflow` provides the open-source functionality; `azureml-mlflow` provides Azure Machine Learning integration.

On a local device, install both packages, obtain the intended workspace's **MLflow tracking URI**, and explicitly configure MLflow to use it. The source directs you from the workspace name in studio to **View all properties in Azure portal**, then to the tracking URI property.

Tutor-adapted Python configuration, with an explicit import added to the source example:

```python
import mlflow

mlflow.set_tracking_uri("YOUR-WORKSPACE-TRACKING-URI")
```

Prerequisites: installed `mlflow` and `azureml-mlflow`, the actual workspace tracking URI replacing the placeholder, and authorized workspace access for subsequent remote tracking. Exact installed versions were not verified; the unit specifies the packages but no version pins. Expected outcome: MLflow is configured to use the specified tracking destination. Not executed; authentication and remote logging were not tested.

Tutor clarification: copying the URI and applying it with `set_tracking_uri()` are separate steps. Configuring the destination does not train a model or log records by itself. These distinctions support AI-300 D2 experiment-tracking objectives. Training and logging are introduced in M02-U06; no JavaScript counterpart was assumed.

#### Worked conceptual practice

Tutor-created, illustrative and not executed: classify learning rate `0.01`, measured validation accuracy `0.91`, and a saved confusion-matrix image. Worked solution: parameter, metric, and artifact respectively. For a laptop notebook with both packages installed, the remaining destination setup is to obtain the workspace tracking URI and apply it using `mlflow.set_tracking_uri()`.

### M02-U06 — Train and track models in notebooks
Source: https://learn.microsoft.com/en-us/training/modules/experiment-azure-machine-learning/6-train-models-notebooks

Source fetched: 2026-11-04. Conceptual study and illustrative Python only; no training, timing, logging, authentication, or studio inspection was executed.

#### Experiments group runs

Official source: an MLflow experiment groups related runs. Select an experiment with `mlflow.set_experiment()` and start a tracked attempt with `mlflow.start_run()`. Selecting an experiment or starting a run does not train a model; training code must execute separately.

Tutor illustration: compare models with 50, 100, and 200 trees in one `maintenance-classifier` experiment with three runs. Each run retains its own parameter settings and results. The tracking destination determines where records go; the experiment organizes related attempts within that destination. This supports AI-300 D2 training and experiment comparison.

```python
import mlflow

mlflow.set_experiment(experiment_name="maintenance-classifier")
with mlflow.start_run():
    # Training and logging code goes here.
    ...
```

Prerequisites: installed MLflow and configured tracking destination; Azure workspace integration/access as described in M02-U05 for remote tracking. The source specifies no version pins; installed versions were not verified. Expected outcome: select the named experiment and open/close a tracked run, not train a model. Illustrative, not executed.

#### Autologging and custom logging can be combined

Official source: `mlflow.autolog()` enables automatic recording for supported framework integrations. Enable it before training; the integration determines the parameters, metrics, artifacts, and models captured. Autologging records training activity, not performs training. Custom logging lets you explicitly record additional information and may be used alone or alongside autologging.

Tutor-adapted examples, not executed; same tracking prerequisites:

```python
with mlflow.start_run():
    mlflow.autolog()
    # Train the model, then measure prediction latency.
    mlflow.log_metric("prediction_latency_ms", measured_latency_ms)
```

`measured_latency_ms` must be calculated by separate code; this is a workflow sketch, not a standalone training program. If autologging already records the tree count, no additional manual tree-count record is needed for that purpose. Add custom metric logging for latency if it is not captured by the integration.

```python
with mlflow.start_run():
    mlflow.log_param("n_trees", 100)
    mlflow.log_metric("prediction_latency_ms", 42.0)
    mlflow.log_artifact("validation_report.txt")
```

Expected outcome: record a parameter, a numeric metric, and an existing file. The report must already exist. These calls do not train a model, measure latency, or create the report. Framework compatibility and actual execution remain unverified; no JavaScript counterpart is assumed.

#### Worked practice and logging pitfalls

Tutor-created conceptual tasks, not executed:
- Compare three tree-count settings: use one experiment and three runs, preserving each run's settings and results.
- Add latency when standard training information is autologged: retain autologging and add `mlflow.log_metric()` for the independently measured latency.
- Attach an existing validation report: use `mlflow.log_artifact()`; recording its path with `log_param()` stores text, not the file itself.

Distinguish **measurement** from **logging**: `mlflow.log_metric("prediction_latency_ms", 42.0)` records the supplied number. It does not prove that MLflow timed predictions or that the number was measured correctly. Parameters are settings, metrics are numeric results, and artifacts are files—not interchangeable categories of “training information.”

### M02-U07 — Evaluate models with the Responsible AI dashboard
Source: https://learn.microsoft.com/en-us/training/modules/experiment-azure-machine-learning/7-responsible-ai-dashboard

Source fetched: 2026-11-04; page updated 2026-08-27. Conceptual study and tutor-created hospital scenarios only; no dashboard pipeline, SDK, CLI, or configuration was executed. Practical creation prerequisites and API versions remain to be verified before an executable example.

#### Evaluate beyond overall accuracy

Official source: model evaluation should consider fairness, transparency, and reliability as well as accuracy. Microsoft's six Responsible AI principles are fairness; reliability and safety; privacy and security; inclusiveness; transparency; and accountability. Minimal personal-data collection supports privacy, while traceable human oversight supports accountability. The dashboard assists evaluation; it does not replace governance or establish compliance with every principle.

#### Choose the analysis for the question

| RAI tool | Purpose and views |
| --- | --- |
| Error Analysis | Identify higher-error subgroups. An error tree map reveals combinations of subgroup characteristics; an error heat map compares errors across one or two features. |
| Explanation | Estimate feature influence. Aggregate importance summarizes influence across test data; individual importance explains one prediction. |
| Counterfactuals | Explore minimal input changes that would flip a selected prediction to a desired outcome. |
| Causal | Use historical data and statistical methods to estimate effects on actual outcomes, including possible interventions. |

Tutor clarification: a data feature (such as age or clinic) is not a training parameter. Drilling into an error tree means examining data subgroups, not tuning hyperparameters. A heat map is a view within Error Analysis, not a separate pipeline component.

Feature importance is not causal proof. Counterfactual prediction changes likewise do not guarantee improved real-world outcomes. Causal estimates depend on statistical methods and assumptions; they are not automatic proof. Explanations and error patterns provide investigation leads rather than guaranteed diagnoses or fixes.

#### Construct and open the dashboard

Official pipeline structure:

**RAI Insights dashboard constructor → one or more RAI tool components → Gather RAI Insights dashboard.**

Available tools are `Add Explanation to RAI Insights dashboard`, `Add Error Analysis to RAI Insights dashboard`, `Add Counterfactuals to RAI Insights dashboard`, and `Add Causal to RAI Insights dashboard`. Select relevant tools; including every tool is not required. Build with Python SDK, CLI, or studio's no-code experience. After successful pipeline completion, open the dashboard from the pipeline overview or the registered model's **Responsible AI** tab.

This is a source-described conceptual structure, not an executable configuration. No unsupported JavaScript equivalent is assumed. It supports AI-300 D2 responsible AI evaluation.

#### Worked hospital analysis example

Tutor-created, illustrative and not executed:

- Strong overall performance can conceal errors among older patients at specific clinics. Start with Error Analysis; use an age-by-clinic heat map or a tree map for subgroup combinations.
- To explain one patient's high-risk prediction, use **individual**, not aggregate, feature importance.
- To explore small input changes that would flip that prediction, use Counterfactuals. Do not treat a prediction flip as evidence of improved health.
- For subgroup errors and individual explanations, include Error Analysis and Explanation between the constructor and Gather. Their findings guide investigation; they do not establish what causes medical outcomes.

### M02-U08 — Exercise - Find the best classification model with Azure Machine Learning
Source: https://learn.microsoft.com/en-us/training/modules/experiment-azure-machine-learning/8-exercise

Pending exercise. Add the studied task and worked solution with execution context; label any equivalent substitute. Preserve learner outcomes and deferred-work status in memory.

### M02-U09 — Module assessment
Source: https://learn.microsoft.com/en-us/training/modules/experiment-azure-machine-learning/9-knowledge-check

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this closing unit; it is excluded from tutor completion, review scheduling, and TLDR readiness. No website confirmation is required.

### M02-U10 — Summary
Source: https://learn.microsoft.com/en-us/training/modules/experiment-azure-machine-learning/10-summary

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this closing unit; it is excluded from tutor completion, review scheduling, and TLDR readiness. No website confirmation is required.

## Key concepts and decision points
Pending study.

## Python examples
Pending study. Record prerequisites/versions, expected outcomes, and execution status.

## JavaScript examples
Pending study. Use relevant supported examples only.

## Azure CLI commands
Pending study. Record CLI/extension prerequisites and expected outcomes.

## Related configuration: YAML, Bicep, or GitHub Actions
Pending study.

## Worked examples and practice
Pending study. Include unit IDs, useful tasks, worked solutions, prerequisites, and execution status. Keep learner-response histories and assessment outcomes in memory.

## Common pitfalls and clarifications
Pending study. Add reusable conceptual explanations as topics are studied.

## Microsoft Learn search terms
- Azure Machine Learning AutoML classification featurization
- MLflow notebook experiment tracking
- Azure Machine Learning Responsible AI dashboard
