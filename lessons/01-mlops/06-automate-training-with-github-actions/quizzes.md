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

<a name="quiz-2026-11-13-session-01"></a>

### Optional tutor quiz — 2026-11-13-session-01

- Date: 2026-11-13
- Units: [M06-U03 — Apply trunk-based development](notes.md#m06-u03--apply-trunk-based-development)
- Verified source: https://learn.microsoft.com/en-us/training/modules/trigger-azure-machine-learn-jobs-github-actions/3-explore-solution-architecture (fetched 2026-11-13).
- Participation: declined.
- Context: offered Short quiz, Full quiz, or Skip quiz at lesson closure; learner selected “Skip quiz.” This is a session-specific decline, not a blanket preference.
- Requested/planned: not applicable; no quiz selected.
- Presented / valid answered: 0 / 0.
- Count scope: this single-module session only.
- Evidence provenance: current-session selection returned by the question tool. No quiz questions were presented; no item records or score apply. The two ordinary conceptual checks are separate and are retained in the memory session.

<a name="quiz-2026-11-13-session-04"></a>

### Optional tutor quiz — 2026-11-13-session-04

- Date: 2026-11-13
- Units: [M06-U06 — Trigger Azure Machine Learning jobs and pipelines](notes.md#m06-u06--trigger-azure-machine-learning-jobs-and-pipelines)
- Verified source S1: https://learn.microsoft.com/en-us/training/modules/trigger-azure-machine-learn-jobs-github-actions/6-trigger-azure-machine-learning-jobs (fetched 2026-11-13). All items cite S1; Q05 also uses the explicitly taught quality-acceptance clarification.
- Participation: completed.
- Requested/planned: Short quiz, up to 5 / 5 questions.
- Presented / valid answered: 5 / 5.
- Correct / incorrect / skipped / invalid / unasked or unanswered: 2 / 3 / 0 / 0 / 0.
- Score: 2/5.
- Difficulty mix: 2 easy, 2 medium, 1 hard; 3 single-answer, 2 multiple-answer. Exact-set scoring for multiple-answer items, no partial credit.
- Count scope: this single-module session only.
- Evidence provenance: current-session initial selections returned by the question tool. No execution evidence; not an official assessment. Feedback below is tutor supplied; no post-feedback learner retries were given.

<a name="quiz-2026-11-13-session-04-q01"></a>

#### Q01 — On-demand trigger; easy; single-answer; M06-U06; S1

Prompt: You want a team member to start a workflow on demand from the GitHub UI. Select one answer.
- A. schedule — Use a time-based trigger.
- B. workflow_dispatch — Use an on-demand workflow trigger.
- C. push — Use a branch-update trigger.
- D. repository_dispatch — Use an external repository event.

Initial learner selections: B. workflow_dispatch.
Correct set: B.
Outcome: correct.
Explanation: workflow_dispatch supports on-demand runs; schedule is time-based, push responds to commits, and repository_dispatch receives external API-generated events.
Follow-up: none.

<a name="quiz-2026-11-13-session-04-q02"></a>

#### Q02 — Single-script job; easy; single-answer; M06-U06; S1

Prompt: Training fits in one script, with no need to connect separate reusable components. Which Azure ML job type is the straightforward choice? Select one answer.
- A. Pipeline job — Submit a graph of connected components.
- B. GitHub Actions job — Run steps directly on a GitHub runner.
- C. Command job — Run a script on Azure ML compute.

Initial learner selections: C. Command job.
Correct set: C.
Outcome: correct.
Explanation: A command job suits a single-script Azure ML workload; a pipeline connects components, while a GitHub Actions job is not an Azure ML job type.
Follow-up: none.

<a name="quiz-2026-11-13-session-04-q03"></a>

#### Q03 — Azure-event bridge; medium; multiple-answer; M06-U06; S1

Prompt: New training data arrives in Azure Storage. You want this Azure-side event to start a GitHub workflow that submits training. Select TWO correct statements.
- A. Actions subscribes directly to Event Grid — Connect Event Grid directly to the workflow trigger.
- B. Use a Function or Logic App intermediary — Receive the Azure event and call GitHub.
- C. Use repository_dispatch at GitHub — Accept an external API-generated event.
- D. Use pull_request for the storage event — Treat the arrival of data as pull-request activity.

Initial learner selections: C. Use repository_dispatch at GitHub; D. Use pull_request for the storage event (returned in that order).
Correct set: B, C.
Outcome: incorrect.
Explanation: C was correctly selected, B was missing, and D was incorrectly selected. Actions does not natively subscribe to Event Grid; an intermediary receives the event, authenticates to GitHub and calls its API. Storage arrival is not pull-request activity. Bridge: Azure event → intermediary → GitHub API → workflow.
Follow-up: tutor explanation only; no learner retry.

<a name="quiz-2026-11-13-session-04-q04"></a>

#### Q04 — Post-merge trigger; medium; single-answer; M06-U06; S1

Prompt: Your repository requires reviewed changes before merging into main. Which trigger best fits training after those changes land on main? Select one answer.
- A. workflow_dispatch — Start each training run on demand.
- B. schedule — Start training at fixed times.
- C. pull_request — Start validation for proposed changes.
- D. push filtered to main — Start training when commits land on main.

Initial learner selections: C. pull_request.
Correct set: D.
Outcome: incorrect.
Explanation: A merge updates main and produces the push event for this scenario. pull_request normally validates proposed changes; manual and scheduled triggers do not directly match code landing. Other GitHub event configurations exist, but the standard source distinction is PR validation versus post-merge push training.
Follow-up: tutor explanation only; no learner retry.

<a name="quiz-2026-11-13-session-04-q05"></a>

#### Q05 — Submission, execution, quality; hard; multiple-answer; M06-U06; S1 and taught tutor clarification

Prompt: Azure ML accepts a pipeline submission. Later, every component completes without execution errors, but evaluation reports a metric below your acceptance threshold. Select TWO correct conclusions.
- A. Submission acceptance proved training had finished — Treat acceptance as completion evidence.
- B. The pipeline completed successfully as an execution — Its components finished without execution errors.
- C. Model quality is automatically acceptable — Treat successful evaluation execution as sufficient quality.
- D. The model fails the stated quality requirement — Its reported metric is below the acceptance threshold.

Initial learner selections: D. The model fails the stated quality requirement; A. Submission acceptance proved training had finished (returned in that order).
Correct set: B, D.
Outcome: incorrect.
Explanation: D was correctly selected, B was missing, and A was incorrectly selected. Completion without errors establishes execution success; the below-threshold metric fails quality acceptance. Submission acceptance precedes completion, and an evaluation can execute successfully yet report unacceptable quality.
Follow-up: tutor explanation only; no learner retry.

Strengths: [Q01](#quiz-2026-11-13-session-04-q01) on-demand trigger and [Q02](#quiz-2026-11-13-session-04-q02) command-job selection; partial correct selections in Q03 and Q05 show recognition of repository_dispatch and quality rejection, not exact-set success.
Misconceptions and remaining gaps: [Q03](#quiz-2026-11-13-session-04-q03) intermediary versus PR activity; [Q04](#quiz-2026-11-13-session-04-q04) proposed versus merged changes; [Q05](#quiz-2026-11-13-session-04-q05) submission versus completed execution. No post-feedback independent recovery demonstrated. Practical submission/waiting and deferred M06-U07 exercise remain unverified.
Review proposal: M06-U06, 2026-11-14, with agreement; independently map code/data events to triggers and bridge, and separate submission, execution, and quality outcomes. Recommend retaining the unit in progress until those goals are demonstrated; quiz score alone is not a completion rule.

<a name="quiz-2026-11-13-session-03"></a>

### Optional tutor quiz — 2026-11-13-session-03

- Date: 2026-11-13
- Units: [M06-U05 — Connect GitHub Actions to Azure Machine Learning securely](notes.md#m06-u05--connect-github-actions-to-azure-machine-learning-securely)
- Verified source: https://learn.microsoft.com/en-us/training/modules/trigger-azure-machine-learn-jobs-github-actions/5-connect-github-actions-azure (fetched 2026-11-13).
- Participation: declined.
- Context: offered Short quiz, Full quiz, or Skip quiz at lesson closure; learner selected “Skip quiz.” This is a session-specific decline, not a blanket preference.
- Requested/planned: not applicable; no quiz selected.
- Presented / valid answered: 0 / 0.
- Count scope: this single-module session only.
- Evidence provenance: current-session selection returned by the question tool. No quiz questions were presented; no item records or score apply. Ordinary lesson checks and scaffolded follow-up evidence are separate and are retained in the memory session.

<a name="quiz-2026-11-13-session-02"></a>

### Optional tutor quiz — 2026-11-13-session-02

- Date: 2026-11-13
- Units: [M06-U04 — Validate changes with GitHub Actions](notes.md#m06-u04--validate-changes-with-github-actions)
- Verified source: https://learn.microsoft.com/en-us/training/modules/trigger-azure-machine-learn-jobs-github-actions/4-use-for-model-training (fetched 2026-11-13).
- Participation: declined.
- Context: offered Short quiz, Full quiz, or Skip quiz at lesson closure; learner selected “Skip quiz.” This is a session-specific decline, not a blanket preference.
- Requested/planned: not applicable; no quiz selected.
- Presented / valid answered: 0 / 0.
- Count scope: this single-module session only.
- Evidence provenance: current-session selection returned by the question tool. No quiz questions were presented; no item records or score apply. The two ordinary conceptual checks are separate and are retained in the memory session.
