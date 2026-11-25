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

Source verified: 2026-11-16. The official unit presents a simplified MLOps architecture and explains automation with human review; implementation details are covered in later units.

#### Registration is the handoff, not the finish line

The official architecture is **setup → model development (inner loop) → continuous integration → model deployment (outer loop) → continuous deployment → monitoring**:

- Setup creates the required Azure resources.
- Model development explores data and trains/evaluates candidates.
- Continuous integration packages and registers the model.
- Model deployment deploys it to an endpoint.
- Continuous deployment tests the deployment and safely promotes it to production.
- Monitoring tracks endpoint operational health and model predictions over time.

Registration is the hinge between the first three and last three stages. A registered version is a deployable asset, not a running prediction service. Good evaluation results and registration do not eliminate deployment, deployment testing, or safe production promotion. This connects to D2 model lifecycle and production deployment.

#### Automate repetitive work while retaining judgment

Official scenario: Proseware regularly retrains and redeploys its no-show model. GitHub Actions automates registration, deployment, and testing, with a workflow triggered when a new model version is ready. This reduces repetitive manual work so the team can focus on reviewing quality. Automation does not replace human judgment: production promotion and investigation of monitoring alerts can retain a person in the loop.

Deployment and promotion are distinct. A version can already be deployed for testing without receiving full production traffic. Tutor clarification: in a release with a reviewer gate, the sequence is **deploy → test → approval → promote to full production traffic → monitor**. Scheduling considerations and satisfaction with the output are useful reasons for human review; these are illustrative decision criteria, not guarantees of model quality or a specified approval configuration from this unit.

#### Conceptual practice: release a registered version

Tutor-created example (illustrative; no code, workflow, or Azure deployment executed): `no-show:7` has been registered and evaluated but is not serving requests. Deploy that version to an endpoint, test the deployment, obtain the required approval before full production promotion, then monitor both operational health and predictions. An approval gate does not contradict automation: automated steps and controlled release decisions can coexist. Actual GitHub environment configuration remains for the following unit.

### M07-U04 — Control deployments with GitHub environments
Source: https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/4-control-deployments-github-environments

Source verified: 2026-11-16. The official unit covers deployment stages, protection rules, scoped configuration, and identity separation. The examples below are conceptual; no GitHub configuration, workflow, or Azure deployment was executed.

#### Deployment targets versus runtime environments

A GitHub environment is a named deployment target in a repository, such as `staging` or `production`. A workflow job references it; GitHub evaluates its protection rules before the job runs or accesses environment secrets. Naming an environment does not provision Azure resources. Teams explicitly map targets to resources, for example separate Azure ML workspaces for stronger isolation or separate endpoints in one workspace for lower management overhead.

An Azure ML environment instead defines the operating system, packages, and dependencies used to run ML code. It is independent of a GitHub environment's deployment controls.

#### Gate the action that changes production

Separate deployment/testing from promotion: deploy and test the candidate without production traffic, then use a later job referencing the protected `production` environment to change traffic after approval. Protection rules can require reviewers, restrict allowed branches or tags, or add a wait timer. The official Proseware scenario permits production runs from `main` and requires a reviewer to examine staging test results.

Automated tests determine whether defined requirements are met; reviewers decide whether the release should proceed now, considering evidence and operational context. An allowed branch is not evidence that tests passed. Tutor-created worked example: if a candidate comes from `main` but staging deployment tests fail, investigate and resolve the failure, then obtain passing test evidence before promotion. Approval needs clear acceptance criteria; it is not a substitute for testing. These controls support D2 safe production deployment.

#### Configuration, authentication, and authorization

Environment variables hold non-sensitive target settings such as workspace and endpoint names. Environment secrets are available only to jobs referencing that environment and only after its protection rules pass.

OIDC avoids storing an Azure client secret but does not itself establish staging–production isolation. The source recommends different federated identities for staging and production, with each granted only the Azure permissions its job requires. Tutor clarification: authentication establishes identity; Azure RBAC authorizes resource operations. An already overprivileged staging identity needs narrower RBAC scope, not simply more permissions.

Tutor-created conceptual practice: a staging identity can modify both staging and production endpoints. Separate the identities and restrict staging permissions to its required staging resources; use the appropriately authorized production identity in the approval-protected promotion job. This reinforces the gate with least-privilege access. Practical identity, RBAC, and workflow configuration remain unverified; no implementation example was executed.

### M07-U05 — Deploy, promote, and roll back a model with GitHub Actions
Source: https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/4-model-deployment

Source verified: 2026-11-16. Studied concepts below cover endpoint/deployment separation, direct testing, progressive traffic allocation, and rollback. GitHub Actions automation and its CLI/YAML implementation remain pending study. All examples below are conceptual tutor illustrations; no commands, workflows, or Azure deployments were executed.

#### Stable endpoint, replaceable deployments

The official source distinguishes a managed online endpoint's stable HTTPS address from its deployments, which host specific model versions and runtime resources. The endpoint can contain multiple deployments, letting the client keep the same URL while the serving model changes beneath it. A deployed candidate is not necessarily promoted to production traffic.

Tutor illustration: `blue` hosts model version 7 at 100% of normal traffic, while `green` hosts version 8 at 0%. Traffic allocations target deployment names, not registered model version numbers directly.

#### Direct tests before user-facing traffic

Wait for green to finish provisioning, then send test requests directly to that deployment and compare responses with expected results. Direct invocation bypasses normal endpoint traffic routing, so green can be tested while blue continues to receive 100% of normal production traffic. Zero allocated traffic does not mean the deployment cannot receive deliberately targeted test requests.

An 80% blue / 20% green split instead sends 20% of normally routed requests to green and returns its predictions to those clients. This is a limited live rollout, not an isolated test.

#### Progressive promotion and acceptance criteria

The source recommends introducing the candidate alongside the existing deployment, testing it first, then shifting traffic gradually and observing production behavior before further promotion. Its illustrative initial split is 90% blue / 10% green; a particular percentage is not a universal safety guarantee.

Tutor-created practice and worked reasoning: start with representative inputs and important edge cases, directly target green, and validate expected responses before a limited live rollout. Live requests can supply a wider variety of inputs, but greater input diversity alone does not prove predictive improvement. Check service health, such as errors and latency, and prediction quality against defined acceptance criteria, with actual outcomes or labels when available. These conceptual distinctions support D2 deployment testing and progressive rollout.

#### Roll back traffic, then investigate

Retain the healthy blue deployment through green's observation period. If green produces frequent errors or unacceptable predictions, restore normal traffic to **blue=100%, green=0%**. Traffic reassignment preserves the endpoint URL and avoids deleting and recreating the endpoint for recovery. Investigate green without continuing to expose normal users to it; when blue is healthy, finishing root-cause diagnosis need not precede restoring service.

Tutor-created conceptual task: green receives 20% of live traffic and begins failing while blue remains healthy. Worked solution: redirect traffic fully to blue, then inspect green's health and errors. Only retire the old deployment after the replacement meets acceptance criteria for the required observation period. The exact recovery allocation is a worked solution; implementation and execution remain pending.

Overall sequence: **deploy green → wait for readiness → test directly → shift limited traffic → observe → promote further or roll back**. Production gates from M07-U04 remain relevant; GitHub Actions automation of these steps has not yet been studied here.

### M07-U06 — Monitor the deployed model
Source: https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/5-monitor-model

Pending study.

### M07-U07 — Exercise
Source: https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/5-exercise

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this unit in lesson selection, teaching, checks, and review scheduling; it is excluded from tutor completion and TLDR readiness. No website confirmation is required.

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
