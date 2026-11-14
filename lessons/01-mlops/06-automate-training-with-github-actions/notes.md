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

Source verified: 2026-11-13.

#### Keep the shared branch healthy

Microsoft Learn describes trunk-based development as frequent integration into one shared branch, typically `main`. Contributors use short-lived feature branches, open pull requests, and integrate reviewed changes while keeping `main` a reliable starting point. Trunk-based development does not require unrestricted direct pushes to `main`.

Short-lived branches reduce divergence from `main`, keeping merge conflicts smaller and exposing integration problems sooner. Small commits and regularly updating a feature branch from `main` help, but do not replace frequently merging small, reviewed increments back into the shared branch. The stale-code and conflict risks are useful practical reasons for limiting branch lifetime.

#### Workflow checks versus merge enforcement

The official source distinguishes GitHub Actions from repository branch protection rules or rulesets:

- A workflow defines and runs automated validation, producing status checks.
- A rule on `main` can restrict direct pushes, require pull requests and reviewer approvals, and require specific checks to pass before merging.

A validation workflow alone does not guarantee that a failed check blocks a merge. Configure the repository rule to require the relevant checks. These concepts connect to D1 Git source control and automation; implementing training validation is the next unit's topic.

#### Worked applications

Tutor-created conceptual examples; no repository settings were changed, commands executed, or workflows run. No SDK/CLI version applies to the conceptual work; repository rules and Actions access are prerequisites for practical implementation.

1. **Failed validation but merge remains available:** investigate the rule targeting `main` and make the relevant validation status checks required before merging. Add pull-request and approval requirements as appropriate for the team's policy.
2. **A feature takes several weeks:** split the work into small, tested, reviewed increments—for example, a helper function and its tests before enabling the new feature in training. Keep `main` healthy and leave the unfinished feature unused until ready. Frequent integration reduces branch drift and reveals incompatibilities earlier than one large final merge. This is a tutor illustration of the source's small-change principle, not an implemented pipeline.

### M06-U04 — Validate changes with GitHub Actions
Source: https://learn.microsoft.com/en-us/training/modules/trigger-azure-machine-learn-jobs-github-actions/4-use-for-model-training

Source verified: 2026-11-13.

#### Workflows, triggers, jobs, runners, and steps

Microsoft Learn defines a GitHub Actions workflow as a YAML file stored under `.github/workflows/`. It specifies what runs and when. The `on:` key defines the trigger; `pull_request` normally starts validation when a pull request opens, reopens, or receives new commits.

A workflow contains jobs. Each job runs on a runner, either a GitHub-hosted virtual machine or a self-hosted machine. A job contains ordered steps, such as checking out the repository, installing dependencies/tools, and running validation commands.

For training code, the source suggests linting with Flake8 and behavioral unit tests with Pytest. Linting detects style issues and certain code errors; unit tests verify expected function behavior. Valid syntax and formatting do not establish correct preprocessing.

#### Turn automated checks into a blocking quality gate

The workflow reports status checks on the pull request. Configure branch protection on `main` to require the relevant validation checks to pass before merging. Running a check and enforcing its outcome are separate responsibilities. Microsoft Learn identifies the check by the job name; use clear, stable names so protection rules target the intended checks.

Illustrative sequence: **pull request event → workflow starts → runner checks out code → steps install dependencies, lint, and test → job reports status → branch protection requires success before merge**. This connects D1 source-control automation with D2 reliable training workflows. Passing code validation alone does not establish acceptable model quality.

#### Worked behavioral-test and enforcement examples

Tutor-created conceptual practice; no code, workflow, or repository configuration was executed. No SDK/CLI version requirement applies to this conceptual sequence. An implementation would require a GitHub repository with Actions enabled, a suitable runner, test dependencies, and permission to configure repository protection. Runnable YAML and dependency versions remain pending for practical study.

1. **Incorrect missing-value replacement:** preprocessing replaces missing ages with zero instead of the intended median. Use a unit test to verify output, rather than relying on linting. A tutor-supplied worked test case uses known ages `20` and `40` plus a missing value and expects `20`, `40`, `30`. This checks the replacement rule under the assumption that the median is calculated from the nonmissing values.
2. **Tests fail but merging remains possible:** configure branch protection to require the validation job's successful status check before merging. A workflow that merely reports failure does not itself enforce the merge restriction.

### M06-U05 — Connect GitHub Actions to Azure Machine Learning securely
Source: https://learn.microsoft.com/en-us/training/modules/trigger-azure-machine-learn-jobs-github-actions/5-connect-github-actions-azure

Source verified: 2026-11-13.

#### Secrets, variables, and least privilege

Microsoft Learn distinguishes encrypted GitHub secrets for sensitive credentials from GitHub variables for non-sensitive configuration, such as workspace and resource-group names. Recognized secret values are masked in logs, but workflows must still avoid exposing them. A workspace name identifies a destination; it does not grant access. Storing it as a secret is not inherently unsafe, but secret protection is unnecessary for ordinary non-sensitive configuration.

A service principal is a non-human identity in Microsoft Entra ID. Assign an appropriate Azure role at the narrowest scope needed for the workflow, such as its target Azure ML workspace. Workspace scope is appropriate only when it covers the required operations; do not assume that every workflow can operate solely at that scope.

#### OIDC authentication does not grant authorization

Microsoft Learn recommends workload identity federation with OpenID Connect (OIDC) over stored service-principal client secrets for new workflows. Configure trust between the GitHub workflow context and a Microsoft Entra application. GitHub issues a short-lived OIDC token during a run; Azure validates it against the configured trust and returns an Azure access token. This avoids storing and rotating a long-lived client secret.

Authentication establishes identity; authorization determines what that identity may do at a resource scope. OIDC changes the authentication mechanism, not the identity's role assignments. Successful sign-in can therefore be followed by a denied job submission when the identity lacks an appropriate Azure role.

Tutor analogy: authentication supplies an identity badge; authorization determines which doors it opens. Short token lifetime reduces credential exposure but does not confer permissions.

#### Git tracking is separate from access

When submitting source files from a local Git repository, Azure ML can record repository, branch, and commit information with the job. This works with compatible Git services and does not attach a particular GitHub repository to the workspace as an authentication mechanism. Tracking answers which source version produced a job; authentication and authorization control access to submit it.

#### Worked conceptual applications

Tutor-created examples; no code, workflow, or Azure operations were run. No SDK/CLI version applies to these conceptual examples. Practical implementation requires a GitHub repository/workflow, a configured Entra identity and federation trust or credential, and suitable Azure role assignments. Runnable configuration and tool-version verification remain pending.

1. **Submit jobs to one workspace:** put its non-sensitive name in a GitHub variable and a client secret, if using one, in a GitHub secret. Assign an appropriate role at workspace scope when sufficient for the workflow's operations.
2. **OIDC sign-in succeeds but job submission is denied:** first inspect the identity's Azure role assignment and scope. Replacing OIDC with a client secret does not repair missing authorization.
3. **A job records a commit:** use that identifier for source traceability, not as evidence that a workflow has Azure access.

### M06-U06 — Trigger Azure Machine Learning jobs and pipelines
Source: https://learn.microsoft.com/en-us/training/modules/trigger-azure-machine-learn-jobs-github-actions/6-trigger-azure-machine-learning-jobs

Source verified: 2026-11-13. Supplementary GitHub documentation verified on the same date: [repository dispatch API](https://docs.github.com/en/rest/repos/repos#create-a-repository-dispatch-event), [repository dispatch trigger](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows#repository_dispatch), and [workflow dispatch inputs](https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax#onworkflow_dispatchinputs).

#### Choose the event that starts the workflow

Microsoft Learn distinguishes these GitHub Actions triggers:

| Trigger | Typical purpose |
| --- | --- |
| `pull_request` | Validate a proposed code change before merging |
| `push` targeting `main` | Train after an approved change lands on the shared branch |
| `workflow_dispatch` | Start a workflow on demand, including from the GitHub UI |
| `schedule` | Retrain periodically against updated data |
| `repository_dispatch` | Accept an external API-generated repository event |

A trigger starts a GitHub Actions workflow; a workflow step then submits an Azure ML job. GitHub orchestrates the automation, while Azure ML executes the training workload. This connects D1 automation with D2 automated training.

#### Bridge Azure-side events to GitHub

The official source explains that Actions does not natively subscribe to Azure Event Grid. An intermediary such as an Azure Function or Logic App receives the Azure event, authenticates to GitHub, and calls its REST API with a `repository_dispatch` payload. Tutor illustration, not deployed:

```text
New data in Azure Storage → Event Grid → Function or Logic App
    → GitHub repository_dispatch → Actions workflow → Azure ML job
```

A storage event is not pull-request activity. The GitHub credential used by the intermediary is separate from the Azure identity the workflow later uses for training submission. Code changes and data changes can reuse the same submission logic with different triggers.

#### Dispatch examples: receiver and sender

Tutor-created examples grounded in supplementary GitHub documentation; not executed. They only print values and do not submit Azure jobs. Prerequisites: GitHub repository with Actions enabled, workflow on its default branch, an available Ubuntu runner, and `curl` for the sender. The sender also needs a securely supplied GitHub token authorized for repository dispatch; GitHub documents `repo` scope for classic PATs. Prefer narrowly scoped GitHub App/fine-grained credentials where possible and verify their endpoint permissions. API version used: `2026-03-10`; no Azure CLI/SDK dependency is involved in this demo.

Receiver, illustrative `.github/workflows/data-arrived.yml`:

```yaml
name: Handle new training data
on:
  repository_dispatch:
    types: [new_training_data]
permissions: {}
jobs:
  inspect-event:
    runs-on: ubuntu-latest
    steps:
      - name: Read the event payload
        env:
          DATASET_VERSION: ${{ github.event.client_payload.dataset_version }}
          EVENT_ID: ${{ github.event.client_payload.event_id }}
        run: |
          printf 'Dataset version: %s\n' "$DATASET_VERSION"
          printf 'Source event ID: %s\n' "$EVENT_ID"
```

`types` filters the sender's custom `event_type`; `github.event.client_payload` exposes the additional JSON data. Environment variables and quoted shell expansion keep payload values out of shell source. This print-only workflow needs no runner-side GitHub API permissions. Treat payloads as untrusted data: validate them and never execute payload-supplied commands.

Sender, illustrative shell request; replace owner/repository placeholders and supply `GH_DISPATCH_TOKEN` securely, never as a literal credential in source:

```bash
export GH_OWNER="YOUR-OWNER"
export GH_REPO="YOUR-REPOSITORY"
curl --fail --silent --show-error \
  --request POST \
  --url "https://api.github.com/repos/${GH_OWNER}/${GH_REPO}/dispatches" \
  --header "Accept: application/vnd.github+json" \
  --header "Authorization: Bearer ${GH_DISPATCH_TOKEN}" \
  --header "X-GitHub-Api-Version: 2026-03-10" \
  --header "Content-Type: application/json" \
  --data '{
    "event_type": "new_training_data",
    "client_payload": {
      "dataset_version": "42",
      "event_id": "storage-event-123"
    }
  }' \
  --write-out '\nHTTP %{http_code}\n'
```

Expected result: HTTP 204 with no response body, followed by a matching enabled workflow run printing version `42` and the event ID. HTTP 204 confirms dispatch success, not workflow or training success. The workflow must exist on the default branch; repository dispatch uses that branch's context. A payload field named `branch` does not automatically change it. Keep secrets out of payloads; production event handling also needs validation and duplicate-event handling to avoid unintended repeated training.

#### Explicit on-demand workflow inputs

`workflow_dispatch` targets an on-demand workflow with declared inputs; it also supports API/CLI invocation, not just the UI. It must be present on the default branch to receive dispatch events. Tutor-created illustrative `.github/workflows/manual-training.yml`; not executed, same Actions/runner prerequisites, no Azure dependency:

```yaml
name: Manual training request
on:
  workflow_dispatch:
    inputs:
      dataset_version:
        description: Dataset version to train on
        required: true
        type: string
permissions: {}
jobs:
  inspect-request:
    runs-on: ubuntu-latest
    steps:
      - name: Show the requested dataset
        env:
          DATASET_VERSION: ${{ inputs.dataset_version }}
        run: |
          printf 'Requested dataset version: %s\n' "$DATASET_VERSION"
```

Expected result: an on-demand run prints the supplied version. `inputs` declares the parameters; `${{ inputs.dataset_version }}` reads the value. Actual Azure authentication, job YAML, CLI submission and waiting implementation remain pending practical work.

#### Command jobs, pipeline jobs, and outcome checks

Microsoft Learn describes a command job as a single script on Azure compute, suitable for a one-step training workload. A pipeline job connects reusable components, such as preparation, training, and evaluation, into a directed graph. Components can be registered as versioned assets. A chain is one possible graph; pipelines can also branch.

The workflow submits a checked-in job YAML definition using the Azure CLI. A step can wait for the Azure ML job to finish and check its exit status. A checked job failure can fail the workflow; required branch-protection checks can then block merging. Acceptance of submission alone is not completion evidence.

Keep three outcomes distinct:

1. **Submission accepted:** Azure ML accepted the request.
2. **Execution succeeded:** the job and its components completed without execution errors.
3. **Quality accepted:** evaluation metrics meet defined requirements (tutor clarification connecting to earlier model-quality validation).

An evaluation script can execute successfully while reporting a poor model. Successful pipeline execution does not automatically enforce a model-quality gate; the workflow or evaluation logic must deliberately check acceptance criteria.

#### Worked conceptual application

Tutor-created exercise, not executed: separate reusable preparation, training, and evaluation components must run together. Which job type fits, and why is successful submission insufficient?

Worked solution: submit a pipeline job to connect the components. Wait for job completion and check execution status, then check the evaluation against quality requirements. Submission, execution, and quality acceptance answer different questions. No lab-equivalent deployment or training execution is established by this conceptual exercise.

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
