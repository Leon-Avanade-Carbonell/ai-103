# Quizzes — Plan and prepare a GenAIOps solution

- Module ID: G01
- Notes: [Lesson notes](notes.md)
- Source: https://learn.microsoft.com/en-us/training/modules/plan-prepare-genaiops/
- Evidence identity: session ID plus question ID; one optional quiz per session, Q01–Q10 unique within that session.

Tutor-created formative checks, not official Microsoft assessments.

## Quiz history

<a name="quiz-2026-11-26-session-03"></a>

### Optional tutor quiz — 2026-11-26-session-03

- Date: 2026-11-26
- Units: [G01-U01 — Introduction](notes.md#g01-u01--introduction)
- Verified source: https://learn.microsoft.com/en-us/training/modules/plan-prepare-genaiops/1-introduction (fetched 2026-11-26).
- Participation: declined.
- Requested/planned: Not applicable; learner selected “Skip quiz” from Short quiz, Full quiz, and Skip quiz options.
- Presented / valid answered: 0 / 0. No quiz items were created.
- Count scope: this module and session only.
- Evidence provenance: direct current-conversation response to the optional quiz offer. Ordinary application-check evidence is retained separately in the memory session.

Declining the optional quiz does not undo the lesson's demonstrated understanding or establish a blanket quiz preference.

<a name="quiz-2026-11-26-session-04"></a>

### Optional tutor quiz — 2026-11-26-session-04

- Date: 2026-11-26
- Units: [G01-U02 — Define agent specifications](notes.md#g01-u02--define-agent-specifications)
- Verified source: https://learn.microsoft.com/en-us/training/modules/plan-prepare-genaiops/2-use-cases (fetched 2026-11-26).
- Participation: declined.
- Requested/planned: Not applicable; learner responded “no need” to the end-of-lesson optional quiz offer.
- Presented / valid answered: 0 / 0. No quiz items were created.
- Count scope: this module and session only.
- Evidence provenance: direct current-conversation response. Ordinary lesson checks, including initial responses and scaffolded clarification, belong in the memory session.

This decline applies to this lesson's optional quiz, not to all future quizzes. No score is assigned.

<a name="quiz-2026-11-26-session-05"></a>

### Optional tutor quiz — 2026-11-26-session-05

- Date: 2026-11-26
- Units: [G01-U03 — Design and optimize your agent](notes.md#g01-u03--design-and-optimize-your-agent)
- Source S: https://learn.microsoft.com/en-us/training/modules/plan-prepare-genaiops/3-select-model (fetched 2026-11-26; page updated 2026-11-04). All items use S; Q04 is a tutor troubleshooting application.
- Participation: completed.
- Requested/planned: Short quiz / 5 questions.
- Presented / valid answered: 5 / 5.
- Correct / incorrect / skipped / invalid / unasked or unanswered: 4 / 1 / 0 / 0 / 0.
- Score: 4/5.
- Difficulty mix: 1 easy, 3 medium, 1 hard. Multiple-answer items use exact-set scoring without partial credit.
- Count scope: this module and session only.
- Evidence provenance: direct current-conversation question-tool responses; no code execution or official assessment result.

<a name="quiz-2026-11-26-session-05-q01"></a>

#### Q01 — Model selection; easy; single-answer; G01-U03; S

Prompt: Question 1/5 — Easy. Select one answer. Which principle should guide model selection for a focused, high-traffic support agent?
- A. Choose the largest model — Prioritize maximum model size over other constraints.
- B. Choose by quality and constraints — Test whether the model meets the rubric within cost and latency requirements.
- C. Choose the smallest model — Prioritize minimum model size regardless of evaluation results.

Initial learner selections: B.
Correct set: B.
Outcome: correct.
Explanation: Match the model to the task and test against the rubric and constraints. A ignores cost and latency; C ignores sufficient quality.

<a name="quiz-2026-11-26-session-05-q02"></a>

#### Q02 — Changing facts; medium; single-answer; G01-U03; S

Prompt: Question 2/5 — Medium. Select one answer. An agent must answer questions about a product catalog that changes daily. Which approach best supplies those changing facts without retraining the model for each update?
- A. Fine-tune on today's catalog — Train the model using a snapshot of product information.
- B. Adjust the friendly-tone prompt — Change the instructions governing response style.
- C. Retrieve catalog data with RAG — Supply relevant external product information when generating answers.

Initial learner selections: C.
Correct set: C.
Outcome: correct.
Explanation: RAG retrieves external facts; its pipeline still needs current data. A can become stale; B changes style rather than factual access.

<a name="quiz-2026-11-26-session-05-q03"></a>

#### Q03 — RAG and fine-tuning; medium; multiple-answer; G01-U03; S

Prompt: Question 3/5 — Medium. Select two answers. Which TWO statements correctly describe RAG and fine-tuning?
- A. Fine-tuning can adapt behavior — Training examples can shape a consistent style or specialized skill.
- B. RAG guarantees grounded answers — Retrieving documents ensures every generated claim is supported.
- C. They can be combined — Use retrieval for current facts and fine-tuning for behavior.
- D. Fine-tuning keeps facts current — Once trained, a model automatically incorporates later policy updates.

Initial learner selections: B, C.
Correct set: A, C.
Outcome: incorrect.
Explanation: A and C describe their complementary roles. B falsely guarantees faithful use of evidence; D falsely implies automatic learning of later updates. The initial selection remains unchanged after feedback.
Follow-up: Tutor explained that finding evidence and using it faithfully are separate checks. Q04 was answered correctly after that explanation; this is scaffolded transfer, not a retry or an independent pre-feedback correction of Q03.

<a name="quiz-2026-11-26-session-05-q04"></a>

#### Q04 — Diagnose answer generation; hard; single-answer; G01-U03; S

Prompt: Question 4/5 — Hard. Select one answer. Logs show that the agent received the correct access-policy passage, but its answer gives instructions that contradict that passage. What is the best next investigation?
- A. Refresh the policy index only — Treat stale source data as the established cause.
- B. Inspect how the answer is generated — Check prompt instructions and interpretation of supplied context, then evaluate a correction.
- C. Release because retrieval worked — Treat successful document retrieval as sufficient evidence of answer quality.

Initial learner selections: B.
Correct set: B.
Outcome: correct.
Explanation: Correct context reached the model, so investigate its use of that context. A assumes a data problem despite the evidence; C overlooks the incorrect answer. Tutor application of the source's grounding and optimization principles, delivered after Q03 feedback.

<a name="quiz-2026-11-26-session-05-q05"></a>

#### Q05 — Release evaluation; medium; multiple-answer; G01-U03; S

Prompt: Question 5/5 — Medium. Select two answers. Before releasing a substantial prompt change, which TWO actions best support the lesson's optimization loop?
- A. Repeat only one successful request — Use consistency on that request as the entire release check.
- B. Run quick smoke tests — Check a small set of known cases for obvious regressions.
- C. Judge only the improved tone — Accept the change if answers sound friendlier.
- D. Run broader rubric-based evaluation — Evaluate representative requests, including ambiguous and boundary cases.

Initial learner selections: B, D.
Correct set: B, D.
Outcome: correct.
Explanation: Smoke tests offer fast feedback and broader rubric-based evaluation supports release decisions. A lacks coverage; C ignores other quality requirements.

Strengths: Model selection considers quality and constraints; RAG fits changing facts; release checks combine smoke tests and broader evaluation.

Remaining gap: [Q03](#quiz-2026-11-26-session-05-q03) showed an unsupported guarantee of groundedness from RAG. [Q04](#quiz-2026-11-26-session-05-q04) showed correct troubleshooting after feedback; independent transfer remains worth checking.

Review proposal: G01-U03, 2026-11-29, with learner agreement: distinguish incorrect retrieval from unsupported generation in a new scenario and select evidence needed to diagnose each.

<a name="quiz-2026-11-26-session-06"></a>

### Optional tutor quiz — 2026-11-26-session-06

- Date: 2026-11-26
- Units: [G01-U04 — Explore the GenAIOps lifecycle](notes.md#g01-u04--explore-the-genaiops-lifecycle)
- Verified source: https://learn.microsoft.com/en-us/training/modules/plan-prepare-genaiops/4-lifecycle-overview (fetched 2026-11-26; page updated 2026-11-04).
- Participation: declined.
- Requested/planned: Not applicable; learner selected “Skip quiz” from Short quiz, Full quiz, and Skip quiz options.
- Presented / valid answered: 0 / 0. No quiz items were created.
- Count scope: this module and session only.
- Evidence provenance: direct current-conversation response to the optional quiz offer. Ordinary lesson-check responses, feedback, and scaffolded recovery are retained separately in the memory session.

This decline applies only to this lesson's optional quiz. No score is assigned, and it does not undo understanding demonstrated in the lesson checks.

<a name="quiz-2026-11-26-session-07"></a>

### Optional tutor quiz — 2026-11-26-session-07

- Date: 2026-11-26
- Units: [G01-U05 — Explore available tools and frameworks to implement GenAIOps](notes.md#g01-u05--explore-available-tools-and-frameworks-to-implement-genaiops)
- Verified source: https://learn.microsoft.com/en-us/training/modules/plan-prepare-genaiops/5-tools-frameworks (fetched 2026-11-26; page updated 2026-11-04).
- Participation: declined.
- Requested/planned: Not applicable; learner selected “Skip quiz” from Short quiz, Full quiz, and Skip quiz options.
- Presented / valid answered: 0 / 0. No quiz items were created.
- Count scope: this module and session only.
- Evidence provenance: direct current-conversation response to the optional quiz offer. Ordinary lesson-check prompts, responses, and feedback are retained separately in the memory session.

This decline applies only to this lesson's optional quiz. No score is assigned, and it does not undo understanding demonstrated in the lesson checks.
