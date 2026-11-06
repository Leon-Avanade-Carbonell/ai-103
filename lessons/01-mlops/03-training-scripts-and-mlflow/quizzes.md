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

<a name="quiz-2026-11-05-session-01"></a>

### Optional tutor quiz — 2026-11-05-session-01

- Date: 2026-11-05
- Units: [M03-U02 — Convert a notebook to a script](notes.md#m03-u02--convert-a-notebook-to-a-script)
- Verified source (S2): https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/2-convert-notebook-script — fetched 2026-11-05. Error/state examples and action boundaries are taught tutor clarifications supporting the source's terminal-testing recommendation.
- Participation: completed
- Requested/planned: Short quiz (up to 5); 4 planned for this unit's scope.
- Presented / valid answered: 4 / 4
- Correct / incorrect / skipped / invalid / unasked or unanswered: 3 / 1 / 0 / 0 / 0
- Score: 3/4
- Difficulty mix and scoring: 1 easy, 2 medium, 1 hard; multiple-answer items require an exact-set match.
- Count scope: this module only; also the session-wide totals.
- Evidence provenance: current conversation; initial selections returned by the question tool. No practical execution or official assessment outcome.

<a name="quiz-2026-11-05-session-01-q01"></a>

#### Q01 — Remove nonessential code; easy; single-answer; M03-U02; S2

Prompt: Question 1/4 — Easy. Select one answer. When converting an exploratory notebook into an automated training script, which code should you remove?
- A. All print statements — Remove output regardless of its operational purpose.
- B. Unused exploratory previews — Remove data previews that nobody uses in the automated workflow.
- C. All preprocessing steps — Leave data preparation out of the training script.
- D. All imports — Rely on packages already imported in the notebook.

Initial learner selections: B. Unused exploratory previews (set {B}).
Correct set: {B}
Outcome: correct
Explanation: Remove exploration without an ongoing purpose. Useful logging can stay (A); required preprocessing and imports must remain (C, D). Source: S2, with tutor standalone-script clarification.
Follow-up: None.

<a name="quiz-2026-11-05-session-01-q02"></a>

#### Q02 — Function benefits; medium; multiple-answer; M03-U02; S2

Prompt: Question 2/4 — Medium. Select two answers. What are benefits of splitting data loading and data preparation into separate small functions?
- A. Easier maintenance — Each function has a focused responsibility.
- B. Guaranteed model accuracy — Function boundaries ensure the model meets its quality target.
- C. Automatic recurring execution — Functions arrange nightly runs without another trigger.
- D. Isolated testing — Preparation can be tested without loading a file or training a model.

Initial learner selections: A. Easier maintenance (set {A}); only one option selected.
Correct set: {A, D}
Outcome: incorrect
Explanation: A and D are benefits named or illustrated by the source. D was omitted; exact-set scoring gives no partial credit. Functions neither guarantee accuracy (B) nor supply recurring automation (C). Source: S2 and taught tutor action-boundary clarification.
Follow-up: Tutor explained isolated testing; no learner retry was supplied.

<a name="quiz-2026-11-05-session-01-q03"></a>

#### Q03 — Terminal execution; medium; single-answer; M03-U02; S2

Prompt: Question 3/4 — Medium. Select one answer. You run `python train.py` in an Azure Machine Learning compute instance terminal. What does this action do?
- A. Creates a nightly schedule — The script will run again automatically every night.
- B. Submits a managed command job — A configured Azure ML command job is created automatically.
- C. Runs the script directly — The current process executes it and shows output or errors in the terminal.
- D. Registers the trained model — Any model produced is automatically added to the model registry.

Initial learner selections: C. Runs the script directly (set {C}).
Correct set: {C}
Outcome: correct
Explanation: The source describes direct execution and visible output/errors. This action alone does not establish scheduling, job submission, or model registration (A, B, D). Source: S2 with taught tutor action-boundary clarification.
Follow-up: None.

<a name="quiz-2026-11-05-session-01-q04"></a>

#### Q04 — Hidden notebook state; hard; single-answer; M03-U02; S2

Prompt: Question 4/4 — Hard. Select one answer. A notebook cell using `df` works because an earlier cell created it. The exported script omits that creation step and raises `NameError: name 'df' is not defined` in a fresh terminal process. What is the best fix?
- A. Initialize df in the script — Add the required data-loading step before df is used.
- B. Remove the target column — Delete the label column from the input CSV.
- C. Increase the compute size — Provide more memory and CPU cores.
- D. Keep the notebook open — Let the terminal script reuse the notebook's variables.

Initial learner selections: A. Initialize df in the script (set {A}).
Correct set: {A}
Outcome: correct
Explanation: Initialize the variable before use. Removing columns or increasing compute cannot repair an undefined name; a fresh process does not inherit notebook variables. Source: S2 terminal-testing context; this specific troubleshooting scenario is a taught tutor Python clarification, not a quoted source example.
Follow-up: None.

Strengths: Q01 purposeful cleanup; Q03 direct execution; Q04 explicit initialization after lesson scaffolding.
Misconceptions and remaining gaps: Q02 omitted isolated testing, despite a correct scaffolded ordinary-check explanation that in-memory data bypasses loading. Independent fault isolation needs reinforcement. No code was run.
Review proposals: M03-U02 function isolation and distinguishing loading/preparation/state failures, 2026-11-06; use a fresh scenario to explain which responsibility is tested and which error belongs to which stage. Completion and review state remain separate.

<a name="quiz-2026-11-05-session-02"></a>

### Optional tutor quiz — 2026-11-05-session-02

- Date: 2026-11-05
- Units: [M03-U03 — Run a script as a command job](notes.md#m03-u03--run-a-script-as-a-command-job)
- Verified source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/3-run-script-command-job — fetched 2026-11-05.
- Participation: declined
- Requested/planned: Not applicable; learner selected Skip quiz.
- Presented / valid answered: 0 / 0
- Count scope: this module only; also the session-wide totals.
- Evidence provenance: current-session response to the optional-quiz question tool. No quiz items were presented, and no score or official assessment outcome is inferred.

Strengths: Ordinary lesson checks demonstrated selecting compute and grouping settings, submission via `create_or_update`, and identifying a separate recurring trigger after a follow-up prompt. Full prompts, initial responses, and feedback belong in the memory session.
Misconceptions and remaining gaps: No demonstrated unresolved conceptual error in these checks; practical SDK authentication, job submission, and execution remain unverified. A decline is not a failed check or a blanket quiz preference.
Review proposals: No new dedicated review proposed from this participation record.

<a name="quiz-2026-11-05-session-03"></a>

### Optional tutor quiz — 2026-11-05-session-03

- Date: 2026-11-05
- Units: [M03-U04 — Use parameters in a command job](notes.md#m03-u04--use-parameters-in-a-command-job)
- Verified source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/4-use-parameters-command-job — fetched 2026-11-05.
- Participation: declined
- Requested/planned: Not applicable; learner selected Skip quiz.
- Presented / valid answered: 0 / 0
- Count scope: this module only; also the session-wide totals.
- Evidence provenance: current-session response to the optional-quiz question tool. No quiz items were presented; no score or official assessment outcome is inferred.

Strengths: Ordinary checks demonstrated switching the filename argument and replacing a hard-coded loading path with the parsed argument. Full prompts, initial responses, feedback, and scaffolding belong in the memory session.
Misconceptions and remaining gaps: The tutor supplied the parsing prerequisite after the first partially answered prompt. The learner then applied the argument-use distinction correctly. No practical execution was verified. Declining this quiz is not a failed check or a blanket preference.
Review proposals: No new dedicated review proposed; naturally revisit parameter use in subsequent MLflow study.

<a name="quiz-2026-11-05-session-04"></a>

### Optional tutor quiz — 2026-11-05-session-04

- Date: 2026-11-05
- Units: [M03-U05 — Track metrics with MLflow](notes.md#m03-u05--track-metrics-with-mlflow)
- Verified source: https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/5-track-metrics — fetched 2026-11-05.
- Participation: declined
- Requested/planned: Not applicable; learner selected Skip quiz.
- Presented / valid answered: 0 / 0
- Count scope: this module only; also the session-wide totals.
- Evidence provenance: current-session response to the optional-quiz question tool. No quiz items were presented; no score or official assessment outcome is inferred.

Strengths: Ordinary application checks demonstrated combining supported autologging with a custom cleaning-time metric and inspecting remote dependencies for an import failure. Full prompts, initial responses, and feedback belong in the memory session.
Misconceptions and remaining gaps: No demonstrated unresolved conceptual error in the checks. Parameter/artifact distinctions were taught but not independently checked. Practical timing, logging, environment registration, and remote execution remain unverified. A decline is not a failed check or a blanket preference.
Review proposals: No new dedicated review proposed; naturally revisit logging categories when inspecting runs in M03-U06.

<a name="quiz-2026-11-05-session-05"></a>

### Optional tutor quiz — 2026-11-05-session-05

- Date: 2026-11-05
- Units: [M03-U06 — View metrics and evaluate models](notes.md#m03-u06--view-metrics-and-evaluate-models)
- Verified source (S6): https://learn.microsoft.com/en-us/training/modules/run-training-scripts-track-models-mlflow/6-view-metrics-evaluate-models — fetched 2026-11-05. Loss-direction and deployment-readiness scenarios use explicitly taught tutor clarifications alongside the source's inspection and query concepts.
- Participation: completed
- Requested/planned: Short quiz (up to 5); 4 planned for this focused unit.
- Presented / valid answered: 4 / 4
- Correct / incorrect / skipped / invalid / unasked or unanswered: 3 / 1 / 0 / 0 / 0
- Score: 3/4
- Difficulty mix and scoring: 1 easy, 2 medium, 1 harder scenario; multiple-answer items require an exact-set match.
- Count scope: this module only; also the session-wide totals.
- Evidence provenance: current-session initial selections returned by the interactive question tool. No execution evidence or official Microsoft assessment outcome.

<a name="quiz-2026-11-05-session-05-q01"></a>

#### Q01 — Parameter inspection; easy; single-answer; M03-U06; S6

Prompt: Question 1/4 — Easy. Select one answer. Where does the source direct you to inspect logged input parameters for a completed run in Azure ML studio?
- A. Metrics — The run’s numeric-result view.
- B. Details → Params — The parameter area within run details.
- C. Images — The run’s logged-plot view.
- D. Outputs + logs → models — The model-output folder.

Initial learner selections: B. Details → Params (set {B}).
Correct set: {B}
Outcome: correct
Explanation: B contains logged parameters; A contains numeric results, C logged plots, and D model output files. Source: S6.
Follow-up: None.

<a name="quiz-2026-11-05-session-05-q02"></a>

#### Q02 — Metric and plot locations; medium; multiple-answer; M03-U06; S6

Prompt: Question 2/4 — Medium. Select two answers. You want to compare a logged training duration and inspect a logged diagnostic plot. Which two locations should you use?
- A. Details → Params for duration — Inspect duration as an input setting.
- B. Outputs + logs → models for the plot — Inspect the model-output folder.
- C. Metrics for duration — Inspect the logged numeric measurement.
- D. Images for the plot — Inspect the logged visualization.

Initial learner selections: C. Metrics for duration, B. Outputs + logs → models for the plot (set {B, C}).
Correct set: {C, D}
Outcome: incorrect
Explanation: C is correct for duration; D is the source's logged-plot view. A is for settings; B holds model files rather than the designated plot view. The initial answer omitted D and selected B; exact-set scoring gives no partial credit. Source: S6.
Follow-up: Tutor explained Images versus the models folder; no learner retry was supplied.

<a name="quiz-2026-11-05-session-05-q03"></a>

#### Q03 — Filter, sort, and limit; medium; single-answer; M03-U06; S6

Prompt: Question 3/4 — Medium. Select one answer. A search uses filter_string="params.num_boost_round='100'", order_by=["start_time DESC"], and max_results=2. What does it return?
- A. Two matching runs with the best quality — Quality determines their order.
- B. Two newly launched training runs — The search starts matching jobs.
- C. At most two oldest matching runs — Earlier start times come first.
- D. At most two newest matching runs — Later start times come first.

Initial learner selections: D. At most two newest matching runs (set {D}).
Correct set: {D}
Outcome: correct
Explanation: The parameter filter selects matching records, descending start time puts newest first, and the limit returns at most two. The query does not rank quality (A), launch training (B), or put oldest first (C). Source: S6.
Follow-up: None.

<a name="quiz-2026-11-05-session-05-q04"></a>

#### Q04 — Quality ranking and deployment boundary; hard; multiple-answer; M03-U06; S6

Prompt: Question 4/4 — Harder scenario. Select two answers. You are comparing eligible completed runs that all logged validation_loss on the same evaluation dataset; lower loss is better. You want the lowest-loss candidates, not the newest runs. Which two decisions are appropriate?
- A. Sort by validation_loss ascending — Put smaller logged loss values first.
- B. Deploy based only on job completion — Treat successful execution as sufficient approval.
- C. Check quality and operational requirements — Evaluate deployment suitability beyond execution success.
- D. Keep descending start-time sorting — Use recency to identify the lowest-loss candidates.

Initial learner selections: A. Sort by validation_loss ascending, C. Check quality and operational requirements (set {A, C}).
Correct set: {A, C}
Outcome: correct
Explanation: A ranks the stated criterion in its appropriate direction; C separates execution from deployment suitability. B overclaims execution success and D ranks recency rather than loss. Source: S6 query context, with taught tutor loss-direction and deployment-boundary clarifications.
Follow-up: None.

Strengths: Q01 and Q03 independently identified parameter inspection and recency ordering. Q04 applied ascending-loss ranking and the deployment boundary after lesson feedback.
Misconceptions and remaining gaps: Q02 confused the plot view with the model-output folder. No post-feedback learner retry confirmed recovery. Practical workspace access and query execution remain unverified.
Review proposals: M03-U06 Images versus model-output locations, 2026-11-06; use a short fresh artifact-location scenario. Sorting syntax and direction were tutor-supplied during ordinary checks; the subsequent quiz confirmed conceptual application rather than independently written query code.
