# Quizzes — Experiment with Azure Machine Learning

- Module ID: M02
- Notes: [Lesson notes](notes.md)
- Source: https://learn.microsoft.com/en-us/training/modules/experiment-azure-machine-learning/
- Evidence identity: session ID plus question ID; one optional quiz per session, Q01–Q10 unique within that session. Resume/retry preserves IDs and initial answers.

Tutor-created formative checks, not official Microsoft assessments. Scores alone do not establish mastery or practical execution.

## Quiz history

<a name="quiz-2026-10-29-session-05"></a>

### Optional tutor quiz — 2026-10-29-session-05

- Date: 2026-10-29
- Units: [M02-U01 — Introduction](notes.md#m02-u01--introduction)
- Verified source (S1 for all items): https://learn.microsoft.com/en-us/training/modules/experiment-azure-machine-learning/1-introduction — fetched 2026-10-29.
- Participation: completed
- Requested/planned: Short quiz (up to 5); 3 planned, avoiding padding a narrow introduction.
- Presented / valid answered: 3 / 3
- Correct / incorrect / skipped / invalid / unasked or unanswered: 3 / 0 / 0 / 0 / 0
- Score: 3/3
- Difficulty mix and scoring: 1 easy, 2 medium; single-answer match for Q01–Q02, exact-set scoring for Q03.
- Count scope: this module only; identical to session-wide totals.
- Evidence provenance: current-conversation learner selections returned by the question tool; tutor-authored questions and feedback grounded in S1. No historical backfill or practical execution.

<a name="quiz-2026-10-29-session-05-q01"></a>

#### Q01 — Automated exploration; easy; single-answer; M02-U01; S1

Prompt: You want Azure Machine Learning to explore different algorithms and preprocessing configurations automatically. Which tool is intended for that job? Select one answer.
- A. MLflow — Experiment tracking.
- B. AutoML — Automated machine learning.
- C. Jupyter notebooks — Interactive coding.

Initial learner selections: B. AutoML
Correct set: {B}
Outcome: correct
Explanation: AutoML automates exploration of algorithms and preprocessing configurations. MLflow tracks runs; notebooks provide an interactive coding environment rather than automatically performing that search. Source: S1.
Follow-up: none.

<a name="quiz-2026-10-29-session-05-q02"></a>

#### Q02 — Tracking custom runs; medium; single-answer; M02-U01; S1

Prompt: You have written custom training code in a notebook and plan to change it across several runs. Which approach matches the introduction's workflow for keeping those runs comparable? Select one answer.
- A. Use MLflow to track the notebook runs — Keep experiment records for comparison.
- B. Use the notebook without experiment tracking — Compare only what you remember from each run.
- C. Replace tracking with AutoML's search — Run an automated search instead of recording the custom runs.

Initial learner selections: A. Use MLflow to track the notebook runs
Correct set: {A}
Outcome: correct
Explanation: MLflow tracks custom runs so results can be compared. Relying on memory does not provide those records; an AutoML search is not a substitute for tracking the custom runs. Source: S1.
Follow-up: none.

<a name="quiz-2026-10-29-session-05-q03"></a>

#### Q03 — Model comparison; medium; multiple-answer; M02-U01; S1

Prompt: Your AutoML and notebook experiments have produced several trained models. Which two comparison approaches does the introduction identify for selecting a model? Select two answers.
- A. Prefer whichever model trained last — Use run order as the selection criterion.
- B. Compare performance metrics — Examine measured model performance.
- C. Prefer notebook models automatically — Use the authoring tool as the selection criterion.
- D. Use the Responsible AI dashboard — Include the dashboard in model evaluation.

Initial learner selections: B. Compare performance metrics; D. Use the Responsible AI dashboard
Correct set: {B, D}
Outcome: correct (exact set)
Explanation: S1 identifies performance metrics and the Responsible AI dashboard for comparing trained models. Training order and notebook authorship alone do not justify selection. Source: S1.
Follow-up: none.

Strengths: identified automatic exploration, custom-run tracking, and the introduction's two model-comparison approaches.
Misconceptions and remaining gaps: no incorrect quiz answers. Ordinary lesson checks raised a notebook-size limitation and an assumed transition of custom preprocessing into AutoML; tutor clarified both. Their independent retention is not demonstrated by this quiz; detailed checks are retained in the memory session. Supported preprocessing configuration and practical execution remain future study, not quiz failures.
Review proposal: M02-U01 tool roles and notebook/custom-preprocessing distinction on 2026-11-01; use a fresh brief application check to distinguish custom control from automated search. This is separate from completion.

<a name="quiz-2026-10-29-session-06"></a>

### Optional tutor quiz — 2026-10-29-session-06

- Date: 2026-10-29
- Units: [M02-U02 — Preprocess data and configure featurization](notes.md#m02-u02--preprocess-data-and-configure-featurization)
- Verified source (S2 for all items): https://learn.microsoft.com/en-us/training/modules/experiment-azure-machine-learning/2-preprocess-data-configure-featurization — fetched 2026-10-29. Tutor clarifications on identifier usefulness and the scaling/featurization distinction supplement this source.
- Participation: completed
- Requested/planned: Full quiz (up to 10); 8 planned for this focused unit, avoiding repetition.
- Presented / valid answered: 8 / 8
- Correct / incorrect / skipped / invalid / unasked or unanswered: 7 / 1 / 0 / 0 / 0
- Score: 7/8
- Difficulty mix and scoring: 2 easy, 4 medium, 2 hard; single-answer match except Q03 and Q08, which use exact-set scoring.
- Count scope: this module only; identical to session-wide totals.
- Evidence provenance: current-conversation learner selections returned by the question tool. Tutor-authored formative questions and feedback; no official assessment or practical execution.

<a name="quiz-2026-10-29-session-06-q01"></a>

#### Q01 — MLTable purpose; easy; single-answer; M02-U02; S2

Prompt: In the studied AutoML workflow, why use an MLTable data asset? Select one answer.
- A. To guarantee all missing values are filled — Data-cleaning guarantee.
- B. To describe how AutoML reads the tabular data — Data-loading definition.
- C. To select the best training algorithm — Algorithm-selection decision.
- D. To store only model evaluation results — Evaluation-output storage.

Initial learner selections: B. To describe how AutoML reads the tabular data
Correct set: {B}
Outcome: correct
Explanation: MLTable describes reading the data; it does not guarantee imputation (A), choose an algorithm (C), or serve only as evaluation-output storage (D). Source: S2.
Follow-up: none.

<a name="quiz-2026-10-29-session-06-q02"></a>

#### Q02 — Missing ages; medium; single-answer; M02-U02; S2

Prompt: A training column contains missing ages. You want to retain those rows and supply replacement age values. Which transformation directly addresses this problem? Select one answer.
- A. Categorical encoding — Represent categories numerically.
- B. Date-part extraction — Derive features from dates.
- C. Numeric scaling — Adjust numeric magnitudes.
- D. Missing-value imputation — Supply values for empty entries.

Initial learner selections: D. Missing-value imputation
Correct set: {D}
Outcome: correct
Explanation: Imputation supplies missing values. A represents categories, B derives date features, and C adjusts magnitudes rather than filling empty entries. Source: S2.
Follow-up: none.

<a name="quiz-2026-10-29-session-06-q03"></a>

#### Q03 — Categories and dates; medium; multiple-answer; M02-U02; S2

Prompt: Your data contains city names and signup timestamps. Which TWO transformation-to-purpose mappings are appropriate? Select two answers.
- A. Encode city names as numeric indicators — Transformation for the city column.
- B. Normalize timestamps to fill missing cities — Transformation across the two columns.
- C. Extract month from signup timestamps — Transformation for the timestamp column.
- D. Impute city names to create an income scale — Transformation linking city and income.

Initial learner selections: A. Encode city names as numeric indicators; C. Extract month from signup timestamps
Correct set: {A, C}
Outcome: correct (exact set)
Explanation: A encodes categories and C derives date features. Timestamp normalization does not fill missing cities (B), and city imputation does not scale income (D). Source: S2.
Follow-up: none.

<a name="quiz-2026-10-29-session-06-q04"></a>

#### Q04 — Scaling purpose; easy; single-answer; M02-U02; S2

Prompt: Why does the unit say AutoML automatically applies scaling and normalization to numeric data? Select one answer.
- A. To assign every feature equal predictive importance — Equalize importance.
- B. To convert all numeric columns into categories — Change the feature type.
- C. To prevent large-scale features from dominating training — Address differences in numeric magnitude.
- D. To remove every outlier from the dataset — Guarantee outlier removal.

Initial learner selections: C. To prevent large-scale features from dominating training
Correct set: {C}
Outcome: correct
Explanation: Scaling addresses numeric magnitude differences, not equal predictive importance (A), universal categorical conversion (B), or guaranteed outlier removal (D). Source: S2.
Follow-up: none.

<a name="quiz-2026-10-29-session-06-q05"></a>

#### Q05 — Identifier usefulness; medium; single-answer; M02-U02; S2

Prompt: A customer ID has a distinct value for almost every record. Which is the best interpretation of the unit's high-cardinality feature guidance? Select one answer.
- A. Every feature with many distinct values must be removed — Apply a universal removal rule.
- B. An identifier-like feature is a candidate for dropping — Evaluate its meaning and usefulness.
- C. Unique IDs guarantee better predictions for new customers — Assume uniqueness improves generalization.
- D. Scaling IDs resolves their lack of predictive meaning — Use numeric magnitude adjustment.

Initial learner selections: C. Unique IDs guarantee better predictions for new customers
Correct set: {B}
Outcome: incorrect
Explanation: The source lists record IDs as candidates for dropping. Tutor clarification: uniqueness identifies records but does not guarantee generalizable predictions (C). High cardinality is not a universal removal rule (A), and scaling cannot create predictive meaning (D). Source: S2 and studied tutor explanation.
Follow-up: tutor explained the distinction; no learner retry or independent post-feedback recovery was observed.

<a name="quiz-2026-10-29-session-06-q06"></a>

#### Q06 — Custom imputation; hard; single-answer; M02-U02; S2

Prompt: You want AutoML's integrated featurization, but a specific feature needs a particular imputation method. What does the studied unit support? Select one answer.
- A. Disable all featurization because customization is unsupported — Turn off integrated transformations.
- B. Register the data again to force the desired method — Use data registration as the control.
- C. Accept the default because column-specific choices are impossible — Leave every setting unchanged.
- D. Customize featurization for the specific feature — Specify its imputation method.

Initial learner selections: D. Customize featurization for the specific feature
Correct set: {D}
Outcome: correct
Explanation: S2 explicitly supports a feature-specific imputation method. Disabling everything is unnecessary (A); registration is not the control (B); column-specific choices are possible, contrary to C.
Follow-up: none.

<a name="quiz-2026-10-29-session-06-q07"></a>

#### Q07 — Separate scaling and featurization; hard; single-answer; M02-U02; S2

Prompt: A teammate disables optional featurization and concludes: 'That also disables all automatic numeric scaling and normalization.' Based on the distinction taught in this unit, what is the best response? Select one answer.
- A. The conclusion confuses optional featurization with automatic numeric scaling — Keep the two behaviors distinct.
- B. The conclusion is correct because the two terms are identical — Treat both as the same control.
- C. The conclusion is correct because scaling only happens with custom imputation — Make scaling depend on imputation customization.
- D. The conclusion is correct because MLTable registration replaces scaling — Treat registration as a scaling substitute.

Initial learner selections: A. The conclusion confuses optional featurization with automatic numeric scaling
Correct set: {A}
Outcome: correct
Explanation: S2 presents automatic scaling separately from optional featurization; the studied tutor clarification preserves this distinction. The terms are not identical controls (B), scaling does not depend on custom imputation (C), and registration is not a scaling substitute (D).
Follow-up: none.

<a name="quiz-2026-10-29-session-06-q08"></a>

#### Q08 — Post-experiment inspection; medium; multiple-answer; M02-U02; S2

Prompt: After the AutoML experiment finishes, which TWO things does this unit say you can inspect or receive? Select two answers.
- A. A guarantee that the data has no quality problems — Assurance about all data issues.
- B. The scaling and normalization methods applied — Transformation details.
- C. Notifications about issues such as missing values or class imbalance — Detected data issues.
- D. Proof that every imputed value matches the unknown original — Certainty about replacement values.

Initial learner selections: B. The scaling and normalization methods applied; C. Notifications about issues such as missing values or class imbalance
Correct set: {B, C}
Outcome: correct (exact set)
Explanation: S2 supports inspection of applied methods and data-issue notifications (B, C), not a guarantee of problem-free data (A) or certainty about unknown original values (D).
Follow-up: none.

Strengths: distinguished MLTable loading, imputation, scaling purpose, categorical/date transformations, feature-specific imputation configuration, separate scaling/featurization behavior, and post-experiment inspection.
Misconceptions and remaining gaps: [Q05](#quiz-2026-10-29-session-06-q05) exposed an assumption that unique IDs guarantee better predictions. Tutor feedback was supplied, but independent retention remains unverified. Ordinary lesson checks initially conflated missing-age handling with normalization; subsequent explanation and an actual imputation answer showed scaffolded recovery. No practical configuration or execution was attempted.
Review proposal: M02-U02 high-cardinality identifier usefulness on 2026-10-30; a fresh scenario should distinguish identifying a row from a feature that generalizes. Completion and review state are separate.

<a name="quiz-2026-10-29-session-07"></a>

### Optional tutor quiz — 2026-10-29-session-07

- Date: 2026-10-29
- Units: [M02-U03 — Run an automated machine learning experiment](notes.md#m02-u03--run-an-automated-machine-learning-experiment)
- Verified source (S3 for every item): https://learn.microsoft.com/en-us/training/modules/experiment-azure-machine-learning/3-run-job — fetched 2026-10-29. Studied tutor task-selection and limits clarifications supplement the source.
- Participation: completed
- Requested/planned: Full quiz, 10 / 10.
- Presented / valid answered: 10 / 10
- Correct / incorrect / skipped / invalid / unasked or unanswered: 9 / 1 / 0 / 0 / 0
- Score: 9/10
- Difficulty mix and scoring: 3 easy, 4 medium, 3 hard. Single-answer match except Q04 and Q08, which require exact sets.
- Count scope: this module only; identical to session-wide counts.
- Evidence provenance: current-conversation learner selections returned by the question tool; tutor-created formative checks and feedback, not an official assessment. No practical execution.

<a name="quiz-2026-10-29-session-07-q01"></a>

#### Q01 — Task selection; easy; single-answer; M02-U03; S3

Prompt: Your inputs are numeric sensor readings, and your target is NeedsMaintenance with values yes/no. Which AutoML task fits? Select one answer.
- A. Regression — Predict a numeric quantity.
- B. Classification — Predict a category.
- C. Forecasting — Predict future values of a time series.

Initial learner selections: B. Classification
Correct set: {B}
Outcome: correct
Explanation: A categorical target requires classification. Regression predicts a quantity; forecasting concerns future time-series values. Numeric inputs do not determine the task. Source: S3 and studied tutor clarification.
Follow-up: none.

<a name="quiz-2026-10-29-session-07-q02"></a>

#### Q02 — Policy restrictions; medium; single-answer; M02-U03; S3

Prompt: A policy prohibits one classification algorithm but permits the other candidates. How should you configure AutoML while preserving its ability to explore alternatives? Select one answer.
- A. Change the task to regression — Use the regression candidate algorithms instead.
- B. Set max_trials to 1 — Limit the search to a single trial.
- C. Block the prohibited algorithm — Keep the permitted classification candidates available.
- D. Change the target column — Train against a different column.

Initial learner selections: C. Block the prohibited algorithm
Correct set: {C}
Outcome: correct
Explanation: Blocking enforces the restriction while preserving permitted candidates. Changing task or target changes the prediction problem; a one-trial limit does not exclude the prohibited algorithm. Source: S3.
Follow-up: none.

<a name="quiz-2026-10-29-session-07-q03"></a>

#### Q03 — Ranking metric; easy; single-answer; M02-U03; S3

Prompt: Which setting tells AutoML how to rank trained models and select its best candidate? Select one answer.
- A. experiment_name — The experiment's name.
- B. compute — The training compute target.
- C. target_column_name — The column to predict.
- D. primary_metric — The metric used for candidate ranking.

Initial learner selections: D. primary_metric
Correct set: {D}
Outcome: correct
Explanation: primary_metric controls ranking; the others identify the experiment, compute, and prediction target respectively. Source: S3.
Follow-up: none.

<a name="quiz-2026-10-29-session-07-q04"></a>

#### Q04 — Trial count and duration; medium; multiple-answer; M02-U03; S3

Prompt: You want at most 12 trials, with each individual trial limited to 10 minutes. Which two settings express those requirements? Select two answers.
- A. max_trials=12 — Set the candidate-trial count limit.
- B. timeout_minutes=10 — Set the overall experiment time limit.
- C. trial_timeout_minutes=10 — Set the individual trial time limit.
- D. max_concurrent_trials=12 — Set the parallel-trial limit.

Initial learner selections: A. max_trials=12; B. timeout_minutes=10
Correct set: {A, C}
Outcome: incorrect (exact-set scoring)
Explanation: A limits total trials and C limits each trial's duration. B instead limits the whole experiment; D limits simultaneous trials. The initial answer incorrectly selected B and omitted C. Source: S3.
Follow-up: tutor explained overall versus individual timeout; no direct retry was requested or observed. Q10 subsequently applied upper-limit semantics and retained the separate time limits, but is not a fresh equivalent configuration check.

<a name="quiz-2026-10-29-session-07-q05"></a>

#### Q05 — Total trials versus concurrency; hard; single-answer; M02-U03; S3

Prompt: An AutoML job has max_trials=12 and max_concurrent_trials=3. Assuming sufficient compute is available, what do those settings allow? Select one answer.
- A. At most 3 trials in total — The concurrency value replaces the total-trial limit.
- B. Up to 12 trials, at most 3 at once — Total search size and simultaneous execution have separate limits.
- C. All 12 trials must run at once — The total-trial value determines simultaneous execution.
- D. Exactly 36 trials in total — Multiply total trials by concurrency.

Initial learner selections: B. Up to 12 trials, at most 3 at once
Correct set: {B}
Outcome: correct
Explanation: Total and simultaneous trial limits are separate. Neither value replaces the other or multiplies the total; all trials need not run at once. Source: S3.
Follow-up: none.

<a name="quiz-2026-10-29-session-07-q06"></a>

#### Q06 — Training input; easy; single-answer; M02-U03; S3

Prompt: In this Microsoft Learn AutoML workflow, what kind of data input is required for training_data? Select one answer.
- A. An MLflow model artifact — A previously packaged trained model.
- B. A studio monitoring URL — A link to a job page.
- C. An MLTable data input — A reference to the table data used for training.

Initial learner selections: C. An MLTable data input
Correct set: {C}
Outcome: correct
Explanation: The source requires an MLTable input; neither a trained-model artifact nor a monitoring URL supplies the training table. Source: S3.
Follow-up: none.

<a name="quiz-2026-10-29-session-07-q07"></a>

#### Q07 — Missing submission; hard; single-answer; M02-U03; S3

Prompt: Your script successfully creates classification_job and calls classification_job.set_limits(...), then exits. No training job was submitted. What operation is missing? Select one answer.
- A. ml_client.jobs.create_or_update(classification_job) — Submit the configured job to the workspace.
- B. print(classification_job) — Display the local job configuration.
- C. Change experiment_name — Give the configuration another experiment name.
- D. Set enable_model_explainability=False — Disable model explainability in the configuration.

Initial learner selections: A. ml_client.jobs.create_or_update(classification_job)
Correct set: {A}
Outcome: correct
Explanation: A submits the job. Displaying or changing the configuration, including explainability, does not submit it. Source: S3.
Follow-up: none.

<a name="quiz-2026-10-29-session-07-q08"></a>

#### Q08 — Monitoring after submission; medium; multiple-answer; M02-U03; S3

Prompt: After returned_job = ml_client.jobs.create_or_update(classification_job) succeeds, which two statements fit the workflow shown in Microsoft Learn? Select two answers.
- A. The best model is necessarily finished — Submission guarantees all training has completed.
- B. returned_job.studio_url provides a monitoring link — Use the returned job's URL to open its studio page.
- C. Training can be monitored in Azure ML studio — Inspect the submitted job's progress in the studio.
- D. Printing the URL starts the trials — Training begins only when the URL is printed.

Initial learner selections: B. returned_job.studio_url provides a monitoring link; C. Training can be monitored in Azure ML studio
Correct set: {B, C}
Outcome: correct (exact set)
Explanation: B and C describe studio monitoring. Submission need not mean completed training, and printing a URL is not submission. Source: S3 and studied workflow clarification.
Follow-up: none.

<a name="quiz-2026-10-29-session-07-q09"></a>

#### Q09 — Early termination; medium; single-answer; M02-U03; S3

Prompt: You want AutoML to be allowed to end the experiment when its score is not improving in the short term. Which setting expresses that choice? Select one answer.
- A. enable_model_explainability=True — Enable model explainability.
- B. n_cross_validations=5 — Use five cross-validation folds.
- C. max_concurrent_trials=1 — Limit simultaneous trials to one.
- D. enable_early_termination=True — Allow stopping based on lack of score improvement.

Initial learner selections: D. enable_early_termination=True
Correct set: {D}
Outcome: correct
Explanation: D allows early termination for lack of score improvement. Explainability, validation folds, and concurrency control other aspects. Source: S3.
Follow-up: none.

<a name="quiz-2026-10-29-session-07-q10"></a>

#### Q10 — Limit semantics; hard; single-answer; M02-U03; S3

Prompt: Your job sets timeout_minutes=60, trial_timeout_minutes=20, and max_trials=5. A colleague says this guarantees five completed trials and exactly 60 minutes of training. Which interpretation is correct? Select one answer.
- A. Five trials must finish, regardless of time limits — The trial count overrides both time limits.
- B. These are upper limits, not completion guarantees — The experiment may stop before five trials finish or before 60 minutes elapse.
- C. Each trial is allowed 60 minutes — The overall timeout becomes the individual trial timeout.
- D. The overall experiment is limited to 20 minutes — The individual trial timeout replaces the overall timeout.

Initial learner selections: B. These are upper limits, not completion guarantees
Correct set: {B}
Outcome: correct
Explanation: Limits bound search size and duration rather than guaranteeing completed trials or exact duration. Overall and individual timeouts remain separate; neither overrides the other. Source: S3 and studied tutor interpretation.
Follow-up: none.

Strengths: task selection, policy-based algorithm restrictions, ranking criterion, concurrency versus total trials, MLTable input, submission, monitoring, early termination, and upper-limit semantics.
Misconceptions and remaining gaps: [Q04](#quiz-2026-10-29-session-07-q04) confused the whole-experiment timeout with the individual-trial timeout despite a correct ordinary lesson configuration answer. Tutor feedback was supplied; independent retention on a fresh equivalent configuration remains unverified. No practical execution was attempted. Initial lesson algorithm-selection confusion was followed by a supported blocking answer and a correct Q02 application.
Review proposal: M02-U03 overall versus individual timeout on 2026-10-30; use a fresh configuration task distinguishing total duration, per-trial duration, trial count, and concurrency. Keep review separate from completion.
