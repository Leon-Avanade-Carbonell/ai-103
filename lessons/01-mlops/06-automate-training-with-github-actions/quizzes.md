# Quizzes — Automate model training with GitHub Actions

- Module ID: M06
- Notes: [Lesson notes](notes.md)
- Source: https://learn.microsoft.com/en-us/training/modules/trigger-azure-machine-learn-jobs-github-actions/
- Evidence identity: session ID plus question ID; one optional quiz per session, Q01–Q10 unique within that session. Resume/retry preserves IDs and initial answers.

Tutor-created formative checks, not official Microsoft assessments.

## Quiz history

<a name="quiz-2026-11-12-session-06"></a>

### Optional tutor quiz — 2026-11-12-session-06

- Date: 2026-11-12
- Units: [M06-U01 — Introduction](notes.md#m06-u01--introduction)
- Verified source: https://learn.microsoft.com/en-us/training/modules/trigger-azure-machine-learn-jobs-github-actions/1-introduction (fetched 2026-11-12).
- Participation: declined.
- Context: offered Short quiz, Full quiz, or Skip quiz at lesson closure; learner selected “Skip quiz.” This is a session-specific decline, not a blanket preference.
- Requested/planned: not applicable; no quiz selected.
- Presented / valid answered: 0 / 0.
- Count scope: this single-module session only.
- Evidence provenance: current-session selection returned by the question tool. No quiz questions were presented; no item records or score apply. The ordinary application check is separate and is retained in the memory session.

<a name="quiz-2026-11-12-session-07"></a>

### Optional tutor quiz — 2026-11-12-session-07

- Date: 2026-11-12
- Units: [M06-U02 — Use source control for machine learning assets](notes.md#m06-u02--use-source-control-for-machine-learning-assets)
- Verified source S1: https://learn.microsoft.com/en-us/training/modules/trigger-azure-machine-learn-jobs-github-actions/2-understand-business-problem (fetched 2026-11-12). All items cite S1; reproducibility wording also uses explicitly taught tutor clarifications.
- Participation: completed.
- Requested/planned: Short quiz, up to 5 / 5 questions.
- Presented / valid answered: 5 / 5.
- Correct / incorrect / skipped / invalid / unasked or unanswered: 5 / 0 / 0 / 0 / 0.
- Score: 5/5.
- Difficulty mix: 1 easy, 4 medium; 4 single-answer, 1 multiple-answer. Multiple-answer scoring requires the exact set.
- Count scope: this single-module session only.
- Evidence provenance: current-session initial responses returned by the question tool; no code or Azure execution evidence. Not an official assessment.

<a name="quiz-2026-11-12-session-07-q01"></a>

#### Q01 — Training recipe; easy; single-answer; M06-U02; S1

Prompt: Where should a training script and its dependency definition normally be versioned? Select one answer.
- A. Azure Key Vault — Store both as secret values.
- B. Git repository — Version both as part of the training recipe.
- C. Azure ML model assets — Register both as trained models.
- D. Training job logs — Keep both only as execution logs.

Initial learner selections: B. Git repository.
Correct set: B.
Outcome: correct.
Explanation: Scripts and dependency definitions describe the training recipe and belong in Git. Key Vault holds secrets, model assets hold trained models, and job logs record execution rather than replace source control.
Follow-up: none.

<a name="quiz-2026-11-12-session-07-q02"></a>

#### Q02 — Assets outside Git; medium; multiple-answer; M06-U02; S1

Prompt: Which two files should normally stay OUT of your Git repository? Select two answers.
- A. Component definition YAML — Defines a pipeline component.
- B. requirements.txt — Lists Python dependencies.
- C. Raw 20-GB training dataset — Contains the training records.
- D. Azure access credential — Grants access to Azure resources.

Initial learner selections: C. Raw 20-GB training dataset; D. Azure access credential.
Correct set: C, D.
Outcome: correct (exact match).
Explanation: Store the dataset in a suitable data service and the credential in a secret store. Component YAML and dependency files belong in Git.
Follow-up: none.

<a name="quiz-2026-11-12-session-07-q03"></a>

#### Q03 — Model registration; medium; single-answer; M06-U02; S1

Prompt: Training produces model.pkl. Your team wants to manage it as a named, versioned model for later use. What should you do? Select one answer.
- A. Commit the binary to Git — Manage it alongside training scripts.
- B. Store it in Key Vault — Manage it as a secret.
- C. Keep only a log message — Record that training finished.
- D. Register an Azure ML model asset — Manage the trained artifact by name and version.

Initial learner selections: D. Register an Azure ML model asset.
Correct set: D.
Outcome: correct.
Explanation: Registration provides named, versioned model management. A job may retain the original output, distinct from registration. Git is for the recipe, Key Vault for secrets, and a log message cannot replace the artifact.
Follow-up: none.

<a name="quiz-2026-11-12-session-07-q04"></a>

#### Q04 — Commit traceability; medium; single-answer; M06-U02; S1

Prompt: A model's performance regresses after a preprocessing change. Why is recording the producing Git commit useful? Select one answer.
- A. It identifies the code change to inspect — Review the producing recipe and compare it with an earlier commit.
- B. It contains the dataset automatically — Recover all training records from the commit.
- C. It guarantees acceptable model quality — A recorded commit establishes model accuracy.
- D. It replaces model registration — No separate trained artifact needs to be retained.

Initial learner selections: A. It identifies the code change to inspect.
Correct set: A.
Outcome: correct.
Explanation: The commit lets you inspect and compare the producing code. It does not automatically contain the dataset, certify model quality, or replace storing and registering the model.
Follow-up: none.

<a name="quiz-2026-11-12-session-07-q05"></a>

#### Q05 — Data version and reproducibility; medium; single-answer; M06-U02; S1 and taught tutor clarification

Prompt: You restore the original training code, dependency definitions, and settings, but train on a newer dataset. Which conclusion is justified? Select one answer.
- A. The original model is guaranteed — An unchanged Git commit fixes every training input.
- B. Training now requires the old model as input — Every training run starts from a registered model.
- C. The model may differ because the data changed — Reproducing a run also requires identifying its data version.
- D. Git should store the credential instead — Credential storage determines the model's learned behavior.

Initial learner selections: C. The model may differ because the data changed.
Correct set: C.
Outcome: correct.
Explanation: A changed dataset can change the trained model. The commit does not fix every input, ordinary training need not start from an old model, and credentials control access rather than learned behavior.
Follow-up: none.

Strengths: appropriate asset storage; distinguishing model registration from job outputs; commit traceability; recognition that a changed dataset may change the model.
Misconceptions and remaining gaps: initial ordinary lesson checks needed tutor clarification of automatic commit links and model-versus-job terminology; all five later quiz selections were correct. Practical implementation remains unverified. Full ordinary check evidence belongs in the memory session.
Review proposal: M06-U02 traceability/reproducibility, 2026-11-15; apply independently which code/data/environment/settings identifiers are needed for a past training run. This is a retention review, not a failed quiz or unit-status reversal.
