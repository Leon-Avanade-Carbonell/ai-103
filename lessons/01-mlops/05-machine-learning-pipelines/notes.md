# Run pipelines in Azure Machine Learning

- Module ID: M05
- Source: https://learn.microsoft.com/en-us/training/modules/run-pipelines-azure-machine-learning/
- Curriculum verified: 2026-10-28
- Exam objectives: D1 components; D2 training pipelines.

## Overview and learning goals

Planned source goals: create reusable components, build an Azure Machine Learning pipeline, and run it as a pipeline job.

[Optional quiz history](quizzes.md)

## Notes by Microsoft Learn unit

### M05-U01 — Introduction
Source: https://learn.microsoft.com/en-us/training/modules/run-pipelines-azure-machine-learning/1-introduction

#### Components, pipelines, and executions

Official source explanation (verified 2026-11-12): notebooks and script jobs support experimentation and training. For an enterprise ML process, separate the work into individual tasks. Package tasks as reusable, shareable **components**, combine them into a **pipeline**, and execute the workflow as a **pipeline job**.

- **Component:** A reusable task implemented by code, such as data preparation.
- **Pipeline:** The workflow connecting individual tasks.
- **Pipeline job:** A particular execution of that workflow.
- **Model:** The artifact produced by model training, not the data-preparation task itself.

These concepts connect to D1 reusable components and D2 training pipelines. This introduction establishes the roles; implementation remains for the following units.

#### Distinguishing pipelines across services

Microsoft Learn distinguishes Azure Machine Learning pipelines for ML training tasks from build/release pipelines in GitHub or Azure DevOps and ingestion/transformation pipelines in Azure Synapse Analytics. These services can interact: an external pipeline can trigger an Azure Machine Learning pipeline without replacing its ML workflow.

#### Illustrative workflow and reuse decision

Tutor-created conceptual example, not executed; no SDK or CLI prerequisites are needed for this diagram:

```text
GitHub Actions trigger → Azure ML pipeline job
                        Prepare data → Train model → Evaluate model
```

If several training workflows need the same data-cleaning code, package that task as a reusable **component**. Each Azure ML pipeline organizes the tasks for its workflow. Reusing a trained model is a different decision: it reuses a training output rather than the preparation code. GitHub Actions can trigger execution when code changes; the diagram is an illustration, not a configured automation or evidence of a successful run.

### M05-U02 — Create components
Source: https://learn.microsoft.com/en-us/training/modules/run-pipelines-azure-machine-learning/2-create-components

#### Component structure and purpose

Official source explanation (verified 2026-11-12): components package specific tasks as reusable code, supporting pipeline construction and sharing ready-to-go code among workspace users. A component has three parts:

| Part | Contents |
| --- | --- |
| Metadata | Name, version, and identifying information |
| Interface | Expected inputs, such as data or hyperparameters, and outputs, such as artifacts |
| Command, code, and environment | The script, how to invoke it, and its runtime/dependencies |

Sharing a script alone does not supply its complete component contract. A data-preparation component defines the reusable task; the cleaned dataset is its output, not the component itself. These distinctions support D1 component assets and D2 training pipelines.

#### Loading, executing, and registering

Loading a local YAML definition creates a component object that can be used to build a pipeline. **Registration is not required to use a local component in a pipeline.** Loading itself does not execute the task; submitting the pipeline job executes its steps. Running the script directly is a separate operation that does not use the component definition.

Registering the component creates or updates a workspace asset for other workspace users to reuse. Keep the script and local YAML definition together when using an unregistered local component.

Source-derived Python SDK v2 example, illustrative and not executed. Prerequisites: `azure-ai-ml`; registration also requires an authenticated `MLClient` named `ml_client`, access to the target workspace, and suitable permissions. No installed package version or successful execution was verified.

```python
from azure.ai.ml import load_component

component = load_component(source="./train.yml")
# Optional for local pipeline use; publishes the workspace asset:
registered_component = ml_client.components.create_or_update(component)
```

Expected outcomes: the first call loads the local definition; the second registers the asset. This snippet does not build or submit a pipeline.

#### Mapping component ports to script arguments

Tutor-created YAML fragment, illustrative and not executed; not a complete component definition. A complete definition also needs metadata, type, code location, and a valid environment. The accompanying script must accept the indicated arguments and write its artifact into the supplied output directory.

```yaml
inputs:
  training_data:
    type: uri_file
outputs:
  model:
    type: uri_folder
command: >-
  python train.py
  --data ${{inputs.training_data}}
  --model-dir ${{outputs.model}}
```

Component port names and script argument names are separate. Renaming the component input to `raw_data` requires changing its declaration and the reference to `${{inputs.raw_data}}`, but the script can still accept `--data`:

```yaml
command: >-
  python train.py --data ${{inputs.raw_data}}
```

Likewise, an input named `lr` maps to a script flag named `--learning-rate` using `--learning-rate ${{inputs.lr}}`. Rename a command-line flag only if the script's argument parser also supports the new flag.

#### Source example caveats

The source preparation script treats its output path as a directory and writes `prepped-data.csv` inside it, while its YAML declares that output as `uri_file`. For this directory-writing pattern, use `uri_folder` (tutor clarification). The source environment example references Python 3.7/scikit-learn 0.24 on Ubuntu 18.04; it is not a current recommended dependency stack. Environment availability and compatibility were not tested. Select a currently supported environment before actual execution.

### M05-U03 — Create a pipeline
Source: https://learn.microsoft.com/en-us/training/modules/run-pipelines-azure-machine-learning/3-create-pipeline

#### Workflow dependencies and compute

Official source explanation (verified 2026-11-12): a pipeline connects reusable components sequentially or in parallel. Executing it creates an overall pipeline job with component executions as child jobs. Components can use different compute targets. These decisions connect to D1 reusable components and D2 training pipelines.

Tutor-created dependency example, illustrative and not executed:

```text
Prepare → Train → Evaluate
    └────────────→ Evaluate (evaluation data)
```

Train waits for Prepare's cleaned data. Evaluate waits for both its data and Train's model, so Train and Evaluate cannot run in parallel in this graph. Two training steps that depend only on Prepare could run in parallel if resources permit. Input/output connections establish dependencies; simply listing Python calls in order is not the dependency mechanism. For real model evaluation, use held-out evaluation data rather than evaluating on the training data; the graph illustrates wiring only.

#### Build the graph and expose outputs

Source-adapted Python SDK v2 illustration, not executed. Prerequisites: `azure-ai-ml` and already-loaded components with the port names shown. No installed SDK version or component environment was verified. The current [DSL API reference](https://learn.microsoft.com/en-us/python/api/azure-ai-ml/azure.ai.ml.dsl?view=azure-python), fetched 2026-11-12, confirms the decorator builds a `PipelineJob` object.

```python
from azure.ai.ml.dsl import pipeline

@pipeline()
def training_pipeline(raw_data):
    prep = prepare_component(input_data=raw_data)
    train = train_component(training_data=prep.outputs.cleaned_data)
    evaluate = evaluate_component(
        model=train.outputs.model,
        test_data=prep.outputs.cleaned_data,
    )
    return {
        "trained_model": train.outputs.model,
        "evaluation_report": evaluate.outputs.report,
    }
```

The component calls create nodes in the graph. Passing `train.outputs.model` into Evaluate connects steps internally. Returning selected outputs exposes them as pipeline-level outputs. Removing `trained_model` from the return dictionary does not remove Train's child-job output or break Evaluate's existing connection; it only removes that named pipeline-level output. The artifact may still be accessed through the child job.

#### Supply versioned data without executing the job

Source-adapted illustration, not executed; requires the preceding pipeline definition and Python SDK v2. When run in Azure ML, the target workspace must contain a compatible file-type data asset named `data`, version `1`, and the component runtimes and compute must be configured appropriately.

```python
from azure.ai.ml import Input
from azure.ai.ml.constants import AssetTypes

pipeline_job = training_pipeline(
    raw_data=Input(type=AssetTypes.URI_FILE, path="azureml:data:1")
)
print(pipeline_job)
```

Expected outcome: build the job object and display its YAML representation, without running Prepare, Train, or Evaluate. `azureml:data:1` identifies a specific registered data-asset version. Printing does not itself save a YAML file. The unit describes YAML-based definitions; the API reference clarifies that the decorated function returns a job object.

**Definition location is not execution location.** Creating the object in a local Python process does not assign the laptop as a compute target or configure local component execution. Submission is separate; after submission, steps execute on the configured compute targets. A pipeline can use a default compute target and step-specific targets. Building a work order on a laptop is distinct from deciding where the work runs.

### M05-U04 — Run a pipeline job
Source: https://learn.microsoft.com/en-us/training/modules/run-pipelines-azure-machine-learning/4-run-pipeline-job

#### Configure, inspect, and submit

Official source explanation (fetched 2026-11-12): configure the built pipeline job before submitting it. `default_compute` supplies the execution target for components without another target; `default_datastore` supplies the default output storage destination. A datastore is not execution compute. Printing the job inspects its configuration without starting component execution.

Source-adapted Python SDK v2 illustration, not executed. Prerequisites: `azure-ai-ml`, an authenticated workspace `MLClient` named `ml_client`, an already-built valid `pipeline_job`, access to the named compute/datastore, suitable permissions, and compatible component environments. No installed SDK version or runtime setup was verified.

```python
pipeline_job.settings.default_compute = "aml-cluster"
pipeline_job.settings.default_datastore = "workspaceblobstore"
print(pipeline_job)

submitted_job = ml_client.jobs.create_or_update(
    pipeline_job, experiment_name="pipeline_job"
)
```

Expected outcomes: configure and inspect the job, then submit it to the workspace. Submission does not itself establish successful completion. Tutor-created worked example: if Prepare has no specific compute and Train specifies `gpu-cluster`, a pipeline default of `cpu-cluster` sends Prepare to CPU and Train to GPU. The location where Python constructs the job does not select execution compute.

#### Troubleshoot at the appropriate job scope

The submitted parent pipeline job contains child jobs for component executions; Azure ML studio displays the graph, parameters, outputs, and child jobs. The source recommends inspecting parent pipeline outputs/logs for pipeline-configuration failures and the relevant child job's outputs/logs for component failures.

Tutor-created worked example, conceptual and not executed: Prepare succeeds but Train fails with “module not found.” Start with Train's child-job logs to diagnose its runtime/dependency issue, rather than inspecting only the parent overview or Prepare's output.

#### Schedule recurring pipeline runs

Official source explanation: `RecurrenceTrigger` specifies timing using `frequency` (`minute`, `hour`, `day`, `week`, or `month`) and an integer `interval`. `JobSchedule` associates that trigger with the pipeline definition supplied as `create_job`.

Source-adapted SDK v2 illustration, not executed; uses the preceding workspace/pipeline prerequisites and requires permission to manage schedules. No installed SDK version or schedule execution was verified.

```python
from azure.ai.ml.entities import JobSchedule, RecurrenceTrigger

trigger = RecurrenceTrigger(frequency="week", interval=2)
schedule = JobSchedule(
    name="retrain_every_two_weeks",
    trigger=trigger,
    create_job=pipeline_job,
)
ml_client.schedules.begin_create_or_update(schedule=schedule).result()
```

Expected outcome: create a schedule that triggers the pipeline every two weeks, not proof that any resulting run succeeds. To express every three days, use `RecurrenceTrigger(frequency="day", interval=3)`.

The source requires disabling a schedule before deleting it. Stopping future scheduled triggers is distinct from diagnosing a failed run.

Tutor clarification for D2 lifecycle automation: a time-based schedule is not a data-drift detector. Scheduling retraining does not automatically deploy or replace a production model; that requires explicit workflow steps and appropriate model validation/deployment gates. No Azure execution or production deployment was performed here.

### M05-U05 — Exercise - Run a pipeline job
Source: https://learn.microsoft.com/en-us/training/modules/run-pipelines-azure-machine-learning/5-exercise-run-pipeline-job

Pending exercise. Add the studied task and worked solution with execution context; label any equivalent substitute. Preserve learner outcomes in memory.

### M05-U06 — Module assessment
Source: https://learn.microsoft.com/en-us/training/modules/run-pipelines-azure-machine-learning/6-knowledge-check

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this closing unit; it is excluded from tutor completion, review scheduling, and TLDR readiness. No website confirmation is required.

### M05-U07 — Summary
Source: https://learn.microsoft.com/en-us/training/modules/run-pipelines-azure-machine-learning/7-summary

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
- Azure Machine Learning reusable components
- Azure Machine Learning SDK v2 pipeline job inputs outputs
- Azure Machine Learning pipeline YAML
