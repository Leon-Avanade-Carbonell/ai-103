# Quizzes — Get started with machine learning in Azure

- Module ID: M01
- Source: https://learn.microsoft.com/en-us/training/modules/design-machine-learning-model-training-solution/
- Notes: [Lesson notes](notes.md)
- Evidence identity: session ID plus question ID; one optional quiz per session, with Q01–Q10 unique within that session. Session/item links use explicit `quiz-<session-ID>[-qNN]` anchors; existing heading links are retained.

These are tutor-created formative quizzes, not official Microsoft assessments. Original records were moved from notes.md without changing learner responses, scores, or progress.

## Quiz history

<a name="quiz-2026-10-29-session-04"></a>

### Optional tutor quiz — 2026-10-29-session-04

- Date: 2026-10-29.
- Units: [M01-U06 — Integrate a model](notes.md#m01-u06--integrate-a-model).
- Verified source S for every item: https://learn.microsoft.com/en-us/training/modules/design-machine-learning-model-training-solution/4-decide-between-compute-options (fetched again 2026-10-29). Questions apply its trained-model scoring, timing, and compute principles to tutor-created scenarios.
- Participation: completed. Requested: Short quiz (up to 5); planned 3 for the focused follow-up scope, announced before delivery.
- Presented / valid answered: 3 / 3.
- Correct / incorrect / skipped / invalid / unasked or unanswered: 3 / 0 / 0 / 0 / 0.
- Score: 3/3. Count scope: this module only, also the complete session quiz.
- Difficulty mix: one easy, two medium. Q03 multiple-answer with exact-set scoring; Q01/Q02 single-answer.
- Evidence provenance: actual current-conversation initial question-tool selections after ordinary follow-up explanations/checks. No quiz retries, code, compute, or endpoint execution. This is new review activity after closed session-03, not a replacement of its initial responses or score. Tutor-created checks, not an official Microsoft assessment or delayed-retention evidence.

<a name="quiz-2026-10-29-session-04-q01"></a>

#### Q01 — Training recognition; easy; single-answer; M01-U06; source S

Prompt: Question 1/3 — Easy. Select one answer. A job reads labeled historical examples, learns new model parameters, and saves a new model version. What operation is it performing?
- A. Training — Learn a model from examples.
- B. Batch scoring — Apply a saved model to collected inputs.
- C. Real-time scoring — Apply a saved model in response to immediate prediction requests.

Initial learner selection: A. Correct set: A. Outcome: correct.
Explanation: A learns parameters and saves the learned model. B and C instead use an already-trained model for predictions, with different timing patterns.
Follow-up: none.

<a name="quiz-2026-10-29-session-04-q02"></a>

#### Q02 — Ready prediction compute; medium; single-answer; M01-U06; source S

Prompt: Question 2/3 — Medium. Select one answer. A support application must return predictions immediately whenever an agent requests them during business hours. Its training job has finished. What should the deployment plan account for?
- A. Wait for the next training run — Handle prediction requests only while the model is being retrained.
- B. Run one batch after closing — Return all requested predictions after business hours.
- C. Provide ready serving compute — Plan execution capacity available for quick responses during business hours.

Initial learner selection: C. Correct set: C. Outcome: correct.
Explanation: C satisfies immediate-response availability. A unnecessarily ties serving to retraining; B delays outputs beyond the requirement.
Follow-up: none.

<a name="quiz-2026-10-29-session-04-q03"></a>

#### Q03 — Batch scoring and idle cluster scaling; medium; multiple-answer; M01-U06; source S

Prompt: Question 3/3 — Medium. Select two answers. A nightly job loads an unchanged saved model, predicts demand for a collected table of stores, and saves the results for a morning report. No other work uses its cluster between nightly jobs. Which TWO statements are correct?
- A. This job retrains the model — Processing a table of stores means it learns new model parameters.
- B. This job performs batch scoring — It applies the saved model to collected inputs and saves predictions.
- C. The cluster must stay at peak size — Saved report predictions require every cluster node to keep running all day.
- D. Idle nodes can scale to zero — After scoring finishes, the cluster can release idle nodes until the next job.

Initial learner selections: B, D. Correct set: B, D. Outcome: correct (exact-set).
Explanation: B describes applying the saved model, and D releases idle capacity after predictions are saved. A falsely implies learning parameters; C falsely requires continued scoring-node execution to retain saved predictions.
Follow-up: none.

Strengths: training recognition (Q01), availability-driven serving compute (Q02), and batch scoring with idle scaling (Q03). Ordinary checks included a recurring use of “training job” for a batch-scoring cluster; tutor correction preceded successful later scoring recognition. These results support same-day recovery, not demonstrated delayed retention or practical deployment.
Remaining gaps: no incorrect quiz answers. Practical deployment and relevant code/configuration examples remain unverified. Keep later retention separate from conceptual completion.
Review proposal: replace the immediate-remediation purpose of the existing U06 review with a retention check on 2026-11-01, using a fresh scenario explaining training versus scoring and ready real-time versus idle batch compute. Memory-agent validates this proposal; preserve the earlier session's original gap and score.

<a name="quiz-2026-10-29-session-03"></a>

### Optional tutor quiz — 2026-10-29-session-03

- Date: 2026-10-29.
- Units: [M01-U06 — Integrate a model](notes.md#m01-u06--integrate-a-model).
- Verified source S for every item: https://learn.microsoft.com/en-us/training/modules/design-machine-learning-model-training-solution/4-decide-between-compute-options (fetched 2026-10-29). Q06 is a tutor-created combined-consumer scenario applying its timing principles.
- Participation: completed. Requested: Full quiz (up to 10); planned 6 for this narrow studied scope, announced before delivery.
- Presented / valid answered: 6 / 6.
- Correct / incorrect / skipped / invalid / unasked or unanswered: 4 / 2 / 0 / 0 / 0.
- Score: 4/6. Count scope: this module only, also the complete session quiz.
- Difficulty mix: two easy, three medium, one hard scenario. Q03 and Q05 multiple-answer with exact-set scoring; other items single-answer.
- Evidence provenance: current-conversation initial selections returned by the question tool. Feedback followed each answer; no retries or practical execution. Tutor-created formative checks, not an official Microsoft assessment.

<a name="quiz-2026-10-29-session-03-q01"></a>

#### Q01 — Endpoint role; easy; single-answer; M01-U06; source S

Prompt: Question 1/6 — Easy. Select one answer. What role does a model endpoint play in the integration pattern described by Microsoft Learn?
- A. Prepare the training dataset — Clean and transform source data.
- B. Let an application request predictions — Provide an address through which the application uses the deployed model.
- C. Select the training algorithm — Compare candidate algorithms during training.

Initial learner selection: B. Correct set: B. Outcome: correct.
Explanation: B exposes prediction access. A is preparation and C training-choice exploration, not endpoint integration.
Follow-up: none.

<a name="quiz-2026-10-29-session-03-q02"></a>

#### Q02 — Batch prediction versus training; easy; single-answer; M01-U06; source S

Prompt: Question 2/6 — Easy. Select one answer. Which operation is batch prediction?
- A. Train using a week of sales — Learn model patterns from historical sales.
- B. Recommend during a page visit — Return recommendations immediately when a shopper selects an item.
- C. Score a collected customer table — Generate each customer's prediction and save the combined results for a later report.

Initial learner selection: A. Correct set: C. Outcome: incorrect.
Explanation: A learns a model, rather than generating batch predictions; B is immediate real-time prediction; C scores collected inputs with an already-trained model and saves results. Feedback clarified that scoring generates predictions, not training. No independent retry occurred.
Follow-up: none.

<a name="quiz-2026-10-29-session-03-q03"></a>

#### Q03 — Prediction availability requirements; medium; multiple-answer; M01-U06; source S

Prompt: Question 3/6 — Medium. Select two answers. A team is choosing a deployment pattern. Which TWO requirements most directly establish when predictions must be available?
- A. How soon results are needed — The allowed delay before the consumer receives predictions.
- B. Which editor developers use — The team's preferred code-editing application.
- C. How often predictions are consumed — The times or frequency at which the application needs results.
- D. What the model file is named — The filename chosen for the trained artifact.

Initial learner selections: A, C. Correct set: A, C. Outcome: correct (exact-set).
Explanation: A and C establish consumer timing; B and D do not establish when predictions are needed.
Follow-up: none.

<a name="quiz-2026-10-29-session-03-q04"></a>

#### Q04 — Serving compute and availability cost; medium; single-answer; M01-U06; source S

Prompt: Question 4/6 — Medium. Select one answer. A model powers an interactive application requiring immediate responses throughout the day, even though requests are infrequent. Which compute-cost consideration fits this requirement?
- A. Training compute also serves requests — No separate prediction compute needs to be considered.
- B. Infrequent requests justify overnight scoring — Delay all predictions until the next scheduled batch.
- C. Prediction compute is unnecessary — The saved model artifact generates results without execution resources.
- D. Ready prediction capacity has a cost — Budget for compute availability needed to respond quickly between infrequent requests.

Initial learner selection: A. Correct set: D. Outcome: incorrect.
Explanation: D budgets for quick-response capacity. A assumes training resources automatically supply serving, instead of planning prediction execution separately; this does not rule out supported infrastructure reuse. B violates immediate response; C omits required execution compute. Feedback supplied the distinction; no independent retry occurred.
Follow-up: none.

<a name="quiz-2026-10-29-session-03-q05"></a>

#### Q05 — Parallel batch processing and idle scaling; medium; multiple-answer; M01-U06; source S

Prompt: Question 5/6 — Medium. Select two answers. A nightly batch-scoring workload uses a compute cluster. Which TWO choices support the batch-processing and idle-cost approach described in the source?
- A. Skip compute for saved models — Generate predictions without running the model on compute.
- B. Process batches across multiple nodes — Use parallel batch processing when appropriate for the workload.
- C. Scale the idle cluster to zero nodes — Configure the cluster to release idle node capacity when no scoring work remains.
- D. Keep peak node capacity all day — Maintain the largest required cluster size even between nightly jobs.

Initial learner selections: C, B (set B, C). Correct set: B, C. Outcome: correct (exact-set).
Explanation: B supports workload processing and C reduces idle node costs. A removes necessary execution compute; D keeps peak capacity unnecessarily between jobs. This post-Q04-feedback recognition does not independently resolve training-versus-serving resource planning.
Follow-up: none.

<a name="quiz-2026-10-29-session-03-q06"></a>

#### Q06 — Two consumers of one sensor stream; hard scenario; single-answer; M01-U06; source S and tutor application

Prompt: Question 6/6 — Hard scenario. Select one answer. A factory uses the same sensor stream for two outputs: an overheating warning needed immediately, and maintenance predictions consumed only in a Monday report. Which integration design best fits both timing requirements?
- A. Batch both outputs on Monday — Generate the warning and maintenance predictions together before the weekly report.
- B. Use separate prediction patterns — Use real-time predictions for warnings and batch predictions for the weekly report.
- C. Retrain whenever a reading arrives — Replace prediction serving with training a model for each new reading.
- D. Require real-time for both outputs — Treat the sensor arrival frequency as requiring immediate generation of every output.

Initial learner selection: B. Correct set: B. Outcome: correct.
Explanation: B meets both consumer timing needs. A delays urgent warnings; C confuses serving and training; D assumes arrival frequency requires immediate prediction for every output. The combined architecture is a tutor illustration, not an executed source lab.
Follow-up: none.

Strengths: endpoint recognition (Q01), timing requirements (Q03), parallel batch/idle scaling (Q05), and separate patterns for separate consumers (Q06).
Remaining gaps: batch scoring versus training (Q02), and prediction compute versus automatic reuse of training resources (Q04). Corrective feedback was supplied, but fresh independent transfer was not checked. Practical endpoint deployment remains unverified.
Review proposal: M01-U06 on 2026-10-30, using a fresh scenario explaining training versus scoring and the compute needed to serve a saved model. Retain existing M01-U02 review separately; no metric quiz was administered here.

<a name="quiz-2026-10-29-session-02"></a>

### Optional tutor quiz — 2026-10-29-session-02

- Date: 2026-10-29.
- Units: [M01-U05 — Use Azure Machine Learning studio](notes.md#m01-u05--use-azure-machine-learning-studio).
- Verified source S for every item: https://learn.microsoft.com/en-us/training/modules/design-machine-learning-model-training-solution/3b-use-automated-machine-learning (fetched 2026-10-29). Q04 also uses the taught synthesis that evaluation precedes deployment approval, consistent with the source's model-results inspection and the earlier training workflow.
- Participation: completed. Requested: Short quiz (up to 5); planned 4 for the studied scope.
- Presented / valid answered: 4 / 4.
- Correct / incorrect / skipped / invalid / unasked or unanswered: 4 / 0 / 0 / 0 / 0.
- Score: 4/4. Count scope: this module only, also the complete session quiz.
- Difficulty mix: two easy, two medium; Q03 multiple-answer, others single-answer. Exact-set scoring for Q03.
- Evidence provenance: actual initial selections returned by the question tool in the current conversation. Feedback followed each answer; no retries or practical execution. Tutor-created formative checks, not an official Microsoft assessment.

<a name="quiz-2026-10-29-session-02-q01"></a>

#### Q01 — Studio recognition; easy; single-answer; M01-U05; source S

Prompt: Question 1/4 — Easy. Select one answer. What is Azure Machine Learning studio?
- A. A browser-based interface — Manage machine learning resources and jobs.
- B. A training compute resource — Execute training code using its CPUs or GPUs.
- C. An Azure subscription — Provide the subscription in which resources are provisioned.

Initial learner selection: A. Correct set: A. Outcome: correct.
Explanation: studio is the browser-based management interface. Compute executes training work; a subscription is where Azure resources are provisioned.
Follow-up: none.

<a name="quiz-2026-10-29-session-02-q02"></a>

#### Q02 — Workspace distinction; easy; single-answer; M01-U05; source S

Prompt: Question 2/4 — Easy. Select one answer. You open Azure Machine Learning studio for the first time. Which statement about a workspace is correct?
- A. The browser tab is the workspace — Opening the interface supplies the required Azure resource.
- B. A workspace is unnecessary — Compute alone replaces the primary Azure ML resource.
- C. Create or access a workspace — The workspace is a separate Azure resource provisioned in a subscription.

Initial learner selection: C. Correct set: C. Outcome: correct.
Explanation: a workspace is a separate Azure resource, not a browser tab. Compute does not replace it. This recognition follows the ordinary lesson's tutor-supplied workspace clarification; it is not an independent practical provisioning check.
Follow-up: none.

<a name="quiz-2026-10-29-session-02-q03"></a>

#### Q03 — Compute selection and monitoring; medium; multiple-answer; M01-U05; source S

Prompt: Question 3/4 — Medium. Select two answers. For a small tabular training dataset, which two decisions follow the compute guidance we studied?
- A. Start with a GPU — Treat GPU compute as mandatory for tabular training.
- B. Start with a CPU — Use a generally sufficient, cost-effective starting option.
- C. Keep the size fixed — Avoid reconsidering resources after training begins.
- D. Monitor time and utilization — Use observed training duration and resource usage to guide adjustments.

Initial learner selections: B, D. Correct set: B, D. Outcome: correct (exact-set).
Explanation: CPU is a sensible starting point and observed time/utilization guide adjustments. GPUs are not mandatory for tabular data, and the initial resource choice need not remain fixed.
Follow-up: none.

<a name="quiz-2026-10-29-session-02-q04"></a>

#### Q04 — AutoML and evaluation; medium; single-answer; M01-U05; source S and taught synthesis

Prompt: Question 4/4 — Medium. Select one answer. Your team has prepared data and wants to explore training choices without writing each experiment. Which approach best fits?
- A. AutoML, then evaluate results — Use automated training experiments and assess the resulting model before deployment approval.
- B. AutoML, then approve immediately — Treat a completed training job as sufficient evidence for deployment.
- C. Deploy without training — Use deployment itself to explore algorithms and train the model.

Initial learner selection: A. Correct set: A. Outcome: correct.
Explanation: AutoML fits the training exploration need, but its results still need evaluation. A completed training job is not deployment approval, and deployment does not replace training. Evaluation-before-approval is the tutor's taught lifecycle synthesis, not a claimed official approval procedure from this unit.
Follow-up: none.

Strengths: studio recognition, post-clarification workspace recognition, CPU/monitoring choices, and AutoML with evaluation before deployment.
Remaining gaps: no incorrect quiz responses; practical provisioning, execution, and delayed retention were not tested. GPU and memory-optimized selection were explained but not independently checked.
Review proposal: M01-U05 on 2026-11-01, using a fresh scenario distinguishing interface/resource/compute and choosing compute with reasons. This is a proposal, not a claim of delayed retention.

<a name="quiz-2026-10-29-session-01"></a>

### Optional tutor quiz — 2026-10-29-session-01

- Date: 2026-10-29.
- Units: [M01-U04 — Train the model](notes.md#m01-u04--train-the-model).
- Verified source S for every item: https://learn.microsoft.com/en-us/training/modules/design-machine-learning-model-training-solution/3-choose-service-train (fetched 2026-10-29).
- Participation: completed. Requested count unspecified; planned 4 for this narrow lesson.
- Presented / valid answered: 4 / 4.
- Correct / incorrect / skipped / invalid / unasked or unanswered: 3 / 1 / 0 / 0 / 0.
- Score: 3/4. Count scope: this module only, also the complete session quiz.
- Difficulty mix: one easy and three medium. Single-answer except Q03; exact-set scoring for multiple answers. No retries or practical execution. Tutor-created formative checks, not an official Microsoft assessment.

<a name="quiz-2026-10-29-session-01-q01"></a>

#### Q01 — Integrated analytics platform; easy; single-answer; M01-U04; source S

Prompt: Which service does Microsoft Learn describe as an integrated analytics platform spanning data preparation, model training, predictions, and Power BI reports? Select one answer.
- A. Azure Databricks — Spark-based data analytics platform.
- B. Microsoft Fabric — An integrated analytics platform.
- C. Foundry Tools — A collection of prebuilt models exposed through APIs.
- D. Azure Machine Learning — A service for managing the machine learning lifecycle.

Initial learner selection: D. Correct set: B. Outcome: incorrect.
Explanation: Fabric is the source-described integrated workflow through Power BI. Azure Machine Learning supports the model lifecycle but is not the platform described by this combination. Databricks emphasizes Spark-based engineering/data science; Foundry Tools offers prebuilt model APIs. Feedback supplied the distinction; no independent retry occurred.

<a name="quiz-2026-10-29-session-01-q02"></a>

#### Q02 — Existing Spark workflow; medium; single-answer; M01-U04; source S

Prompt: A team already uses distributed Spark compute for its data engineering and wants to train models within that platform, with the option to integrate with Azure Machine Learning. Which service most directly matches this setup? Select one answer.
- A. Foundry Tools — Use this service as the training platform.
- B. Microsoft Fabric — Use this service as the training platform.
- C. Azure Databricks — Use this service as the training platform.

Initial learner selection: C. Correct set: C. Outcome: correct.
Explanation: the source explicitly describes Databricks' Spark compute, model training, and Azure Machine Learning integration. Fabric also supports training but does not directly match this stated existing platform; Foundry Tools is not the described Spark platform.

<a name="quiz-2026-10-29-session-01-q03"></a>

#### Q03 — AutoML, pipelines, and access; medium; multiple-answer; M01-U04; source S

Prompt: Which TWO statements accurately describe Azure Machine Learning capabilities in this unit? Select two answers.
- A. Studio is required — Training workloads must be managed through the visual studio interface.
- B. AutoML explores training choices — It runs multiple training jobs with different algorithms and parameters.
- C. Pipelines coordinate processes — They orchestrate steps for processes such as training or inferencing.
- D. Deployment is outside its scope — Trained models must be deployed using a different service.

Initial learner selections: B, C. Correct set: B, C. Outcome: correct (exact-set).
Explanation: B and C describe the source's capabilities. A excludes supported Python SDK/CLI access; D incorrectly excludes model deployment.

<a name="quiz-2026-10-29-session-01-q04"></a>

#### Q04 — Prebuilt model investigation; medium; single-answer; M01-U04; source S

Prompt: A developer needs a common image-analysis feature quickly. A prebuilt model might meet the requirements, and custom training control is not required. What is the most appropriate first step? Select one answer.
- A. Start custom training — Build a new model in Azure Machine Learning before investigating existing models.
- B. Set up Spark compute — Provision Databricks because all image-analysis features require distributed training.
- C. Build a reporting workflow — Choose Fabric primarily to visualize the model's predictions in Power BI.
- D. Investigate Foundry Tools — Check whether a suitable prebuilt model meets the application's requirements.

Initial learner selection: D. Correct set: D. Outcome: correct.
Explanation: investigate the source-described prebuilt model APIs and evaluate suitability. A prematurely assumes custom training; B asserts an unsupported requirement; C prioritizes reporting without a scenario requirement.

Strengths: Databricks/Spark selection (Q02), AutoML versus orchestration and code-first access (Q03), and prebuilt model investigation (Q04).
Remaining gap: Fabric's integrated analytics/Power BI role versus Azure Machine Learning's lifecycle focus (Q01). Feedback was given, but no fresh transfer check occurred.
Review proposal: M01-U04 service selection on 2026-10-30, using a fresh Fabric-versus-Azure-Machine-Learning scenario with an explanation of the deciding workflow requirement.

<a name="quiz-2026-10-28-session-05"></a>

### Optional tutor quiz — 2026-10-28-session-05

- Date: 2026-10-28.
- Units: [M01-U03 — Get and prepare data](notes.md#m01-u03--get-and-prepare-data).
- Source S for every item: https://learn.microsoft.com/en-us/training/modules/design-machine-learning-model-training-solution/2a-prepare-data. The original tutor reported fetching it on 2026-10-28; this repair does not claim a new source fetch.
- Participation: completed. Learner requested “let's proceed with the quiz”; requested count unspecified / planned 5.
- Presented / valid answered: 5 / 5.
- Correct / incorrect / skipped / invalid / unasked or unanswered: 5 / 0 / 0 / 0 / 0.
- Score: 5/5. Count scope: this module only, also the complete session quiz.
- Difficulty mix: two easy and three medium; Q04 multiple-answer, others single-answer. Exact-set scoring for Q04; feedback followed each initial answer, no retries reported. Tutor-created formative quiz, not an official Microsoft assessment.
- Repair provenance (2026-10-29): restored from [the original memory session's tutor-reported handoff](../../../memory/sessions/2026-10-28-session-05.md#optional-lesson-quiz). Before notebook migration, notes corroborated participation, topics and all-correct aggregate outcomes, but not exact choices, keys or selections. Detailed items below retain that handoff attribution. This backfill repairs persistence and navigation; it is not independent corroboration of historical learner responses, new learning, or a progress/review change.

<a name="quiz-2026-10-28-session-05-q01"></a>

#### Q01 — Incoming-format recognition; easy; single-answer; M01-U03; source S

Prompt: An IoT sensor sends temperature readings as JSON objects. What is the format of those incoming readings?
- A. Structured tabular data — Rows and columns in a predefined table.
- B. Semi-structured data — Named fields in JSON objects.
- C. Unstructured image data — Measurements represented as photographs.

Initial learner selection (tutor-reported handoff): B, Semi-structured data. Correct set: B. Outcome: correct.
Explanation: the unit calls IoT JSON semi-structured; A is the training table rather than the incoming readings; C describes images, not JSON. No retry reported.

<a name="quiz-2026-10-28-session-05-q02"></a>

#### Q02 — Mean aggregation and one row; medium; single-answer; M01-U03; source S

Prompt: Machine A reports valid temperatures of 16°C, 20°C, and 24°C during the same minute. Training requires one row per machine per minute containing the average temperature. Which output meets the requirement?
- A. Three rows: 16°C, 20°C, 24°C — Keep each original reading as a separate row.
- B. One row: 24°C — Store highest reading for minute.
- C. One row: 20°C — Store mean of three readings.
- D. One row: 60°C — Store sum of three readings.

Initial learner selection (tutor-reported handoff): C, One row: 20°C. Correct set: C. Outcome: correct.
Explanation: (16+20+24)/3 = 20, with one row; A has the wrong granularity, B the maximum, D the sum. This checks selection of the correct mean and row, not a separately shown calculation process. The numbers are a tutor-created example, not an official source example. No retry reported.

<a name="quiz-2026-10-28-session-05-q03"></a>

#### Q03 — ETL order; medium; single-answer; M01-U03; source S

Prompt: A pipeline extracts sensor readings, converts them into the required training table, and then loads that prepared table into storage. Which processing order is this?
- A. ELT — Extract, load, then transform.
- B. ETL — Extract, transform, then load.
- C. Extract and load only — Move data without transforming it.

Initial learner selection (tutor-reported handoff): B, ETL. Correct set: B. Outcome: correct.
Explanation: transformation precedes loading; A reverses this order and C omits transformation. No retry reported.

<a name="quiz-2026-10-28-session-05-q04"></a>

#### Q04 — Ingestion sequence and triggering; easy; multiple-answer; M01-U03; source S

Prompt: According to the studied Microsoft Learn unit, which TWO statements describe a data ingestion pipeline? Select two answers.
- A. It can run only when started manually — Scheduled execution is not available.
- B. It is a sequence of data movement and transformation tasks — It organizes steps for preparing and serving data.
- C. It replaces the model-training process — Moving data also teaches the model its patterns.
- D. It can be triggered manually or scheduled — Its execution can be on demand or recurring.

Initial learner selections (tutor-reported handoff): D and B, set B, D. Correct set: B, D. Outcome: correct (exact-set).
Explanation: B and D describe pipeline tasks and triggering; A incorrectly excludes scheduling and C confuses data preparation with training. No retry reported.

<a name="quiz-2026-10-28-session-05-q05"></a>

#### Q05 — Prepared-data serving layer; medium; single-answer; M01-U03; source S

Prompt: In the Microsoft Learn unit’s example architecture, Azure Synapse Analytics copies and transforms the source data. Where is the prepared data stored before Azure Machine Learning uses it for training?
- A. Azure Blob Storage — A storage layer holding prepared data.
- B. The original IoT device — Device generated raw measurements.
- C. A model prediction response — Output returned after using a trained model.

Initial learner selection (tutor-reported handoff): A, Azure Blob Storage. Correct set: A. Outcome: correct.
Explanation: A is the prepared-data layer in this example; B is the raw source and C a prediction output, not the training data store. No retry reported.

Strengths: format, mean/row selection, ETL, pipeline sequencing/triggering, and example storage recognition. No new misconceptions or follow-up retries were reported. Same-day recognition does not establish delayed retention or practical execution.
Review proposals: retain the existing M01-U03 aggregation/ETL retention review for 2026-10-31. Historical proposal restored, not a new or resolved review.

<a name="quiz-2026-10-28-session-04"></a>

### Optional tutor quiz — 2026-10-28-session-04

- Date: 2026-10-28.
- Units: [M01-U02 — Define the problem](notes.md#m01-u02--define-the-problem), [M01-U03 — Get and prepare data](notes.md#m01-u03--get-and-prepare-data).
- Sources discussed in the original session: https://learn.microsoft.com/en-us/training/modules/design-machine-learning-model-training-solution/2-identify-tasks ; https://learn.microsoft.com/en-us/azure/machine-learning/how-to-understand-automated-ml?view=azureml-api-2 ; https://learn.microsoft.com/en-us/training/modules/design-machine-learning-model-training-solution/2a-prepare-data. No quiz items were administered.
- Participation: declined for this session. The original summary records the tutor treating the session quiz as skipped after the learner said “Can we stop with the precision/recall quizzes?” This is a topic-specific preference, not a blanket decline of later quizzes.
- Requested/planned: not established in the historical record.
- Presented / valid answered: 0 / 0. Correct / incorrect / skipped / invalid items: 0 / 0 / 0 / 0. Unasked or unanswered count: not established because no planned count was recorded. Count scope: this session only; no item evidence or score.
- Repair provenance (2026-10-29): restored from [the saved session-04 preference and participation record](../../../memory/sessions/2026-10-28-session-04.md#optional-lesson-quiz). Conversational offer/skip recorded; no question-tool offer or skill use is established. This is a persistence repair, not new learner activity, a failed check, or a progress/review change.

<a name="quiz-2026-10-28-session-03"></a>

### Optional tutor quiz — 2026-10-28-session-03

- Related unit: [M01-U02 — Define the problem](notes.md#m01-u02--define-the-problem).
- Participation: completed. Requested Full quiz; planned 10, presented 10, valid answered 10. Difficulty mix: 3 easy, 4 medium, 3 hard application; single/multiple-answer mix. Exact-set scoring for multiple-answer items.
- Correct / incorrect / skipped / invalid / unasked or unanswered: 9 / 1 / 0 / 0 / 0. Score: 9/10. No retries. Tutor-created formative check, not an official Microsoft assessment.
- Every item: M01-U02. Source T: https://learn.microsoft.com/en-us/training/modules/design-machine-learning-model-training-solution/2-identify-tasks . Source E: https://learn.microsoft.com/en-us/azure/machine-learning/how-to-understand-automated-ml?view=azureml-api-2 . Abbreviations below resolve to these verified full URLs. Q09 uses the tutor's generalization/representativeness application of T's split-and-evaluate workflow, not a quoted official farmhouse example.

<a name="quiz-2026-10-28-session-03-q01"></a>

#### Q01 — Algorithm selection (easy, single-answer; source T)

Prompt: In Microsoft Learn’s training workflow, which step selects and configures the algorithm that will learn from the data? Select one answer.
- A. Preprocess data — Normalize and clean the dataset.
- B. Choose model — Select and configure an algorithm.
- C. Score model — Generate predictions on test data.
- D. Evaluate — Calculate performance metrics.

Initial selection: B. Correct set: B. Outcome: correct. Explanation: choosing selects/configures the algorithm; A prepares data, C predicts, D measures performance.

<a name="quiz-2026-10-28-session-03-q02"></a>

#### Q02 — Scoring (easy, single-answer; source T)

Prompt: A trained model receives features for test houses and produces predicted sale prices. Which workflow step is this? Select one answer.
- A. Evaluate — Calculate performance metrics.
- B. Train model — Learn patterns from training examples.
- C. Score model — Generate predictions on test examples.
- D. Load data — Import and inspect the dataset.

Initial selection: C. Correct set: C. Outcome: correct. Explanation: scoring produces predictions; A measures performance, B learns, D imports/inspects.

<a name="quiz-2026-10-28-session-03-q03"></a>

#### Q03 — Categorical output (easy, single-answer; source T)

Prompt: A delivery model must output either “late” or “on time.” Which task matches that requested output? Select one answer.
- A. Regression — Predict a numerical value.
- B. Time-series forecasting — Predict future numerical values from time-series data.
- C. Computer vision — Classify images or detect objects.
- D. Classification — Predict a categorical value.

Initial selection: D. Correct set: D. Outcome: correct. Explanation: requested labels are categories; A predicts amounts, B numerical time-series futures, C concerns images.

<a name="quiz-2026-10-28-session-03-q04"></a>

#### Q04 — Numerical outputs (medium, multiple-answer; source T)

Prompt: Which two requested outputs fit regression rather than classification or time-series forecasting? Select two answers.
- A. Delivery duration in minutes — Estimate duration from distance, traffic, and package features.
- B. Parcel priority category — Assign “standard” or “urgent.”
- C. House sale price in dollars — Estimate price from property features.
- D. Next six monthly sales totals — Forecast the monthly sequence from five years of monthly sales.

Initial selections: A, C. Correct set: A, C. Outcome: correct. Explanation: A/C numerical outputs from features; B categorical, D time-series forecasting.

<a name="quiz-2026-10-28-session-03-q05"></a>

#### Q05 — Mean absolute error (medium, single-answer; source E)

Prompt: For two test houses, actual prices are $200,000 and $300,000. Predictions are $190,000 and $330,000. What is the mean absolute error? Select one answer.
- A. $10,000 — A candidate mean error.
- B. $20,000 — A candidate mean error.
- C. $30,000 — A candidate mean error.
- D. $40,000 — A candidate mean error.

Initial selection: B. Correct set: B. Outcome: correct. Explanation: absolute errors $10,000/$30,000 average to $20,000; A/C individual errors, D sum rather than mean.

<a name="quiz-2026-10-28-session-03-q06"></a>

#### Q06 — Preparation workflow (medium, multiple-answer; source T)

Prompt: Which two actions belong to data preparation steps before choosing and training the model in the workflow studied? Select two answers.
- A. Calculate test-set recall — Measure how many actual positives were detected.
- B. Generate test predictions — Apply the trained model to test examples.
- C. Clean inconsistent data — Preprocess the dataset for consistency.
- D. Separate training and test sets — Split the data for learning and testing.

Initial selections: C, D. Correct set: C, D. Outcome: correct. Explanation: preprocessing/splitting precede choosing/training; A evaluation, B scoring.

<a name="quiz-2026-10-28-session-03-q07"></a>

#### Q07 — Recall denominator (medium, single-answer; source E)

Prompt: There are 12 actual late deliveries. A model flags 20 deliveries as late, of which 9 actually are late. What is its recall for late deliveries? Select one answer.
- A. 75% — 9 divided by 12.
- B. 45% — 9 divided by 20.
- C. 25% — 3 divided by 12.
- D. 60% — 12 divided by 20.

Initial selection: B. Correct set: A. Outcome: incorrect. Explanation: recall 9/12 = 75%; B is precision 9/20 = 45%; C missed share 3/12; D neither. Tutor explicitly identified remaining actual-positive versus predicted-positive denominator confusion. No retry; feedback is not successful learner evidence.

<a name="quiz-2026-10-28-session-03-q08"></a>

#### Q08 — Imbalance and success criterion (hard application, multiple-answer; sources T, E)

Prompt: Of 200 test deliveries, 10 actually arrive late. A model predicts “on time” for every delivery. The company requires at least 80% late-delivery recall. Which two conclusions are correct? Select two answers.
- A. The requirement is met — Overall accuracy exceeds 80%.
- B. Overall accuracy is 95% — 190 of 200 labels are correct.
- C. Late-delivery recall is 95% — Most deliveries are labeled correctly.
- D. The requirement is not met — None of the actual late deliveries is detected.

Initial selections: D, B. Correct set: B, D. Outcome: correct. Explanation: 95% accuracy but 0% late recall; A compares the wrong metric, C confuses accuracy/recall. Confirms metric-specific criterion interpretation; does not resolve Q07's denominator confusion.

<a name="quiz-2026-10-28-session-03-q09"></a>

#### Q09 — Representative evaluation (hard application, single-answer; sources T, E; tutor extension)

Prompt: A price model performs well on held-out city apartments. The team wants to use it for rural farmhouses, which were absent from both training and test data. Which next step best addresses the evidence gap? Select one answer.
- A. Evaluate representative farmhouse data — Collect relevant examples and assess performance for the intended use.
- B. Replace MAE with recall — Change metrics while retaining only apartment data.
- C. Accept the apartment results — Treat holding out apartments as evidence for farmhouse performance.
- D. Reevaluate training apartments — Measure performance on examples used to fit the model.

Initial selection: A. Correct set: A. Outcome: correct. Explanation: representative farmhouse examples assess intended use and may reveal need for training-data improvement; B substitutes a classification metric without addressing coverage, C assumes transfer, D reuses familiar examples. Post-lesson check addresses the learner's earlier different-metrics claim.

<a name="quiz-2026-10-28-session-03-q10"></a>

#### Q10 — Evaluation against acceptance threshold (hard application, single-answer; sources T, E)

Prompt: A team has trained a house-price model and generated predictions on held-out houses. It declares success because the model produced a price for every house. The agreed success criterion is mean absolute error no greater than $15,000. What is still needed to establish whether that criterion is met? Select one answer.
- A. Repeat scoring on the training houses — Generate predictions for familiar examples.
- B. Choose a classification algorithm — Change the task despite the numerical output requirement.
- C. Evaluate against actual test prices — Calculate test MAE and compare it with $15,000.
- D. Count generated predictions — Check that each test house received an output.

Initial selection: C. Correct set: C. Outcome: correct. Explanation: producing predictions is scoring, evaluation must compare test MAE to threshold; A lacks required test evaluation, B changes task unnecessarily, D measures availability rather than quality.

Strengths: workflow recognition, numerical/categorical task selection, independent MAE, imbalance/criterion application, and representative evaluation choice. Remaining gap: Q07 recall versus precision when both counts appear. Proposed review 2026-10-29: a fresh scenario requiring both metrics, explicit denominator explanations, and acceptance decision. Retain existing M01-U01 review 2026-10-31. No official assessment or lab attempted. Conservative next step: brief M01-U02 independent denominator check before M01-U03; do not infer completion from 9/10 alone.

<a name="quiz-2026-10-28-session-02"></a>

### Optional tutor quiz — 2026-10-28-session-02

- Related unit: [M01-U02 — Define the problem](notes.md#m01-u02--define-the-problem).
- Participation: completed. Requested: Full quiz (up to 10); planned 8 to avoid padding this focused lesson. Difficulty mix: 2 easy, 4 medium, 2 hard application; single/multiple-answer mix.
- Presented / valid answered: 8 / 8. Correct / incorrect / skipped / invalid / unasked or unanswered: 6 / 2 / 0 / 0 / 0. Score: 6/8. Exact-set scoring for multiple-answer items. No retries. Tutor-created, not an official Microsoft assessment.
- All questions: M01-U02. Task source (T): https://learn.microsoft.com/en-us/training/modules/design-machine-learning-model-training-solution/2-identify-tasks . Metric source (E): https://learn.microsoft.com/en-us/azure/machine-learning/how-to-understand-automated-ml?view=azureml-api-2 . Each item cites T and/or E below; these abbreviations resolve to those full verified URLs.

<a name="quiz-2026-10-28-session-02-q01"></a>

#### Q01 — Numerical output (easy, single-answer; source T)

Prompt: A model must estimate a house’s selling price as a dollar amount from its size, location, and age. Which machine learning task best matches the requested output? Select one answer.
- A. Classification — Predict a category.
- B. Time-series forecasting — Predict future values from time-series data.
- C. Regression — Predict a numerical value.
- D. Natural language processing — Extract insights from text.

Initial selection: A. Correct set: C. Outcome: incorrect. Explanation: dollar amount is numerical, hence regression; classification is categorical, forecasting requires the time-series setup, NLP concerns text. Learner acknowledged feedback with "ok"; acknowledgment is not a successful retry.

<a name="quiz-2026-10-28-session-02-q02"></a>

#### Q02 — Recall meaning (easy, single-answer; source E)

Prompt: Which metric asks: “Of all borrowers who actually defaulted, what proportion did our model correctly flag?” Select one answer.
- A. Precision — A classification evaluation metric.
- B. Recall — A classification evaluation metric.
- C. Accuracy — A classification evaluation metric.
- D. Mean absolute error — A numerical prediction error metric.

Initial selection: B. Correct set: B. Outcome: correct. Explanation: recall uses actual positives as denominator; precision uses predicted positives, accuracy counts all correct classifications, MAE measures numerical error.

<a name="quiz-2026-10-28-session-02-q03"></a>

#### Q03 — Categorical outputs (medium, multiple-answer; source T)

Prompt: Which two requests have categorical outputs and therefore fit classification? Select two answers.
- A. Predict an invoice amount — Output the expected amount in dollars.
- B. Flag an email as spam or not spam — Output one of two labels.
- C. Forecast monthly sales — Output next year’s monthly quantities using sales history.
- D. Label a loan as low or high risk — Output one of two risk categories.

Initial selections: B, D. Correct set: B, D. Outcome: correct. Explanation: B/D are categorical; A is regression, C forecasting. This check follows Q01 feedback and does not erase the initial Q01 error.

<a name="quiz-2026-10-28-session-02-q04"></a>

#### Q04 — Forecasting setup (medium, single-answer; source T)

Prompt: A retailer has five years of monthly sales data and wants to predict sales quantities for each of the next six months. Which task most specifically matches this setup? Select one answer.
- A. Time-series forecasting — Predict future numerical values using time-series data.
- B. Classification — Predict categorical labels.
- C. Computer vision — Analyze images or detect objects.
- D. Natural language processing — Extract insights from text.

Initial selection: A. Correct set: A. Outcome: correct. Explanation: historical monthly sequence and future quantities fit forecasting; other options concern categories, images, or text.

<a name="quiz-2026-10-28-session-02-q05"></a>

#### Q05 — Recall calculation (medium, single-answer; source E)

Prompt: A model flags 15 borrowers. Of those, 6 actually default. There are 8 actual defaults overall. What is the model’s recall for default? Select one answer.
- A. 40% — 6 divided by 15.
- B. 25% — 2 divided by 8.
- C. 53.3% — 8 divided by 15, approximately.
- D. 75% — 6 divided by 8.

Initial selection: D. Correct set: D. Outcome: correct. Explanation: detects 6/8 actual defaults; A is precision, B missed share, C neither metric. Demonstrates improvement after the lesson arithmetic correction.

<a name="quiz-2026-10-28-session-02-q06"></a>

#### Q06 — Absolute error (medium, single-answer; source E)

Prompt: A house sells for $250,000, and the model predicted $235,000. What is the absolute prediction error for this house? Select one answer.
- A. $235,000 — The predicted price.
- B. $15,000 — The magnitude of the difference.
- C. −$15,000 — The signed prediction-minus-actual difference.
- D. $485,000 — The sum of the two prices.

Initial selection: B. Correct set: B. Outcome: correct. Explanation: absolute difference is nonnegative; other options give prediction, signed difference, or sum. This is a single error, not a multi-house MAE calculation.

<a name="quiz-2026-10-28-session-02-q07"></a>

#### Q07 — Accuracy versus detection success (hard application, multiple-answer; sources T, E)

Prompt: In a test set of 100 borrowers, 5 actually default. A model predicts “no default” for all 100. The bank requires detection of at least 80% of actual defaults. Which two conclusions are correct? Select two answers.
- A. Its accuracy is 95% — 95 predictions match the actual labels.
- B. It meets the detection requirement — Its overall accuracy exceeds 80%.
- C. Its default recall is 0% — It detects none of the actual defaults.
- D. Its default recall is 95% — Most borrowers were correctly labeled.

Initial selections: A, B. Correct set: A, C. Outcome: incorrect (exact-set). Explanation: A correctly reports accuracy, C reports 0/5 default recall. B compares the wrong metric to the requirement; D confuses accuracy and recall. Unresolved independent application gap; feedback does not count as a successful retry.

<a name="quiz-2026-10-28-session-02-q08"></a>

#### Q08 — Metric-specific threshold comparison (hard application, single-answer; sources T, E)

Prompt: A bank requires at least 90% default recall. On the same test population, Model A catches 18 of 20 actual defaults and flags 60 borrowers total. Model B catches 16 of 20 actual defaults and flags 20 borrowers total. Based only on the stated recall requirement, which conclusion is correct? Select one answer.
- A. Only Model B meets it — Model B has fewer false alarms.
- B. Both models meet it — Both catch most actual defaults.
- C. Only Model A meets it — Model A catches 90%; Model B catches 80%.
- D. Neither model meets it — Neither model has 90% precision.

Initial selection: C. Correct set: C. Outcome: correct. Explanation: A's recall is 90%, B's 80%; fewer false alarms or precision do not answer this specific requirement. Does not establish overall production readiness. This was a distinct post-Q07-feedback application, not a replacement of Q07's score.

Strengths: recall definition and corrected arithmetic, categorical examples, forecasting setup, absolute error, and explicit threshold comparison. Remaining gaps: numerical-output task selection (Q01) and accuracy masking missed defaults (Q07), despite successful related checks after feedback. Suggested review 2026-10-29: fresh numerical versus categorical output explanation and an imbalanced classification scenario requiring both accuracy and recall, matched to a detection target. Resume U02 before U03; teach the source's load/preprocess/split/choose/train/score/evaluate workflow next. Existing U01 review remains separate.

<a name="quiz-2026-10-28-session-01"></a>

### Optional tutor quiz — 2026-10-28-session-01

- Related unit: [M01-U01 — Introduction](notes.md#m01-u01--introduction).
- Unit/source for every item: M01-U01; https://learn.microsoft.com/en-us/training/modules/design-machine-learning-model-training-solution/1-introduction
- Participation: completed. Learner accepted an optional quiz without specifying a count; tutor planned three for the narrow introduction (one easy, two medium).
- Requested/planned: unspecified / 3. Presented / valid answered: 3 / 3.
- Correct / incorrect / skipped / invalid / unasked or unanswered: 3 / 0 / 0 / 0 / 0. Score: 3/3.
- Tutor-created formative checks, not an official Microsoft assessment. No retries.

<a name="quiz-2026-10-28-session-01-q01"></a>

#### Q01 — Defining success (easy, single-answer)

Prompt: In the Microsoft Learn lifecycle, which step establishes what the model should predict and what counts as success? Select one answer.

- A. Prepare the data — Explore, clean, and transform the data.
- B. Define the problem — Specify the prediction task and success criteria.
- C. Train the model — Experiment with algorithms and hyperparameters.
- D. Integrate the model — Deploy the model to generate predictions.

Initial learner selection: B. Correct set: B. Outcome: correct.
Explanation: defining the problem establishes the task and success criteria; A prepares data, C concerns training, D concerns integration.

<a name="quiz-2026-10-28-session-01-q02"></a>

#### Q02 — Getting and preparing data (medium, multiple-answer)

Prompt: A team has defined its prediction task but has not yet obtained or prepared its training data. Which two actions belong to the get-data and prepare-data steps? Select two answers.

- A. Deploy a prediction endpoint — Make the model available to applications.
- B. Compare algorithm hyperparameters — Experiment with training settings.
- C. Obtain access to relevant data sources — Acquire the data needed for the task.
- D. Explore, clean, and transform the data — Prepare the data for the model's requirements.

Initial learner selections: D, C. Correct set: C, D. Outcome: correct (exact-set scoring).
Explanation: C gets data and D prepares it; A integrates a model and B belongs to training.

<a name="quiz-2026-10-28-session-01-q03"></a>

#### Q03 — Iterative lifecycle (medium, single-answer)

Prompt: After deployment, monitoring shows that forecast performance no longer meets the agreed success criteria. Which response best reflects Microsoft Learn's description of the ML lifecycle? Select one answer.

- A. Continue serving without investigation — Treat deployment as the end of the lifecycle.
- B. Change the success criteria to match the results — Accept current performance without revisiting the solution.
- C. Revisit earlier steps, potentially including retraining — Use monitoring evidence to guide an iterative response.
- D. Repeat endpoint deployment as the only response — Address performance solely through redeployment.

Initial learner selection: C. Correct set: C. Outcome: correct.
Explanation: the process is iterative and monitoring can prompt retraining. A ignores the problem, B alters the target without justification, D assumes redeployment fixes predictive performance.

Strengths: lifecycle recognition, data-step distinction, and evidence-guided iteration. Clarification: business results versus predictive performance. Review proposal: a short M01-U01 recap on 2026-10-31 distinguishing sales volume from forecast error; no unresolved quiz misconception. Score alone is not mastery evidence; completion proposal also uses the application explanation.
