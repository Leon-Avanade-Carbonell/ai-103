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

<a name="quiz-2026-11-16-session-01"></a>

### Optional tutor quiz — 2026-11-16-session-01

- Date: 2026-11-16
- Units: [M07-U03 — Explore the deployment and monitoring architecture](notes.md#m07-u03--explore-the-deployment-and-monitoring-architecture)
- Verified source: https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/3-explore-solution-architecture (fetched 2026-11-16)
- Participation: declined. Learner selected “Skip quiz” after the lesson.
- Requested/planned: Not applicable; no quiz count selected.
- Presented / valid answered: 0 / 0.
- Count scope: this module and the whole session; no quiz items presented.
- Evidence provenance: current-conversation question-tool offer and learner decline. Ordinary lesson-check prompts, responses, feedback, and scaffolded recovery are separate and handed off for the memory session.

No item records or score: the decline does not undo lesson-check evidence and does not establish a blanket quiz preference.

<a name="quiz-2026-11-16-session-02"></a>

### Optional tutor quiz — 2026-11-16-session-02

- Date: 2026-11-16
- Units: [M07-U04 — Control deployments with GitHub environments](notes.md#m07-u04--control-deployments-with-github-environments)
- Verified source: https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/4-control-deployments-github-environments (fetched 2026-11-16)
- Participation: declined. Learner selected “Skip quiz” after the lesson.
- Requested/planned: Not applicable; no quiz count selected.
- Presented / valid answered: 0 / 0.
- Count scope: this module and the whole session; no quiz items presented.
- Evidence provenance: current-conversation question-tool offer and learner decline. The three ordinary application checks and tutor feedback are separate and handed off for the memory session.

No item records or score: declining the quiz does not undo lesson-check evidence or establish a blanket quiz preference.

<a name="quiz-2026-11-16-session-03"></a>

### Optional tutor quiz — 2026-11-16-session-03

- Date: 2026-11-16
- Units: [M07-U05 — Deploy, promote, and roll back a model with GitHub Actions](notes.md#m07-u05--deploy-promote-and-roll-back-a-model-with-github-actions)
- Verified source: https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/4-model-deployment (fetched 2026-11-16)
- Participation: declined. Learner selected “Skip quiz” after requesting “Save and Pause”.
- Requested/planned: Not applicable; no quiz count selected.
- Presented / valid answered: 0 / 0.
- Count scope: this module and the whole session; no quiz items presented.
- Evidence provenance: current-conversation question-tool offer and learner decline. Ordinary lesson-check prompts, initial answers, tutor feedback, and follow-up results are separate and supplied to the memory session.

No item records or score: the decline is not a failed check and does not establish a blanket quiz preference. The unit's remaining automation work is separate from optional quiz participation.

<a name="quiz-2026-11-26-session-01"></a>

### Optional tutor quiz — 2026-11-26-session-01

- Date: 2026-11-26
- Units: [M07-U05](notes.md#m07-u05--deploy-promote-and-roll-back-a-model-with-github-actions); supporting reinforcement of [M07-U04](notes.md#m07-u04--control-deployments-with-github-environments).
- Verified sources: S1 = https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/4-model-deployment; S2 = https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/4-control-deployments-github-environments. Both fetched 2026-11-26.
- Participation: completed.
- Requested/planned: Short quiz (up to 5) / 5.
- Presented / valid answered: 5 / 5.
- Correct / incorrect / skipped / invalid / unasked or unanswered: 5 / 0 / 0 / 0 / 0.
- Score: 5/5.
- Difficulty mix: 1 easy, 3 medium, 1 hard; single-answer except Q03, scored by exact set.
- Count scope: M07 module-local counts equal session-wide counts.
- Evidence provenance: initial selections returned by the question tool in this conversation. No retries, deployment execution, or official Microsoft assessment claimed. Q04's numeric response is from a labeled tutor illustration.

<a name="quiz-2026-11-26-session-01-q01"></a>

#### Q01 — OIDC authentication; easy; single-answer; M07-U05; S1

Prompt: What is the main authentication benefit of OIDC in this deployment workflow? Select one answer.
- A. Automatic production approval — Approve releases when Azure login succeeds.
- B. Short-lived federated access — Authenticate without storing a long-lived Azure client secret.
- C. Guaranteed model accuracy — Validate predictions during authentication.
- D. Unrestricted Azure permissions — Give the workflow access to all Azure resources.

Initial learner selections: B. Short-lived federated access.
Correct set: B.
Outcome: correct.
Explanation: OIDC provides short-lived federated authentication without a stored client secret. It does not approve releases (A), validate predictions (C), or grant unrestricted permissions (D); S1, with control separation in S2.
Follow-up: No retry.

<a name="quiz-2026-11-26-session-01-q02"></a>

#### Q02 — Isolated direct testing; medium; single-answer; M07-U05; S1

Prompt: Green is ready at 0% routed traffic. You want to test it without returning green's predictions to normally routed users. Which action fits? Select one answer.
- A. Route 10% to green — Use a limited live traffic split.
- B. Route 100% to green — Test after full promotion.
- C. Invoke the registered model asset — Use registration alone as the prediction service.
- D. Invoke green directly — Specify --deployment-name green in the endpoint invocation.

Initial learner selections: D. Invoke green directly.
Correct set: D.
Outcome: correct.
Explanation: Direct invocation targets green while normal routing remains unchanged. A and B expose normally routed users to green; C confuses a registered asset with a serving deployment (S1).
Follow-up: No retry.

<a name="quiz-2026-11-26-session-01-q03"></a>

#### Q03 — Approval and authorization; medium; multiple-answer; M07-U04, M07-U05; S1, S2

Prompt: A team separates deployment/testing from production traffic promotion. Which two statements correctly describe the controls? Select two answers.
- A. Promotion references production — The traffic-change job targets an environment configured with required-reviewer protection.
- B. OIDC replaces reviewer approval — Successful authentication alone authorizes the release decision.
- C. RBAC limits Azure operations — Each federated identity receives only the resource permissions its job requires.
- D. Naming production provisions Azure — The GitHub environment name creates the production endpoint.

Initial learner selections: C. RBAC limits Azure operations; A. Promotion references production (returned in this order).
Correct set: A, C.
Outcome: correct (exact set).
Explanation: The protected environment gates promotion, and RBAC limits resource operations. OIDC does not replace approval (B), and an environment name does not provision Azure resources (D); S1, S2.
Follow-up: No retry.

<a name="quiz-2026-11-26-session-01-q04"></a>

#### Q04 — Validate rather than merely invoke; hard; single-answer; M07-U05; S1

Prompt: A workflow invokes green and prints its prediction successfully. The fixed test input should produce approximately 0.82, but green returns 0.20. What is the best interpretation? Select one answer.
- A. Successful invocation proves quality — The workflow can safely shift traffic because a response arrived.
- B. Validation must block promotion — Compare the response with the test criterion and fail the test step when it is violated.
- C. More traffic repairs the result — Increase green's allocation before checking expected outputs.
- D. Approval replaces response testing — Let a reviewer approve without automated validation.

Initial learner selections: B. Validation must block promotion.
Correct set: B.
Outcome: correct.
Explanation: S1 requires comparing direct responses with expectations before traffic changes. Invocation success is not validation (A), more traffic does not repair a violated criterion (C), and approval complements testing (D; S2). Numeric values and the validation script are tutor-created illustrations, not the source's model or supplied code.
Follow-up: No retry.

<a name="quiz-2026-11-26-session-01-q05"></a>

#### Q05 — Restore healthy routing; medium; single-answer; M07-U05; S1

Prompt: Green receives 10% of live traffic and starts failing; blue is healthy and still available. Which immediate recovery best follows the safe-rollout approach? Select one answer.
- A. Delete the endpoint — Recreate its serving URL before investigating.
- B. Diagnose before changing traffic — Keep the failing split until root cause is known.
- C. Restore blue=100 green=0 — Recover normal routing first, then investigate green.
- D. Delete blue and promote green — Remove the working deployment and route all requests to green.

Initial learner selections: C. Restore blue=100 green=0.
Correct set: C.
Outcome: correct.
Explanation: Restore normally routed traffic to healthy blue, preserving the endpoint URL, then investigate green. A disrupts recovery, B prolongs exposure, and D removes the working fallback (S1).
Follow-up: No retry.

Strengths: OIDC purpose, isolated testing, approval versus authorization, response validation, and exact rollback allocation (Q01–Q05).
Remaining gaps: no incorrect quiz responses. Full workflow implementation, files, readiness checks, and execution remain unverified; the score is conceptual evidence, not practical proficiency or an official pass.
Review proposal: M07-U05 release-control transfer on 2026-12-03, with agreement; explain and apply testing, approval, and rollback in a changed scenario. Existing reviews should be validated and deduplicated by memory-agent rather than automatically multiplied.

<a name="quiz-2026-11-26-session-02"></a>

### Optional tutor quiz — 2026-11-26-session-02

- Date: 2026-11-26
- Units: [M07-U06 — Monitor the deployed model](notes.md#m07-u06--monitor-the-deployed-model).
- Verified source: S1 = https://learn.microsoft.com/en-us/training/modules/deploy-model-github-actions/5-monitor-model (fetched 2026-11-26; page updated 2026-11-06).
- Participation: completed.
- Requested/planned: Short quiz / 5.
- Presented / valid answered: 5 / 5.
- Correct / incorrect / skipped / invalid / unasked or unanswered: 5 / 0 / 0 / 0 / 0.
- Score: 5/5.
- Difficulty mix: 2 easy, 2 medium, 1 hard; single-answer except Q02, scored by exact set.
- Count scope: M07 module-local counts equal session-wide counts.
- Evidence provenance: actual initial question-tool selections in the current conversation, after lesson feedback. No retries, practical execution, or official assessment outcome claimed.

<a name="quiz-2026-11-26-session-02-q01"></a>

#### Q01 — Operational health; easy; single-answer; M07-U06; S1

Prompt: Question 1/5 — Easy. Select one answer. Which observation primarily indicates an endpoint operational-health problem?
- A. Appointment lead times shift — The incoming feature distribution changes.
- B. Request latency rises sharply — Requests take substantially longer to complete.
- C. Predicted risk scores shift — The model's output distribution changes.
- D. Feature importance changes — The relative influence of features shifts.

Initial learner selections: B. Request latency rises sharply.
Correct set: B.
Outcome: correct.
Explanation: Latency measures service responsiveness. A is data drift, C is prediction drift, and D is feature attribution drift (S1).
Follow-up: No retry.

<a name="quiz-2026-11-26-session-02-q02"></a>

#### Q02 — Monitoring setup; medium; multiple-answer; M07-U06; S1

Prompt: Question 2/5 — Medium. Select two answers. A team has deployed an online model but has not configured model monitoring. Which two setup actions does the unit describe for comparing production data with reference data?
- A. Enable deployment data collection — Collect incoming requests and model responses.
- B. Register another model version — Create an additional versioned model asset.
- C. Create a scheduled model monitor — Configure comparison with a reference dataset.
- D. Allocate traffic to every deployment — Give each deployed version live requests.

Initial learner selections: A. Enable deployment data collection; C. Create a scheduled model monitor.
Correct set: A, C.
Outcome: correct (exact set).
Explanation: Data collection supplies production inputs and outputs; the configured monitor compares data on a schedule. Registering another version or distributing traffic to every deployment does not configure monitoring (S1).
Follow-up: No retry.

<a name="quiz-2026-11-26-session-02-q03"></a>

#### Q03 — Data quality; easy; single-answer; M07-U06; S1

Prompt: Question 3/5 — Easy. Select one answer. Production requests begin containing missing values and previously unseen categories. Which monitoring signal directly addresses these issues?
- A. Prediction drift — A change in the distribution of model outputs.
- B. Feature attribution drift — A change in relative feature importance.
- C. Request count — The number of requests handled by the service.
- D. Data quality — Problems in the validity or completeness of input data.

Initial learner selections: D. Data quality.
Correct set: D.
Outcome: correct.
Explanation: Data quality covers missing values, unexpected categories, and out-of-range values. A concerns outputs, B concerns feature importance, and C measures request volume (S1).
Follow-up: No retry.

<a name="quiz-2026-11-26-session-02-q04"></a>

#### Q04 — Release-related failure; medium; single-answer; M07-U06; S1

Prompt: Question 4/5 — Medium. Select one answer. Immediately after a new deployment is promoted, scoring errors spike. The retained previous deployment remains healthy. What is the best immediate response?
- A. Retrain before changing traffic — Complete new training while the faulty deployment keeps serving.
- B. Restore traffic to the previous deployment — Recover service, then investigate the new deployment.
- C. Delete the entire endpoint — Remove the service and create a replacement URL.
- D. Wait for a drift alert — Keep the traffic allocation until a model monitor signals drift.

Initial learner selections: B. Restore traffic to the previous deployment.
Correct set: B.
Outcome: correct.
Explanation: A healthy fallback supports immediate rollback, followed by investigation. A delays recovery without evidence that training is the fix; C unnecessarily removes the endpoint; D waits for an unrelated signal despite known scoring failures (S1).
Follow-up: No retry.

<a name="quiz-2026-11-26-session-02-q05"></a>

#### Q05 — Drift without established quality loss; hard; single-answer; M07-U06; S1

Prompt: Question 5/5 — Hard. Select one answer. No model deployment has changed. A clinic changes scheduling policy, and appointment lead-time data crosses a drift threshold. There is not yet evidence that prediction quality has declined. What is the best next step?
- A. Automatically retrain and promote — Treat the threshold crossing as sufficient release evidence.
- B. Roll back to the previous model — Assume the older version avoids the changed input conditions.
- C. Investigate the change and its impact — Check the policy change and evaluate predictions against actual outcomes when available.
- D. Ignore drift while latency is normal — Treat service responsiveness as proof of prediction quality.

Initial learner selections: C. Investigate the change and its impact.
Correct set: C.
Outcome: correct.
Explanation: A drift threshold prompts investigation. A skips evaluation; B assumes an older model solves changed conditions; D confuses service health with prediction quality (S1).
Follow-up: No retry.

Strengths: service-health recognition, explicit monitoring setup, data-quality identification, release-failure rollback, and investigation before responding to drift (Q01–Q05).
Remaining gaps: no incorrect quiz answers. Earlier lesson responses required clarification of rollback versus changed conditions; Q04–Q05 demonstrate post-feedback recognition, not delayed independent transfer. Monitoring implementation remains unverified.
Review proposal: M07-U06, 2026-11-29, with agreement: apply investigate/rollback/retraining decisions to a changed scenario and distinguish operational from model-monitoring signals. This score is formative evidence, not an official pass or practical proficiency.
