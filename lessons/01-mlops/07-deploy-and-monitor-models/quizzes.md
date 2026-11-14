# Quizzes — Deploy and monitor a model in Azure Machine Learning

- Module ID: M07
- Notes: [Lesson notes](notes.md)
- Source: https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/
- Evidence identity: session ID plus question ID; one optional quiz per session, Q01–Q10 unique within that session.

Tutor-created formative checks, not official Microsoft assessments.

## Quiz history

<a name="quiz-2026-11-13-session-05"></a>

### Optional tutor quiz — 2026-11-13-session-05

- Date: 2026-11-13
- Units: [M07-U01 — Introduction](notes.md#m07-u01--introduction)
- Verified source: https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/1-introduction (fetched 2026-11-13)
- Participation: declined. Learner response to the optional quiz offer: “no need”.
- Requested/planned: Not applicable; no quiz count selected.
- Presented / valid answered: 0 / 0.
- Count scope: this module and the whole session; no quiz items presented.
- Evidence provenance: current-conversation quiz offer and learner decline. The ordinary lesson application check is separate and retained in the memory session.

No item records or score: declining the optional quiz does not undo demonstrated understanding in the lesson check and does not establish a blanket quiz preference.

<a name="quiz-2026-11-13-session-06"></a>

### Optional tutor quiz — 2026-11-13-session-06

- Date: 2026-11-13
- Units: [M07-U02 — Prepare a model for deployment](notes.md#m07-u02--prepare-a-model-for-deployment)
- Verified source (S1, all items): https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/2-understand-business-problem (fetched 2026-11-13)
- Participation: completed.
- Requested/planned: Short quiz (up to 5) / 4; narrow unit scope, no padding.
- Presented / valid answered: 4 / 4.
- Correct / incorrect / skipped / invalid / unasked or unanswered: 3 / 1 / 0 / 0 / 0.
- Score: 3/4.
- Difficulty mix: 1 easy, 3 medium; single-answer and exact-set multiple-answer scoring.
- Count scope: M07 only; module-local counts equal session-wide counts.
- Evidence provenance: actual initial selections returned by the question tool in this conversation. No retries or independent deployment execution reported.

<a name="quiz-2026-11-13-session-06-q01"></a>

#### Q01 — Endpoint choice; medium; single-answer; M07-U02; S1

Prompt: An appointment-booking application must display a no-show risk prediction immediately after each booking. Which deployment approach fits this requirement? Select one answer.
- A. Scheduled batch endpoint — Collect records and score them in a periodic job.
- B. Managed online endpoint — Return a prediction synchronously for each request.
- C. Registered model only — Store the model as a versioned workspace asset.

Initial learner selections: B. Managed online endpoint.
Correct set: B.
Outcome: correct.
Explanation: Online serving meets the synchronous-response requirement. Periodic batch scoring does not, and registration stores an asset rather than serving it (S1).
Follow-up: No retry.

<a name="quiz-2026-11-13-session-06-q02"></a>

#### Q02 — MLflow no-code deployment; medium; single-answer; M07-U02; S1

Prompt: A team has a supported MLflow model and wants Azure Machine Learning no-code deployment. What does Azure Machine Learning generate from the model’s MLflow metadata? Select one answer.
- A. A new training dataset — Data for the next retraining run.
- B. Production approval rules — Controls for approving deployment releases.
- C. Scoring script and environment — The inference code and runtime environment.
- D. A retraining schedule — A recurring schedule for updating the model.

Initial learner selections: C. Scoring script and environment.
Correct set: C.
Outcome: correct.
Explanation: MLflow metadata supports generation of inference code and environment, not training data, approval rules, or a retraining schedule (S1).
Follow-up: No retry.

<a name="quiz-2026-11-13-session-06-q03"></a>

#### Q03 — Registered model lifecycle; medium; multiple-answer; M07-U02; S1

Prompt: A team manages registered model versions in Azure Machine Learning. Which two actions follow the lifecycle rules described in this unit? Select two answers.
- A. Update an existing version’s tags — Change descriptive metadata without changing its artifact.
- B. Replace an existing version’s artifact — Keep the same version number after retraining.
- C. Archive a version to delete it — Remove the artifact so workflows cannot reference it.
- D. Register a changed artifact as a new version — Give the retrained model its own version.

Initial learner selections: A. Update an existing version’s tags; D. Register a changed artifact as a new version.
Correct set: A, D.
Outcome: correct (exact match).
Explanation: Tags/descriptions can change on an existing version; changed artifacts require new versions. Replacing the artifact violates that rule, and archiving is not deletion (S1).
Follow-up: No retry.

<a name="quiz-2026-11-13-session-06-q04"></a>

#### Q04 — Repeatability versus predictive quality; easy; single-answer; M07-U02; S1

Prompt: Why does the unit recommend automating registration, deployment, and testing when a model is regularly retrained? Select one answer.
- A. To avoid registering model versions — Deploy without keeping versioned assets.
- B. To make repeated releases less error-prone — Replace recurring manual steps with a repeatable pipeline.
- C. To guarantee prediction accuracy — Ensure every retrained model is accurate in production.
- D. To remove the need for testing — Treat successful registration as sufficient validation.

Initial learner selections: C. To guarantee prediction accuracy.
Correct set: B.
Outcome: incorrect.
Explanation: The source motivates automation by slow, error-prone manual releases. Tutor feedback clarified that process repeatability does not guarantee predictive quality. Automation retains registration and testing rather than eliminating them (S1).
Follow-up: Tutor supplied the distinction; no learner response or recovery check after feedback.

Strengths: appropriate endpoint selection, supported MLflow no-code deployment requirements, and version-management rules (Q01–Q03).
Remaining gap: release-process reliability versus predictive accuracy (Q04); explanation supplied, independent recovery not yet demonstrated.
Review proposal: M07-U02, 2026-11-14, brief conceptual check with agreement on why a repeatable pipeline can deploy a poor model. Quiz percentage alone is not mastery or an official assessment pass.
