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

Source verified: 2026-11-13. Implementation details appear in later units.

#### Production responsibility continues after deployment

The official scenario is Proseware, a health care technology company whose classification model predicts missed clinic appointments. Staff use no-show risk scores to decide whom to call ahead of time. The machine learning engineer must turn the trained model into a reliable production service through a repeatable, automated process.

The lifecycle is **register/version → deploy/test → promote or roll back → monitor → investigate and, when appropriate, retrain**. Azure ML manages model versions and managed online endpoints; GitHub environments control promotion, and Actions automate deployment and testing.

#### Predictive quality versus operational reliability

Tutor clarification, conceptual and not executed: monitor both prediction quality and service reliability. Historical performance does not prove current quality as patient behavior changes; compare predictions with actual appointment outcomes or labels when available. Also monitor request failures and response time: a reliable service can make poor predictions, and an accurate model can be unavailable. Investigate signals before deciding whether retraining is appropriate.

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

Recurring retraining motivates automation of **registration → deployment → testing**. Tutor clarification: automation can consistently deploy a poor model, so evaluation and testing remain necessary.

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

Registration is the handoff: a registered version is a deployable asset, not a running prediction service. It still needs deployment, testing, and safe promotion.

#### Automate repetitive work while retaining judgment

Proseware uses GitHub Actions to automate registration, deployment, and testing when a new version is ready. Human judgment can remain in promotion and monitoring investigations.

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

Tests check defined requirements; reviewers decide whether to proceed using that evidence and operational context. Tutor example: a candidate from `main` with failed staging tests needs investigation and passing test evidence before promotion. An allowed branch or approval does not replace testing and clear acceptance criteria.

#### Configuration, authentication, and authorization

Environment variables hold non-sensitive target settings such as workspace and endpoint names. Environment secrets are available only to jobs referencing that environment and only after its protection rules pass.

OIDC avoids storing an Azure client secret but does not itself establish staging–production isolation. The source recommends different federated identities for staging and production, with each granted only the Azure permissions its job requires. Tutor clarification: authentication establishes identity; Azure RBAC authorizes resource operations. An already overprivileged staging identity needs narrower RBAC scope, not simply more permissions.

Tutor-created conceptual practice: a staging identity can modify both staging and production endpoints. Separate the identities and restrict staging permissions to its required staging resources; use the appropriately authorized production identity in the approval-protected promotion job. This reinforces the gate with least-privilege access. Practical identity, RBAC, and workflow configuration remain unverified; no implementation example was executed.

### M07-U05 — Deploy, promote, and roll back a model with GitHub Actions
Source: https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/4-model-deployment

Source verified: 2026-11-26. Studied concepts below cover endpoint/deployment separation, direct testing, progressive traffic allocation, rollback, and GitHub Actions automation. CLI/YAML and Python examples are illustrative; no commands, scripts, workflows, or Azure deployments were executed. Complete end-to-end configuration and practical execution remain unverified.

#### Stable endpoint, replaceable deployments

The official source distinguishes a managed online endpoint's stable HTTPS address from its deployments, which host specific model versions and runtime resources. The endpoint can contain multiple deployments, letting the client keep the same URL while the serving model changes beneath it. A deployed candidate is not necessarily promoted to production traffic.

Tutor illustration: `blue` hosts model version 7 at 100% of normal traffic, while `green` hosts version 8 at 0%. Traffic allocations target deployment names, not registered model version numbers directly.

#### Direct tests before user-facing traffic

Wait for green to finish provisioning, then send test requests directly to that deployment and compare responses with expected results. Direct invocation bypasses normal endpoint traffic routing, so green can be tested while blue continues to receive 100% of normal production traffic. Zero allocated traffic does not mean the deployment cannot receive deliberately targeted test requests.

An 80% blue / 20% green split instead sends 20% of normally routed requests to green and returns its predictions to those clients. This is a limited live rollout, not an isolated test.

#### Progressive promotion and acceptance criteria

The source recommends introducing the candidate alongside the existing deployment, testing it first, then shifting traffic gradually and observing production behavior before further promotion. Its illustrative initial split is 90% blue / 10% green; a particular percentage is not a universal safety guarantee.

Tutor practice: test green directly with representative inputs and edge cases before limited live rollout. Live requests may add variety, but that alone does not prove improvement. Check errors and latency, and evaluate prediction quality against acceptance criteria using actual outcomes or labels when available.

#### Roll back traffic, then investigate

Retain the healthy blue deployment through green's observation period. If green produces frequent errors or unacceptable predictions, restore normal traffic to **blue=100%, green=0%**. Traffic reassignment preserves the endpoint URL and avoids deleting and recreating the endpoint for recovery. Investigate green without continuing to expose normal users to it; when blue is healthy, finishing root-cause diagnosis need not precede restoring service.

Tutor example: if green fails at 20% live traffic while blue is healthy, restore blue to 100% and inspect green. Retire blue only after green meets acceptance criteria for the required observation period. This allocation is a worked solution; implementation and execution remain pending.

Sequence: **deploy green → wait → test directly → shift limited traffic → observe → promote or roll back**. Apply the M07-U04 production gates.

#### Automate the pipeline with GitHub Actions

The official unit uses Azure Machine Learning CLI v2 in GitHub Actions to register a model from `model.yml`, create green from `green-deployment.yml`, invoke green with `sample-request.json`, and update traffic to `blue=90 green=10`. It uses `actions/checkout@v4` and `azure/login@v2`; these are the versions shown in the verified source, not a claim that they are the latest available releases. The sample assumes the endpoint and blue already exist and supporting configuration files are available.

The safe release order is **authenticate → register → deploy → wait for readiness → validate direct responses → approval-gated traffic change → observe → promote or roll back**. OIDC requests short-lived federated access rather than using a stored Azure client secret. The workflow declares `id-token: write` and `contents: read`, and `azure/login` uses the configured client, tenant, and subscription identifiers. Azure RBAC separately determines which resource operations the identity can perform.

The source's “Test the new deployment” step invokes green but does not supply a response-validation script. Its text requires comparison with expected responses. Tutor clarification: invocation success only establishes that a response arrived; a meaningful test must evaluate that response and fail when acceptance criteria are violated. The worked Python example below is tutor-created, not an omitted Microsoft sample.

#### Make tests and approval control promotion

As described in [M07-U04](#m07-u04--control-deployments-with-github-environments), deploy/test in one job and change production traffic in a later job referencing the protected `production` environment. Configure a required-reviewer rule when approval is required; the environment name alone creates neither an approval requirement nor Azure resources. OIDC authenticates, RBAC authorizes resource operations, and GitHub protection rules enforce approval.

Tutor control-flow illustration: `needs: deploy_and_test` makes the promotion job depend on successful deployment/testing. Normal later steps are skipped after failure; avoid overrides such as `continue-on-error` or unconditional execution on a safety-critical promotion path. Each job must establish its own Azure authentication; a CLI login does not automatically carry between jobs. Configure federation to match the identity of the job, including its environment when applicable.

Supporting syntax reference: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax (fetched 2026-11-26; large response truncated). This is supplementary implementation guidance, not additional completion evidence.

<a id="python-examples"></a>
#### M07-U05 — Validate a fixed deployment-test response

Tutor-created illustration; not supplied by Microsoft Learn and not executed. Prerequisites: Python 3.10+ with the standard library, a saved `response.json`, and a reviewed expected result for a fixed input. Assume the model-specific response contract is `{"predictions": [0.82]}`. Azure ML does not impose this example response shape on every model.

```python
# validate_response.py
import json
import sys

with open("response.json", encoding="utf-8") as file:
    response = json.load(file)

expected = 0.82
tolerance = 0.01

predictions = response.get("predictions")
if not isinstance(predictions, list) or len(predictions) != 1:
    sys.exit("FAIL: expected exactly one prediction")

actual = predictions[0]
if type(actual) not in (int, float):
    sys.exit("FAIL: prediction must be numeric")

if not abs(actual - expected) <= tolerance:
    sys.exit(f"FAIL: expected approximately {expected}, got {actual}")

print("PASS: response matches the expected test result")
```

Expected outcome: a matching numeric prediction prints PASS and exits successfully. A contract or tolerance violation exits unsuccessfully; a missing file or invalid JSON also fails. The sample assumes a JSON object; a different top-level shape would fail and needs contract-specific handling. This is a fixed-input regression check, not evidence of population-level predictive accuracy. Evaluate representative datasets with suitable metrics separately, and review expected outputs when intentionally changing model versions.

Other relevant Python model registration/deployment examples remain pending study.

<a id="javascript-examples"></a>

<a id="azure-cli-commands"></a>
#### M07-U05 — Direct invocation and traffic controls

Illustrative, not executed. Prerequisites: authenticated Azure CLI with the `ml` extension v2, an AML workspace and appropriate RBAC, an existing managed online endpoint, ready deployments, and a model-compatible `sample-request.json`. Set `ENDPOINT_NAME`, `RESOURCE_GROUP`, and `WORKSPACE_NAME` to the intended target. The source installs the extension with `az extension add -n ml -y`; no installed CLI/extension version was measured here.

```bash
# Test green directly, independently of normal traffic routing.
az ml online-endpoint invoke \
  --name "$ENDPOINT_NAME" \
  --deployment-name green \
  --request-file sample-request.json \
  --resource-group "$RESOURCE_GROUP" \
  --workspace-name "$WORKSPACE_NAME" \
  > response.json

# Only after readiness, validation, and required approval:
az ml online-endpoint update \
  --name "$ENDPOINT_NAME" \
  --traffic "blue=90 green=10" \
  --resource-group "$RESOURCE_GROUP" \
  --workspace-name "$WORKSPACE_NAME"

# Recovery when blue remains healthy:
az ml online-endpoint update \
  --name "$ENDPOINT_NAME" \
  --traffic "blue=100 green=0" \
  --resource-group "$RESOURCE_GROUP" \
  --workspace-name "$WORKSPACE_NAME"
```

These are separate operational actions, not a script to run consecutively. Expected outcomes: direct invocation saves green's response; the first update allocates limited live traffic; rollback restores normally routed traffic to blue without changing the endpoint URL. Saving output to a file is a tutor addition for validation. Endpoint/model/deployment construction files and an implemented readiness check remain pending examples.

<a id="related-configuration-yaml-bicep-or-github-actions"></a>
#### M07-U05 — Connect direct invocation to validation

Tutor-created step fragment, not a complete workflow; not executed. Requires checked-out request and validation files, Python 3.10+, authenticated CLI with the `ml` extension v2, target variables, and ready green. The prediction contract must match the Python example above.

```yaml
- name: Test green and validate its response
  run: |
    az ml online-endpoint invoke \
      --name "$ENDPOINT_NAME" \
      --deployment-name green \
      --request-file sample-request.json \
      --resource-group "$RESOURCE_GROUP" \
      --workspace-name "$WORKSPACE_NAME" \
      > response.json
    python validate_response.py
```

Expected outcome: invocation and validation must both succeed before a normal later traffic-change step runs.

#### M07-U05 — Separate testing from protected promotion

Tutor-created control-flow sketch; deliberately incomplete and not executed. The echo placeholders do not deploy, test, authenticate, or change traffic and must not be treated as a functional release workflow.

```yaml
jobs:
  deploy_and_test:
    runs-on: ubuntu-latest
    steps:
      # Authenticate, deploy green, wait, invoke, and validate.
      - run: echo "Deployment and test implementation goes here"

  promote:
    needs: deploy_and_test
    environment: production
    runs-on: ubuntu-latest
    steps:
      # Authenticate with production identity, then change traffic.
      - run: echo "Traffic-change implementation goes here"
```

Expected control flow after real implementations replace placeholders: failed tests block promotion; passing tests still require configured environment approval. Protection-rule availability depends on repository visibility and GitHub plan; verify prerequisites before implementation. Full workflow triggers, per-job login, versioned model/deployment YAML, readiness implementation, and sample files remain pending examples.

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

<a id="key-concepts-and-decision-points"></a>
<a id="worked-examples-and-practice"></a>
<a id="common-pitfalls-and-clarifications"></a>

## Remaining study and examples

- M07-U06 remains pending study. Further key concepts, worked practice, and pitfalls remain pending.
- JavaScript examples remain pending; relevance is not yet assessed. Other Python registration/deployment examples, endpoint/model/deployment construction files, readiness checks, and complete workflow and sample files remain pending as described above.

Optional quiz participation and results: [Quiz history](quizzes.md).

## Microsoft Learn search terms
- Azure Machine Learning MLflow model register archive
- managed online endpoint traffic rollout rollback GitHub Actions
- Azure Machine Learning model monitoring data drift retraining
