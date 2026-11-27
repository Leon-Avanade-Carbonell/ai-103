# Evaluate and optimize AI agents through structured experiments

- Module ID: G03
- Source: https://learn.microsoft.com/en-us/training/modules/evaluate-optimize-agents/
- Curriculum verified: 2026-10-28
- Exam objectives: D4 quality evaluation; D5 experiment-based optimization foundations.

## Overview and learning goals

Planned source goals: design experiments with quality/cost/performance metrics, organize agent variants with Git, create consistent scoring rubrics, and compare results for evidence-based optimization.

## Notes by Microsoft Learn unit

### G03-U01 — Introduction
Source: https://learn.microsoft.com/en-us/training/modules/evaluate-optimize-agents/1-introduction

Source fetched: 2026-11-27; page updated: 2026-11-04.

#### Optimize with evidence, not guesswork

A cheaper model is useful only if the agent's quality and response time remain acceptable. Microsoft Learn frames optimization around three dimensions: **quality, cost, and performance**. Controlled experiments isolate a change, while shared scoring rubrics make comparisons consistent rather than dependent on individual impressions.

For a model comparison, keep the prompts, test cases, and scoring rubric unchanged. Changing both the model and prompt makes it difficult to identify which change caused an improvement or regression.

**Tutor example — conceptual, no code or Azure execution:** A support team tests a cheaper model using the same prompts and test requests. Compare cost, output quality, and response time before adopting it. Safety is an additional criterion raised by the learner; define it consistently across variants. Savings alone do not justify adoption if required quality or performance deteriorates.

The module develops experiment design, Git-based organization of variants, and consistent evaluation rubrics; those methods remain to be studied in the following units.

### G03-U02 — Design evaluation experiments
Source: https://learn.microsoft.com/en-us/training/modules/evaluate-optimize-agents/2-design-evaluation-experiments

Source fetched: 2026-11-27; page updated: 2026-11-04. The explanations below follow Microsoft Learn; examples are tutor-created conceptual practice, with no code or Azure execution.

#### Define acceptance before testing

Evaluate **quality, cost, and performance** together. Quality measures whether the agent solves the task correctly; groundedness matters when answers rely on retrieved documents. Cost depends on token usage and the model's pricing. Performance includes complete response time and, for streaming, time-to-first-token. Showing an answer sooner is distinct from completing it sooner.

Set acceptance thresholds before seeing results. A cheaper, faster variant is unsuitable if it fails a required quality threshold. An average-quality target and a minimum per-answer target serve different purposes: the minimum prevents a strong average from hiding seriously poor answers.

**Worked tutor example:** Require average quality ≥4.2/5, no answer below 3.5, at least 50% lower cost, and average complete response time <10 seconds. A candidate with 60% cost savings, 7-second responses, and average quality 4.4 still fails if two answers score 2/5. These are illustrative business thresholds, not universal Azure requirements.

#### Compare one change at a time

Use the current agent as the **baseline**. A variant can change the system prompt, model, or an agent setting. Isolate one change first; otherwise an improvement could come from either change or their interaction. Successful individual changes can later be tested together.

**Tutor example — shorter system prompt:** Change only the system prompt. Keep the model, agent settings, tools/retrieval setup, test requests, and scoring criteria fixed. Compare quality, cost, and performance against the baseline using the same requests. User test requests are not the same thing as system-prompt variants: expanding test coverage does not require introducing another agent configuration.

#### Test representative requests and edge cases

Include typical use cases and challenging requests, such as ambiguity or missing information. Each case needs a request, expected information needs, and ideal response characteristics so comparisons are repeatable. Microsoft Learn suggests 5–10 diverse prompts for manual testing or smoke tests; this is a practical starting point, not comprehensive production validation.

**Tutor-supplied edge case:** For “Can I return this?”, a support agent should ask for the details needed to determine eligibility rather than invent a policy or approve the return without enough information.

Passing thresholds on five easy questions supports only those tested cases. Before a deployment decision, evaluate the same baseline and variant on representative and challenging user requests; avoid generalizing from easy cases alone.

Document baseline and variant configurations, test requests, scoring criteria, acceptance thresholds, and rationale. Record quality scores, token usage/cost, and response times for each variant so another person can reproduce the comparison and inspect weaknesses hidden by averages.

### G03-U03 — Apply Git-based workflows to optimization experiments
Source: https://learn.microsoft.com/en-us/training/modules/evaluate-optimize-agents/3-git-based-experimentation-workflow

Source fetched: 2026-11-27; page updated: 2026-11-04. The workflow follows Microsoft Learn; the examples below are tutor-created conceptual illustrations, not executed Git or Foundry operations.

#### Isolate each variant from the same baseline

Create one experiment branch per variant, changing one factor at a time. Compare each with the same baseline using the same test requests and scoring criteria. Changing both the system prompt and model makes a quality change difficult to attribute: either change or their interaction could be responsible. Successful individual changes can later be tested together.

```text
main                             # Production baseline
experiment/prompt-concise         # Change only the system prompt
experiment/cheaper-model          # Change only the model
```

Git records the configuration changes; evaluation supplies evidence about their effects.

#### Retain outputs as well as scores

Keep system prompts, user test requests, and evaluation results distinct:

```text
prompts/                  # System prompts defining agent behavior
test-prompts/             # User requests used to test every variant
experiments/prompt-concise/
    agent-responses.json  # Captured outputs
    evaluation.csv        # Scores and observations
```

The source workflow checks out an experiment branch, creates the corresponding agent version, runs the test requests, captures responses, and then manually scores them. Use consistent evaluation criteria and formats across manual, portal, and automated evaluations so results can be compared and consolidated. Script implementation and execution were not covered here.

Raw responses let reviewers inspect actual failures; scores and comments explain how outputs performed against the shared criteria. Preserve the tested configuration and test requests for traceability and reproduction. Before deleting an unsuccessful branch, ensure its results and rationale are already committed and documented elsewhere. Keeping the record prevents repeated unsuccessful approaches.

#### Merge an accepted configuration; deploy it separately

Compare variants against predefined acceptance criteria, then merge a successful experiment into `main` and tag the accepted revision for traceability. A Git merge does not by itself deploy an agent; a separate deployment action or configured automation must do that. Release controls such as traffic management depend on the serving architecture, not on the merge alone.

**Worked tutor example:** A shorter-prompt variant meets all required quality, cost, and response-time thresholds. A cheaper-model variant saves more money but fails the quality threshold. Choose the shorter-prompt variant, retain the cheaper model's failure evidence, and deploy the accepted configuration through the appropriate release process.

### G03-U04 — Apply evaluation rubrics for consistent scoring
Source: https://learn.microsoft.com/en-us/training/modules/evaluate-optimize-agents/4-evaluate-agent-responses

Source fetched: 2026-11-27; page updated: 2026-11-04. The process below follows Microsoft Learn; returns-assistant examples are tutor-created conceptual illustrations, not executed evaluations.

#### Define what each score means

A metric says **what to judge**; a rubric says **how to score it**. Include the metric definition, descriptions for each score level, and concrete example responses. Vague guidance such as “score helpfulness” lets evaluators interpret “good” differently, making an apparent improvement indistinguishable from more generous scoring.

**Tutor example — returns assistant:** For “My headphones arrived damaged. How do I get a replacement?”, an intent-resolution rubric might distinguish a complete replacement process, a partial answer missing important steps, and an answer that misses the request entirely. Groundedness needs its own rubric: are the stated steps supported by the supplied returns policy? Clarify how accuracy affects intent resolution too; an apparently complete list of incorrect steps should not automatically receive the highest score. Separate metrics diagnose weaknesses rather than making unsupported instructions acceptable.

#### Calibrate before comparing variants

Select 5–8 responses spanning strong, weak, and ambiguous examples. Evaluators score independently without seeing intended scores, then compare interpretations. Discuss differences greater than one point, clarify the rubric, and repeat until the team applies it consistently. Calibration resolves reasons for disagreement; it is not simply asking everyone to copy a preferred score.

Keep rubrics and calibrated examples in the repository for new evaluators and refreshers. Align manual criteria with supported built-in or custom automated evaluators where appropriate, enabling later automation with human spot-checks. No automated evaluator API or implementation was verified here.

#### Agreement is not answer quality

Check **inter-rater reliability** by having multiple evaluators independently score the same responses. The source suggests 10–15 responses and at least 80% agreement within one point as practical guidance for small manual-evaluation teams, not a universal production requirement. For each response and metric, the highest and lowest scores must differ by no more than one.

| Evaluator scores | Agreement |
| --- | --- |
| 4, 4, 4 | Exact; also counts as within one point |
| 3, 4, 4 | Within one point |
| 2, 4, 5 | Divergent |

**Worked tutor example:** Six exact agreements plus three additional within-one-point agreements among ten responses give 9/10, or 90%, meeting the source's target. This establishes scoring consistency, not high-quality answers: evaluators can consistently agree that responses deserve 1/5. Low scores indicate weaknesses in the agent on the evaluated criteria and test cases.

Review divergent cases, refine rubrics, and recalibrate if agreement drops below the target. Check at major optimization initiatives, when evaluators join, and periodically to catch scoring drift. Percent agreement is a simple measure; more formal reliability statistics exist but were not studied here.

### G03-U05 — Exercise - Evaluate and compare AI agent versions
Source: https://learn.microsoft.com/en-us/training/modules/evaluate-optimize-agents/5-exercise

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this unit in lesson selection, teaching, checks, and review scheduling; it is excluded from tutor completion and TLDR readiness. No website confirmation is required.

### G03-U06 — Knowledge check
Source: https://learn.microsoft.com/en-us/training/modules/evaluate-optimize-agents/6-knowledge-check

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this closing unit; it is excluded from tutor completion, review scheduling, and TLDR readiness. No website confirmation is required.

### G03-U07 — Summary
Source: https://learn.microsoft.com/en-us/training/modules/evaluate-optimize-agents/7-summary

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this closing unit; it is excluded from tutor completion, review scheduling, and TLDR readiness. No website confirmation is required.

<a id="key-concepts-and-decision-points"></a>
<a id="python-examples"></a>
<a id="javascript-examples"></a>
<a id="azure-cli-commands"></a>
<a id="related-configuration-yaml-bicep-or-github-actions"></a>
<a id="worked-examples-and-practice"></a>
<a id="common-pitfalls-and-clarifications"></a>

## Remaining study and examples

- G03-U04: full calibration-set design and an independent reliability-check exercise remain unverified; conceptual rubric and agreement distinctions were covered.
- G03-U03: runnable agent creation/testing scripts and practical Git/Foundry execution remain unverified; the conceptual workflow was covered without a dedicated lab.
- Python, JavaScript, Azure CLI, and YAML/Bicep/GitHub Actions examples remain pending; relevance is not yet assessed. Record prerequisites, versions, expected outcomes, and execution status where applicable.

[Optional quiz history](quizzes.md)

## Microsoft Learn search terms
- AI agent evaluation experiments quality cost performance
- Git agent variants evaluation rubrics
- Microsoft Foundry compare agent experiment results
