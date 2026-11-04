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

Pending study.

### M03-U03 — Run a script as a command job
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/3-run-script-command-job

Pending study.

### M03-U04 — Use parameters in a command job
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/4-use-parameters-command-job

Pending study.

### M03-U05 — Track metrics with MLflow
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/5-track-metrics

Pending study.

### M03-U06 — View metrics and evaluate models
Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/6-view-metrics-evaluate-models

Pending study.

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
- Azure Machine Learning command job parameters
- MLflow log metrics artifacts models Azure
- convert notebook training script Azure Machine Learning
