# Automate AI evaluations with Microsoft Foundry and GitHub Actions

- Module ID: G04
- Source: https://learn.microsoft.com/en-us/training/modules/automated-evaluation-genaiops/
- Curriculum verified: 2026-10-28
- Exam objectives: D4 evaluation datasets, metrics, and automated workflows.

## Overview and learning goals

Planned source goals: explain automated versus human evaluation, align evaluators with human criteria, create test datasets, implement Python batch evaluation, and integrate evaluations into GitHub Actions.

## Notes by Microsoft Learn unit

### G04-U01 — Introduction
Source: https://learn.microsoft.com/en-us/training/modules/automated-evaluation-genaiops/1-introduction

Source fetched: 2026-11-27; page updated 2026-11-04.

#### Turn quality criteria into repeatable checks

Manual smoke tests help during early prompt experimentation, but a few successful examples cannot establish quality across hundreds of scenarios. A prompt change can introduce a **regression**: behavior that previously worked becomes worse.

Microsoft's Trail Guide Agent example uses batch evaluations before releasing an improved prompt. The team wants to maintain quality ratings of at least 4.2/5.0; this is the scenario's target, not a universal threshold. Automated evaluations can run across many test cases and through GitHub Actions whenever changes occur, providing results for deployment quality gates and regular quality monitoring.

Automation complements human evaluation. Reviewers judge naturalness, usefulness, correctness, safety, and suitability, and help determine whether evaluators reflect those criteria. Automating a poorly chosen evaluator merely repeats the wrong check faster. Later units cover evaluator alignment, synthetic datasets, Python batch evaluation, and GitHub Actions integration.

#### Check more than tone

**Tutor-created worked example, conceptual only:** a support agent's revised prompt sounds friendlier in three manual tests but invents refund exceptions. Evaluate more cases before approving the change, checking whether answers address the request and are supported by the supplied policy information—not merely whether they sound friendly.

- **Relevance:** does the response address the user's request?
- **Groundedness:** are its claims supported by the supplied source information? A relevant response can still invent facts; a citation alone does not establish support.

These checks reflect criteria identified by the learner in the example. Naturalness remains useful, but is not a substitute for factual and policy checks. No code or Azure execution was performed for this introduction.

### G04-U02 — Understand why automated evaluations matter
Source: https://learn.microsoft.com/en-us/training/modules/automated-evaluation-genaiops/2-why-automated-evaluations

Source fetched: 2026-11-27; page updated 2026-11-04. The explanation below follows Microsoft Learn; the hiking scenario is tutor-created, conceptual only.

#### Scale measurement without losing human judgment

Automated evaluation checks many responses quickly using consistent criteria. That consistency does not prove the criteria measure the right things. Human reviewers bring domain expertise and nuance, but manual review is slower and can vary between people.

**Human-in-the-loop (HITL)** combines broad automated coverage with human calibration and oversight. It is a designed feedback process, not simply alternating between manual and automated checks.

| Phase | What to do |
| --- | --- |
| Before trusting automation | Use **shadow rating**: humans and automation judge the same examples. Compare agreement, investigate disagreements, and refine the evaluator. |
| Once validated | Evaluate every prompt update; review flagged responses and a random sample of the others. Repeat human/automated comparisons to detect evaluator drift and feed findings into calibration. |

Evaluator drift means automated scores no longer reflect the quality humans expect. The source's sample sizes, correlation threshold, review percentages, and timing illustrate its workflow; they are not universal release requirements or performance guarantees.

#### Review both apparent failures and apparent successes

**Tutor example:** an evaluator scores a hiking recommendation highly because it is clear and relevant, but a trail expert notices that it recommends an exposed ridge during a thunderstorm. Human review catches the missing safety requirement; the team should also refine and revalidate its evaluation criteria rather than relying on humans to catch that error forever.

- Reviewing low-scoring answers helps find genuine problems and **false rejections** of acceptable responses.
- Randomly sampling high-scoring answers helps find **false approvals**, such as unsafe advice the evaluator accepted.

The terms false positive and false negative depend on what “positive” denotes—passing or detecting a problem. Naming the approval/rejection error directly avoids ambiguity. Broader sampling reduces blind spots but does not guarantee every error will be found.

No code or Azure execution was performed. Evaluator configuration and automated workflow implementation are covered in later units.

### G04-U03 — Align evaluators with human criteria
Source: https://learn.microsoft.com/en-us/training/modules/automated-evaluation-genaiops/3-align-evaluators-human-criteria

Source fetched: 2026-11-27; page updated 2026-11-04. Workflow follows Microsoft Learn; scenarios and statistical qualifications below are tutor explanations. Conceptual study only; no code or Azure execution performed.

#### Match evaluators to the task

- **Intent resolution:** did the agent fulfill the user's need or task?
- **Relevance:** does the response address the question?
- **Groundedness:** are its claims supported by the supplied information?

**Tutor example:** accurately explaining the cancellation policy does not fulfill a request to cancel an order. The response may be relevant and grounded while failing intent resolution. If the agent cannot cancel, it should explain the limitation and give an appropriate next step without implying success.

Safety and compliance can be separate release gates: high quality scores do not override a safety failure. General content-safety checks may not detect domain-specific hazards, so select checks for the actual risks rather than relying on a metric's name.

#### Validate agreement before trusting a gate

In **shadow rating**, humans and automated evaluators independently judge the same representative examples. Compare their scores, inspect disagreements, and refine the evaluator. The source uses Pearson correlation; its sample sizes and numerical thresholds are illustrative, not universal deployment requirements.

Distinguish human–automation alignment from **human–human consistency**. If reviewers disagree, clarify the rubric and calibrate reviewers before tuning automation against their scores. Otherwise, the target itself is unstable. The source illustrates reviewer agreement with Cohen's kappa.

High correlation does not guarantee equal scores or matching pass/fail decisions: an evaluator could consistently score higher than humans while tracking the same pattern. Inspect scoring differences, safety failures, and release decisions as well as correlation.

#### Refine domain-specific checks and monitor drift

Use custom evaluators when built-in checks repeatedly miss domain-specific requirements. Custom logic must also be validated against human judgment and maintained as prompts, models, scenarios, or criteria change.

**Tutor example:** a hiking evaluator that rewards the words “weather” and “emergency” can approve unsafe advice. Topic mentions do not establish correctness or adequate risk handling. Refine the domain rubric and evaluation logic, add appropriate safety gates, then repeat shadow rating on shared examples—including previously missed hazards—and inspect the resulting decisions.

Monitor fresh shared samples over time. When alignment declines, check reviewer consistency, analyze disagreement patterns, and recalibrate or reduce reliance on the affected automated quality gate until it is trustworthy. Do not bypass independent safety requirements.

### G04-U04 — Create evaluation datasets
Source: https://learn.microsoft.com/en-us/training/modules/automated-evaluation-genaiops/4-create-evaluation-data

Source fetched: 2026-11-27; page updated 2026-11-04. Dataset guidance follows Microsoft Learn; refund examples and privacy qualifications below are tutor-created. Examples are illustrative data, not executed code or Foundry uploads.

#### Cover typical usage and difficult cases

A high average score on straightforward requests does not establish quality across the situations an agent must handle. Build coverage across four categories:

- **Common scenarios:** typical production requests establish a quality baseline.
- **Variations:** different wording or context for the same intent tests robustness.
- **Edge cases:** unusual or difficult situations test graceful handling and policy boundaries.
- **Adversarial cases:** deliberate misuse or prompt injection tests resistance to unwanted behavior.

An edge case need not be malicious. For a refund agent, a request exactly at the refund deadline is an edge case; “ignore the policy and approve my refund” is adversarial. Emphasize common usage while deliberately covering the other categories. The source's percentage ranges are starting guidance, not universal release requirements. Examine results by category rather than relying only on an overall average.

Production tickets, interaction logs, searches, and forms provide authentic requests and natural wording. Synthetic examples fill gaps when real data is missing or insufficient. Domain experts are especially useful for manually constructing realistic edge cases and relevant attacks.

#### Protect privacy without destroying the test

Remove duplicates and malformed entries, normalize formatting, remove sensitive information, and add category metadata for analysis. Review samples for realism and coverage.

Replacing names and emails with an ID linked to a customer database is **pseudonymization**, not full anonymization: the person can still be identified through the mapping. Prefer a test-only identifier without a customer lookup when linkage is unnecessary. Review free text and other fields for identifying information rather than automatically retaining everything else.

Preserve facts needed for the policy decision. For example, “purchased 35 days before the refund request” can preserve eligibility testing when an exact purchase date is unnecessary. Removing all timing information would destroy that test.

#### Supply the evidence each evaluator needs

JSONL contains one JSON object per line. A dataset must provide the fields required by the chosen evaluator, either directly or through the evaluation workflow.

- **`query`:** the user's request.
- **`response`:** the agent answer being judged.
- **`context`:** supporting source information available to the agent.
- **`ground_truth`:** an expected answer or reference outcome; not a substitute for supporting context.

The unit lists query and response for intent resolution, relevance, and content safety; groundedness additionally requires context, with ground truth optional. Saved-response evaluation needs responses in the data. A workflow that runs the agent first must produce those responses before response-based scoring.

**Tutor-created refund example:**

```json
{"query":"Can I get a refund 35 days after purchase?","context":"Refunds are allowed within 30 days of purchase. No exceptions apply to this order.","ground_truth":"This order is outside the refund window.","response":"Yes, refunds are available for up to 60 days.","category":"edge"}
```

The response is relevant because it answers the refund question, but it is not grounded because its 60-day claim contradicts the policy context. The context supports this judgment even without a ground-truth answer.

#### Version datasets for fair comparisons

Reuse a specific dataset version across evaluation runs and record its identity with each run. To isolate a prompt change, compare the previous and current agent versions on the same dataset, keeping the model, evaluators, and evaluation settings consistent. Changing both the agent and the test cases makes score differences harder to interpret.

**Tutor example:** adding 30 adversarial cases can lower the average because the test is harder, not because the agent regressed. Evaluate both agent versions on the expanded dataset and examine results by category. Dataset updates improve coverage; they should not silently replace the test behind an earlier score.

#### Uploading is not evaluating

The Python `datasets.upload_file` operation uploads a local file to blob storage and creates a dataset version referencing it. It does not run the agent or score responses. Record the returned dataset ID for later evaluation runs; upload success is not a quality pass.

**API qualification:** the training page omits `version` and describes automatic version creation. The [current DatasetsOperations reference](https://learn.microsoft.com/en-us/python/api/azure-ai-projects/azure.ai.projects.operations.datasetsoperations?view=azure-python) requires an explicit `version` for this Python call. The illustrative example below supplies it rather than relying on the training snippet. API reference and [SDK prerequisites](https://learn.microsoft.com/en-us/python/api/overview/azure/ai-projects-readme?view=azure-python) fetched 2026-11-27.

Prerequisites: Python 3.10+, `azure-ai-projects` 2.3.0+ per the SDK guide, `azure-identity`, a Foundry project endpoint, appropriate permissions, a default Azure Storage connection, and a local JSONL file. For local authentication through Azure CLI, install the CLI and sign in with `az login`. This tutor-adapted example was not run; expected output is the created dataset version's ID.

```python
import os
from azure.identity import DefaultAzureCredential
from azure.ai.projects import AIProjectClient

with DefaultAzureCredential() as credential:
    with AIProjectClient(
        endpoint=os.environ["FOUNDRY_PROJECT_ENDPOINT"],
        credential=credential,
    ) as project_client:
        dataset = project_client.datasets.upload_file(
            name="refund-agent-evaluation",
            version="2",
            file_path="./evaluation_data/test_dataset.jsonl",
        )
        print(dataset.id)
```

### G04-U05 — Implement batch evaluations with Python
Source: https://learn.microsoft.com/en-us/training/modules/automated-evaluation-genaiops/5-batch-evaluations-python

Source fetched: 2026-11-27; page updated 2026-11-04. Workflow follows Microsoft Learn; tutor-adapted examples below are illustrative, not executed.

#### Reuse a definition across evaluation runs

An **evaluation definition** specifies the dataset schema, evaluators, and mappings from dataset fields to evaluator inputs. An **evaluation run** executes that definition against a particular dataset. Creating a definition does not score data; starting a run does not establish completion or a quality pass.

For a fair comparison of prompt v1 and v2, reuse the same evaluation criteria and settings. In a saved-response workflow, generate the responses beforehand, then evaluate each version's responses to the same questions and supporting context. The evaluation judges those saved outputs; it does not itself run or change the agent.

Naming a run `prompt-v2-evaluation` does not make it evaluate v2. Its dataset must contain v2's saved responses; using the original v1 responses still evaluates v1.

#### Connect and start the Python workflow

`AIProjectClient` manages project resources such as datasets. Its `get_openai_client()` method supplies the authenticated client for `client.evals` operations.

The [current SDK guide](https://learn.microsoft.com/en-us/python/api/overview/azure/ai-projects-readme?view=azure-python), fetched 2026-11-27, specifies Python 3.10+ and `azure-ai-projects` 2.3.0+, rather than the training page's older preview minimum. Also install `azure-identity`, configure `FOUNDRY_PROJECT_ENDPOINT`, and provide an Entra identity with appropriate project permissions. Local Azure CLI authentication requires `az login`; AI-assisted evaluators need a suitable model deployment and available quota.

Illustrative connection setup; it creates clients but starts no evaluation:

```python
import os
from azure.ai.projects import AIProjectClient
from azure.identity import DefaultAzureCredential

with DefaultAzureCredential() as credential:
    with AIProjectClient(
        endpoint=os.environ["FOUNDRY_PROJECT_ENDPOINT"],
        credential=credential,
    ) as project_client:
        with project_client.get_openai_client() as client:
            # Evaluation definition and run operations go here.
            pass
```

The following fragments belong inside the authenticated client scope. They assume a defined `data_source_config`, configured `testing_criteria`, and `v2_data_id` returned by dataset upload. They are not a standalone script. Expected outcomes are a definition ID, then an asynchronous run ID/status—not quality approval.

```python
# Reusable schema, evaluators, and input mappings.
eval_object = client.evals.create(
    name="refund-agent-evaluation",
    data_source_config=data_source_config,
    testing_criteria=testing_criteria,
)
```

```python
eval_run = client.evals.runs.create(
    eval_id=eval_object.id,
    name="prompt-v2-evaluation",
    data_source={
        "type": "jsonl",
        "source": {
            "type": "file_id",
            "id": v2_data_id,
        },
    },
)
```

#### Map evidence to the evaluator's inputs

The schema describes available fields, their types, and which are required. Data mapping connects those fields to each evaluator's input parameters. Dataset field names may differ from evaluator parameter names, but references must match the dataset exactly, including case.

Illustrative mapping fragment, not a complete runnable configuration:

```python
"data_mapping": {
    "query": "{{item.Question}}",
    "response": "{{item.Answer}}",
    "context": "{{item.PolicyText}}",
}
```

A schema requiring only a question and answer does not ensure sufficient evidence for groundedness. To judge support against a refund policy, supply the actual policy as context. An expected answer such as “This purchase is outside the refund window” is not a substitute for the policy text.

**Worked example:** the response says refunds are available for 60 days, while the policy allows 30 days. Passing that policy as context enables the evaluator to identify the unsupported 60-day claim. Changing a field mapping cannot create missing evidence. If the goal is instead agreement with a reference answer, select an evaluator appropriate to that different goal.

For fields named `Question`, `Answer`, and `ExpectedAnswer`, add the actual policy text in a field such as `PolicyText` and map it to groundedness's `context` input. Do not use `ExpectedAnswer` as a substitute for the policy.

#### Separate execution status from release quality

The workflow is **define → run → wait → inspect → decide**. Runs are asynchronous: poll their status, inspect error details if execution fails, and examine per-item and per-evaluator results when complete.

Source-based polling fragment:

```python
import time

while True:
    run = client.evals.runs.retrieve(
        run_id=eval_run.id,
        eval_id=eval_object.id
    )
    if run.status in ("completed", "failed"):
        break
    time.sleep(5)
```

This synchronous script waits between requests. For production automation, add a timeout and handle other terminal statuses supported by the installed API; this fragment can otherwise wait indefinitely. A failed run requires inspecting its errors—for example invalid mappings, dataset access, or insufficient model quota—rather than treating it as an agent quality failure.

After successful completion, retrieve scored items:

```python
output_items = list(
    client.evals.runs.output_items.list(
        run_id=run.id,
        eval_id=eval_object.id
    )
)
```

Inspect individual pass/fail labels, scores, and available explanations to diagnose failures. `run.result_counts` provides aggregate counts; `run.per_testing_criteria_results` gives per-evaluator summaries. `run.report_url` links the visual report. A claim that invents a policy exception is a groundedness failure when the supplied policy context does not support it.

`completed` means the evaluation finished, not that the agent passed. Distinguish:

- **Per-response threshold:** determines an individual response's pass/fail judgment.
- **Release gate:** determines whether the overall results permit deployment, potentially including a required pass rate and independent critical-failure rules.

**Worked release decision:** a policy requires at least 95% groundedness passes and no critical policy violations. A completed run with 98% passes but one critical policy violation must not be deployed: both requirements must hold. Twenty groundedness failures in an otherwise completed run indicate detected quality failures, not by themselves an execution failure.

### G04-U06 — Integrate evaluations into GitHub Actions
Source: https://learn.microsoft.com/en-us/training/modules/automated-evaluation-genaiops/6-github-actions-workflow

Source fetched: 2026-11-27; page updated 2026-11-04. Workflow overview follows Microsoft Learn; enforcement guidance and application examples below are tutor explanations. Conceptual study only; no workflow, code, or Azure commands were run.

#### Turn evaluation results into an enforced quality gate

A pull request proposing prompt or configuration changes triggers a workflow that prepares Python, authenticates to Azure, runs evaluation against a test dataset, and reports metrics on the PR. Automated results support human review; they do not replace it.

Reporting failure is not the same as blocking a merge. The source's JavaScript reporting step reads `results.json` and posts a pass/fail comment, but does not itself fail the workflow when `passed` is false. An enforced gate needs both:

- A script or workflow condition that makes a failed quality decision fail the CI check, such as a nonzero exit code.
- Branch protection or repository rulesets requiring that check to pass before merging.

**Tutor example:** a PR comment says “FAILED,” but every Actions step exits successfully. This reports a quality problem without enforcing a merge block. Make the check fail and require it for merging. Execution errors must also block approval, but a dataset-access error is missing evaluation evidence—not a measured prompt-quality failure.

#### Separate federated trust from resource permissions

OIDC federation lets GitHub obtain a short-lived token accepted by Azure without storing a long-lived Azure client secret. Federated trust identifies the allowed repository and workflow context; Azure RBAC separately authorizes the authenticated service principal or managed identity to access resources.

GitHub's `id-token: write` permits requesting an OIDC token, not accessing Foundry. If authentication succeeds but dataset access is denied, inspect the workflow identity's resource permissions and role-assignment scope first.

**Source qualification:** the unit pairs a pull-request trigger with a federated credential subject for the `main` branch. These contexts are not interchangeable; a runnable configuration must match the token-requesting job's context. Exact federation configuration and role requirements remain to be verified against current references before execution.

#### Define the script/reporting contract

The evaluation script needs candidate prompt/configuration inputs, an identifiable test-dataset version, structured metrics and a quality decision, plus diagnostic results. The source's `results.json` includes `metrics`, `passed`, `total_examples`, and `failed_examples`. Its JavaScript step reports the Python results; it does not perform the evaluation.

Handle execution errors and timeouts explicitly. Preserve diagnostics when quality fails and arrange reporting to run on that failure path; stopping immediately can otherwise leave only a red check with no explanation.

**Tutor example:** evaluating v1's saved responses cannot validate a PR proposing v2, even if the required check passes. Generate responses using v2, then evaluate those outputs on the versioned test cases using the intended criteria and quality policy. Run names and workflow success do not establish which candidate was tested.

### G04-U07 — Exercise - Set up automated evaluations
Source: https://learn.microsoft.com/en-us/training/modules/automated-evaluation-genaiops/7-exercise

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this unit in lesson selection, teaching, checks, and review scheduling; it is excluded from tutor completion and TLDR readiness. No website confirmation is required.

### G04-U08 — Knowledge check
Source: https://learn.microsoft.com/en-us/training/modules/automated-evaluation-genaiops/8-knowledge-check

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this closing unit; it is excluded from tutor completion, review scheduling, and TLDR readiness. No website confirmation is required.

### G04-U09 — Summary
Source: https://learn.microsoft.com/en-us/training/modules/automated-evaluation-genaiops/9-summary

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this closing unit; it is excluded from tutor completion, review scheduling, and TLDR readiness. No website confirmation is required.

<a id="key-concepts-and-decision-points"></a>
<a id="python-examples"></a>
<a id="javascript-examples"></a>
<a id="azure-cli-commands"></a>
<a id="related-configuration-yaml-bicep-or-github-actions"></a>
<a id="worked-examples-and-practice"></a>
<a id="common-pitfalls-and-clarifications"></a>

## Remaining study and examples

- G04-U04: upload prerequisites and the supported Python API have been examined conceptually; local configuration, installed package versions, and actual upload execution remain unverified. No dedicated Azure lab was performed.
- G04-U05: connection, definition/run/poll/results operations and prerequisites have been examined conceptually. A complete assembled script, installed versions, live execution, and production polling hardening remain unverified. The context input was identified in practice; supplying the actual policy text was clarified by the tutor and remains a useful transfer check.
- G04-U06: workflow triggers, enforced quality gates, OIDC/RBAC separation, candidate-response provenance, and result reporting have been examined conceptually. Runnable YAML/Python/JavaScript integration, precise federation context and permissions, dependency alignment with U05, and live execution remain unverified.
- Python, JavaScript, Azure CLI, and YAML/Bicep/GitHub Actions examples remain pending; relevance is not yet assessed. Record prerequisites, versions, expected outcomes, and execution status where applicable.

[Optional quiz history](quizzes.md)

## Microsoft Learn search terms
- Microsoft Foundry Python batch evaluation datasets evaluators
- AI evaluation groundedness relevance coherence fluency
- GitHub Actions automated AI evaluation workflow
