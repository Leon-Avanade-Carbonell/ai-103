# Automate model training with GitHub Actions

- Module ID: M06
- Source: https://learn.microsoft.com/en-us/training/modules/trigger-azure-machine-learn-jobs-github-actions/
- Curriculum verified: 2026-10-28
- Exam objectives: D1 GitHub authentication/source control; D2 automated training.

## Overview and learning goals

Planned source goals: decide which ML assets belong in Git or specialized stores, apply trunk-based development, validate changes through GitHub Actions, compare authentication approaches including OIDC, and submit AML jobs/pipelines from workflows.

## Notes by Microsoft Learn unit

### M06-U01 — Introduction
Source: https://learn.microsoft.com/en-us/training/modules/trigger-azure-machine-learn-jobs-github-actions/1-introduction

Source verified: 2026-11-12.

#### Why automate model training?

Microsoft Learn explains that manual training does not scale well when teams iterate frequently, retrain on fresh data, or need to trace model versions to reviewed and approved changes. Automation supports repeatable execution, validation of proposed changes, and an auditable connection between code changes and model versions.

The module introduces source control for ML assets, trunk-based development, automatic validation with GitHub Actions, secure Azure authentication, and submission of Azure Machine Learning jobs from GitHub events or Azure-side signals. These are planned module topics, not implementation work performed in this introduction.

#### Orchestration versus training and validation

Conceptual tutor illustration: **GitHub change → Actions workflow → Azure ML training job → results checked**. GitHub Actions coordinates automation; Azure ML executes the submitted training job. This connects D1 source control/secure automation with D2 automated model training.

Successful execution alone does not demonstrate acceptable model quality. A workflow should also apply relevant quality checks and retain traceability to the reviewed change.

#### Worked application: detect a regression

Tutor-created practice scenario, conceptual only; no code was run: a teammate changes data preparation, training completes successfully, but model performance worsens. Why is job success insufficient, and what additional check is useful?

Worked solution: job success establishes that execution finished, not that the resulting model meets quality requirements. Check the primary metric against a defined acceptance threshold and compare it with a previous accepted model. The metric-comparison idea arose in the learner's application reasoning; thresholds and an accepted baseline are tutor elaborations. Use comparable evaluation conditions: changing the evaluation dataset can confound interpretation of a metric difference.

No SDK, CLI, or workflow implementation was studied or executed here; relevant implementation examples remain pending for later units.

### M06-U02 — Use source control for machine learning assets
Source: https://learn.microsoft.com/en-us/training/modules/trigger-azure-machine-learn-jobs-github-actions/2-understand-business-problem

Source verified: 2026-11-12.

#### What belongs in Git

Microsoft Learn places the assets defining how a model is produced in source control: training/preprocessing scripts, job and component YAML definitions, environment/dependency files such as `requirements.txt` and `conda.yml`, and nonsecret configuration references such as workspace, resource group, and compute names. Git supports shared code, reviewable changes, and recovery of an earlier training recipe.

#### What doesn't belong in Git

- Datasets/raw data: use Azure ML data assets or Azure Data Lake Storage; version data separately from code.
- Trained model artifacts: register named, versioned model assets in Azure ML.
- Training outputs and logs: retain them with the Azure ML job.
- Secrets/credentials: use GitHub secrets or Azure Key Vault, not the repository.

A workspace name is nonsecret configuration; a credential granting access is sensitive. Text-based files defining the recipe generally belong in Git, but being text-based does not make a secret safe to commit.

#### Why source control matters for machine learning

The official source connects Git to collaboration, code review, reproducibility, and an audit trail linking model versions to producing changes. This supports D1 source control/workspace assets and D2 model lifecycle traceability.

Tutor clarification: a commit identifies code/configuration, but does not automatically contain a model link or its dataset. Record the producing commit in job/model metadata as part of traceability. A job's retained model output is distinct from a registered, named/versioned model asset.

Recovering an existing model artifact is not the same as reproducing training. To retrain reproducibly, identify code, data version, dependencies/environment, and training settings; randomness can also affect results. Returning to a code commit alone does not guarantee the same trained model.

#### Worked asset-placement and reproducibility examples

Tutor-created conceptual exercises; no code or Azure operations were executed. No SDK/CLI version requirement applies to these conceptual examples; implementation remains pending in the appropriate later topics.

| Asset | Suitable home | Reason |
| --- | --- | --- |
| `train.py` | Git repository, for example GitHub | Version and review the training recipe |
| 20-GB dataset | Azure Data Lake Storage, with its version identified for training | Keep large data outside Git and trace training inputs |
| Azure access credential | Azure Key Vault or GitHub secrets | Keep sensitive access values out of source control |
| `model.pkl` | Registered Azure ML model asset; original output may also remain with its job | Manage the trained artifact by name and version |

Scenario: restore the original Git commit, but train on a newer dataset. Worked conclusion: the resulting model may differ because the training data changed. Ordinary training uses code/data/environment/settings to produce a model; it need not consume the previous model unless deliberately resuming or fine-tuning.

### M06-U03 — Apply trunk-based development
Source: https://learn.microsoft.com/en-us/training/modules/trigger-azure-machine-learn-jobs-github-actions/3-explore-solution-architecture

Pending study.

### M06-U04 — Validate changes with GitHub Actions
Source: https://learn.microsoft.com/en-us/training/modules/trigger-azure-machine-learn-jobs-github-actions/4-use-for-model-training

Pending study.

### M06-U05 — Connect GitHub Actions to Azure Machine Learning securely
Source: https://learn.microsoft.com/en-us/training/modules/trigger-azure-machine-learn-jobs-github-actions/5-connect-github-actions-azure

Pending study.

### M06-U06 — Trigger Azure Machine Learning jobs and pipelines
Source: https://learn.microsoft.com/en-us/training/modules/trigger-azure-machine-learn-jobs-github-actions/6-trigger-azure-machine-learning-jobs

Pending study.

### M06-U07 — Exercise
Source: https://learn.microsoft.com/en-us/training/modules/trigger-azure-machine-learn-jobs-github-actions/5-exercise

Pending exercise. Add the studied task and worked solution with execution context; label any equivalent substitute. Preserve learner outcomes in memory.

### M06-U08 — Module assessment
Source: https://learn.microsoft.com/en-us/training/modules/trigger-azure-machine-learn-jobs-github-actions/6-knowledge-check

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this closing unit; it is excluded from tutor completion, review scheduling, and TLDR readiness. No website confirmation is required.

### M06-U09 — Summary
Source: https://learn.microsoft.com/en-us/training/modules/trigger-azure-machine-learn-jobs-github-actions/7-summary

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

[Quiz history](quizzes.md)

## Common pitfalls and clarifications
Pending study. Add reusable conceptual explanations as topics are studied.

## Microsoft Learn search terms
- GitHub Actions Azure Machine Learning OIDC federation
- trunk based development machine learning assets
- Azure Machine Learning repository_dispatch training pipeline
