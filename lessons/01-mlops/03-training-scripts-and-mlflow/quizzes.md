# Quizzes — Run training scripts and track models with MLflow in Azure Machine Learning

- Module ID: M03
- Notes: [Lesson notes](notes.md)
- Source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/
- Evidence identity: session ID plus question ID; one optional quiz per session, Q01–Q10 unique within that session. Retries preserve initial answers.

Tutor-created formative checks, not official Microsoft assessments.

## Quiz history

<a name="quiz-2026-11-04-session-05"></a>

### Optional tutor quiz — 2026-11-04-session-05

- Date: 2026-11-04
- Units: [M03-U01 — Introduction](notes.md#m03-u01--introduction)
- Verified source (S1): https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/1-introduction — fetched 2026-11-04.
- Participation: completed
- Requested/planned: Short quiz (up to 5); 3 planned because the introduction is narrow.
- Presented / valid answered: 3 / 3
- Correct / incorrect / skipped / invalid / unasked or unanswered: 3 / 0 / 0 / 0 / 0
- Score: 3/3
- Difficulty mix and scoring: 1 easy, 2 medium; exact-set scoring for the multiple-answer item.
- Count scope: this module only; also the session-wide totals.
- Evidence provenance: current-session responses returned by the interactive question tool; no execution evidence or official assessment outcome.

<a name="quiz-2026-11-04-session-05-q01"></a>

#### Q01 — Interactive development; easy; single-answer; M03-U01; S1

Prompt: Question 1/3 — Easy. Select one answer. Which workflow is the best fit for interactive exploration while you are still developing your training approach?
- A. Develop in a notebook — Explore data and revise training code interactively.
- B. Submit a fixed training script — Execute an already-defined training workflow as a command job.
- C. Inspect existing MLflow records — Review evidence from previously tracked runs.

Initial learner selections: A. Develop in a notebook.
Correct set: {A}
Outcome: correct
Explanation: The source positions notebooks as ideal for interactive experimentation and development. B executes an established workflow; C reviews recorded evidence rather than developing training code. Source: S1.
Follow-up: None.

<a name="quiz-2026-11-04-session-05-q02"></a>

#### Q02 — Command-job configuration; medium; multiple-answer; M03-U01; S1

Prompt: Question 2/3 — Medium. Select two answers. You are configuring an Azure Machine Learning command job to run an existing training script. Which two settings does the introduction explicitly identify as configurable for the job?
- A. Weekly recurrence — The calendar rule for repeated submissions.
- B. Input data — The data supplied to the training workload.
- C. Compute environment — The environment in which the workload executes.
- D. Guaranteed model accuracy — A required outcome that execution must achieve.

Initial learner selections: C. Compute environment, B. Input data (set {B, C}).
Correct set: {B, C}
Outcome: correct
Explanation: The introduction names input data and the compute environment. A is a recurring-automation concern, not one of the settings named here; D is not a guaranteed training outcome. Exact-set match. Source: S1, with tutor scheduling clarification from the lesson.
Follow-up: None.

<a name="quiz-2026-11-04-session-05-q03"></a>

#### Q03 — Comparing tracked runs; medium; single-answer; M03-U01; S1

Prompt: Question 3/3 — Medium. Select one answer. Your training script has run three times with different settings. You want to compare those settings, measured performance, and saved output files. What role should MLflow play?
- A. Schedule the next training run — Provide the recurring trigger for future execution.
- B. Replace the training algorithm — Perform training instead of the script's training code.
- C. Guarantee the best deployment choice — Select a production-ready model without further evaluation.
- D. Track parameters, metrics, artifacts — Retain run evidence for comparison and next-step decisions.

Initial learner selections: D. Track parameters, metrics, artifacts.
Correct set: {D}
Outcome: correct
Explanation: MLflow retains parameters, metrics, and artifacts for comparison. It does not supply the recurring trigger, replace training code, or guarantee production readiness. Source: S1, with tutor clarifications from the lesson.
Follow-up: None.

Strengths: Recognized notebooks' interactive role, configurable job inputs/environment, and MLflow's comparison role across Q01–Q03.
Misconceptions and remaining gaps: No incorrect quiz answers. The ordinary lesson check initially conflated job execution with its recurring trigger; feedback and a scheduler follow-up clarified it. Practical execution remains unverified. Full ordinary-check evidence belongs in memory.
Review proposals: No new mandatory review from the quiz; reuse these distinctions naturally in M03-U02–U03.
