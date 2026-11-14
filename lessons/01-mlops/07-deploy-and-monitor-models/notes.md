# Deploy and monitor a model in Azure Machine Learning

- Module ID: M07
- Source: https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/
- Curriculum verified: 2026-10-28
- Exam objectives: D2 model registration/versioning, production deployment, monitoring.

## Overview and learning goals

Planned source goals: register/version/archive MLflow models, use GitHub environments for promotion controls, deploy/troubleshoot managed online endpoints, safely promote/roll back models, automate testing/deployment, and monitor retraining signals.

## Notes by Microsoft Learn unit

### M07-U01 — Introduction
Source: https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/1-introduction

Source verified: 2026-11-13. This introduction establishes the module's production-lifecycle goals; implementation details remain for later units.

#### Production responsibility continues after deployment

The official scenario is Proseware, a health care technology company whose classification model predicts missed clinic appointments. Staff use no-show risk scores to decide whom to call ahead of time. The machine learning engineer must turn the trained model into a reliable production service through a repeatable, automated process.

The lifecycle covered by this module is **register/version → deploy/test → safely promote or roll back → monitor → investigate and, when appropriate, retrain**. Azure Machine Learning manages MLflow model versions and managed online endpoints. GitHub environments protect production promotion through access controls and approvals; GitHub Actions automate deployment and testing. These goals connect to D2 model lifecycle and operations.

#### Predictive quality versus operational reliability

Tutor clarification: monitor both whether predictions remain useful and whether the deployed service responds successfully and promptly. Good historical evaluation results do not establish current production quality. Evaluation on recent examples requires actual outcomes or labels when available. A reliable service can make poor predictions, and an accurate model can be unavailable when users need it.

Tutor illustration (conceptual; no code executed): strong historical performance for a clinic model does not establish that its deployed service handles requests reliably or that predictions remain useful as patient behavior changes. Monitoring signals call for investigation; retraining is not automatically the correct remedy for every production problem.

Useful recap task: identify one predictive-quality concern and one service-reliability concern after deployment, and explain why both matter. Worked reasoning: assess predictions against observed appointment outcomes when available, and monitor request failures and response times so staff can use the service reliably.

### M07-U02 — Prepare a model for deployment
Source: https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/2-understand-business-problem

Source verified: 2026-11-13. The official unit covers endpoint choice, MLflow registration, version lifecycle, and repeatable deployment.

#### Choose by prediction-consumption requirements

An online endpoint returns a prediction synchronously with low latency. A batch endpoint scores many records without an immediate per-request response; a scheduled job can invoke it for periodic scoring. Production use does not imply online serving.

Official scenario: Proseware needs a no-show risk prediction when an appointment is booked or rescheduled, so it selects a managed online endpoint. Tutor-created conceptual example: score tomorrow's 40,000 appointments overnight to produce a morning call list using scheduled batch scoring. No code or deployment was executed.

#### MLflow packaging and model registration

MLflow packages models in a standard format. The source describes `mlflow.autolog()` logging the model, parameters, and metrics during training; actual behavior depends on a supported framework/integration and configuration. For supported MLflow no-code deployment, Azure Machine Learning generates the scoring script and environment from model metadata. This does not mean the entire release workflow requires no code. A custom model format, such as a pickle file, requires an authored scoring script and environment in the source's comparison.

Register from a completed training job's output or model files in a workspace datastore. Registration creates a versioned workspace asset referenceable by name and version; registration alone does not serve predictions. Implementation examples and SDK/CLI prerequisites remain for later study; no APIs were executed here.

#### Version lifecycle and repeatable releases

- Changed model artifacts require a new registered version, rather than replacement of an existing version's artifact.
- An existing version's description and tags can be updated.
- Archiving hides versions from default lists; it does not delete them or prevent workflows from referencing them.

Tutor illustration: preserving `no-show:1` alongside `no-show:2` gives deployment and rollback workflows explicit artifacts to target. Actual rollback implementation is a later topic.

Recurring retraining motivates automation of **registration → deployment → testing**, reducing slow, error-prone manual repetition. Tutor clarification: reliable release automation is not a guarantee of predictive accuracy. A pipeline can consistently deploy a poor model; evaluation and testing remain necessary. These decisions connect to D2 registration/versioning and production deployment.

### M07-U03 — Explore the deployment and monitoring architecture
Source: https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/3-explore-solution-architecture

Pending study.

### M07-U04 — Control deployments with GitHub environments
Source: https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/4-control-deployments-github-environments

Pending study.

### M07-U05 — Deploy, promote, and roll back a model with GitHub Actions
Source: https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/4-model-deployment

Pending study.

### M07-U06 — Monitor the deployed model
Source: https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/5-monitor-model

Pending study.

### M07-U07 — Exercise
Source: https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/5-exercise

Pending exercise. Add the studied task and worked solution with execution context; label any equivalent substitute. Preserve learner outcomes in memory.

### M07-U08 — Module assessment
Source: https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/6-knowledge-check

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this closing unit; it is excluded from tutor completion, review scheduling, and TLDR readiness. No website confirmation is required.

### M07-U09 — Summary
Source: https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/7-summary

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

Optional quiz participation and results: [Quiz history](quizzes.md).

## Common pitfalls and clarifications
Pending study. Add reusable conceptual explanations as topics are studied.

## Microsoft Learn search terms
- Azure Machine Learning MLflow model register archive
- managed online endpoint traffic rollout rollback GitHub Actions
- Azure Machine Learning model monitoring data drift retraining
