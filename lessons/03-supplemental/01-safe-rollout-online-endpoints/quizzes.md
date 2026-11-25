# Quizzes — Safe rollout for online endpoints

- Module ID: S01
- Notes: [Lesson notes](notes.md)
- Source: https://learn.microsoft.com/en-us/azure/machine-learning/how-to-safely-rollout-online-endpoints
- Evidence identity: session ID plus question ID; one optional quiz per session, Q01–Q10 unique within that session. Initial answers are preserved.

Tutor-created formative checks, not official Microsoft assessments.

## Quiz history

<a name="quiz-2026-11-25-session-01"></a>

### Optional tutor quiz — 2026-11-25-session-01

- Date: 2026-11-25
- Units: [S01-U01](notes.md#s01-u01--safe-rollout-for-online-endpoints)
- Verified sources: `S` below means https://learn.microsoft.com/en-us/azure/machine-learning/how-to-safely-rollout-online-endpoints, fetched 2026-11-25. Retrieved content covered all question keys; the response was truncated after the initial CLI mirroring example. Rollback/retention reasoning is a tutor application of documented traffic controls.
- Participation: completed
- Requested/planned: Full quiz / 10 questions
- Presented / valid answered: 10 / 10
- Correct / incorrect / skipped / invalid / unasked or unanswered: 9 / 1 / 0 / 0 / 0
- Score: 9/10
- Difficulty mix and scoring: 3 easy, 4 medium, 3 hard; single-answer and exact-set multiple-answer scoring, one point per valid answer.
- Count scope: S01 only; module-local counts equal session-wide counts.
- Evidence provenance: actual current-conversation question-tool selections; no retries or independent Azure execution.

<a name="quiz-2026-11-25-session-01-q01"></a>

#### Q01 — Endpoint role; easy; single-answer; S01-U01; S

Prompt: In an Azure Machine Learning blue-green rollout, which resource holds the client-facing address and traffic-routing rules? Select one answer.
- A. Registered model — The versioned model asset.
- B. Online endpoint — The endpoint resource.
- C. Online deployment — An inference deployment beneath an endpoint.
- D. Registered environment — The versioned runtime environment asset.

Initial learner selections: B. Online endpoint
Correct set: B
Outcome: correct
Explanation: The endpoint holds the address and routing rules. A deployment runs inference; registered models and environments are assets used by deployments. Source: S.
Follow-up: None.

<a name="quiz-2026-11-25-session-01-q02"></a>

#### Q02 — Direct invocation at zero routed traffic; easy; single-answer; S01-U01; S

Prompt: Green exists with 0% routed live traffic. What happens when an authorized test request explicitly targets green by deployment name? Select one answer.
- A. Blue handles the request — The request follows blue's 100% allocation.
- B. The request is rejected — Zero routed traffic prevents invocation.
- C. Traffic allocation becomes green 100% — The invocation changes endpoint routing.
- D. Green handles the request — The explicit target bypasses ordinary routing rules.

Initial learner selections: D. Green handles the request
Correct set: D
Outcome: correct
Explanation: Explicit targeting invokes green without changing allocation. Blue's allocation applies to ordinary requests; zero routed traffic does not block direct testing. Source: S.
Follow-up: None.

<a name="quiz-2026-11-25-session-01-q03"></a>

#### Q03 — Instance count; easy; single-answer; S01-U01; S

Prompt: What does increasing a deployment's instance_count change? Select one answer.
- A. Its provisioned instance count — The number of compute instances used by the deployment.
- B. Its live traffic percentage — The share of ordinary requests routed to it.
- C. Its mirrored traffic percentage — The share of request copies sent to it.
- D. Its registered model version — The model asset version referenced by it.

Initial learner selections: A. Its provisioned instance count
Correct set: A
Outcome: correct
Explanation: Instance count changes provisioned compute, not routing, mirroring, or the model version. Source: S.
Follow-up: None.

<a name="quiz-2026-11-25-session-01-q04"></a>

#### Q04 — Shadow traffic behavior; medium; multiple-answer; S01-U01; S

Prompt: Blue receives 100% of routed traffic. Green receives 10% mirrored traffic on a managed online endpoint. For ordinary requests without an explicit deployment target, which two statements are true? Select two answers.
- A. Green answers 10% of clients — Its mirrored predictions become client responses.
- B. Blue supplies client predictions — The client-facing responses still come from blue.
- C. Green receives request copies — A 10% share is copied to green for observation.
- D. Mirroring disables direct testing — Green cannot be explicitly invoked while shadowing.

Initial learner selections: B. Blue supplies client predictions; C. Green receives request copies
Correct set: B, C
Outcome: correct
Explanation: Mirroring copies requests to green while blue supplies responses. Shadow predictions are not returned to those clients, and direct testing remains available. Source: S.
Follow-up: None.

<a name="quiz-2026-11-25-session-01-q05"></a>

#### Q05 — Transition to live traffic; medium; single-answer; S01-U01; S

Prompt: Green has passed shadow testing and currently receives mirrored traffic. You now want it to serve 10% of ordinary requests. Which configuration is valid? Select one answer.
- A. Keep mirroring; add green 10% live — Green receives both mirrored and routed live traffic.
- B. Increase green's instances only — Change its instance count without changing routing.
- C. Remove mirroring; blue 90%, green 10% live — Clear green's mirror allocation and set live routing.
- D. Keep blue 100%; mirror green 10% — Leave green as a shadow deployment.

Initial learner selections: C. Remove mirroring; blue 90%, green 10% live
Correct set: C
Outcome: correct
Explanation: Green cannot receive both mirrored and routed live traffic simultaneously. Increasing instances does not promote it; leaving it shadowing does not let it serve ordinary client responses. Source: S.
Follow-up: None.

<a name="quiz-2026-11-25-session-01-q06"></a>

#### Q06 — Mirroring restrictions; medium; multiple-answer; S01-U01; S

Prompt: Which two restrictions apply to the managed-endpoint mirroring feature described in this lesson? Select two answers.
- A. Mirror at most 50% of traffic — Mirroring has a percentage cap.
- B. Mirror to every deployment independently — Multiple shadow destinations can be configured.
- C. Use it on Kubernetes online endpoints — The same mirroring feature is supported there.
- D. Mirror to only one deployment — An endpoint has a single mirror destination.

Initial learner selections: D. Mirror to only one deployment; B. Mirror to every deployment independently
Correct set: A, D
Outcome: incorrect
Explanation: D is correct, but B conflicts with the one-destination limit. A was omitted: the mirrored share is capped at 50%. C is false because the feature is not supported for Kubernetes online endpoints. Exact-set scoring yields zero points. Source: S.
Follow-up: Tutor supplied the correction; no learner retry or independent recovery check occurred.

<a name="quiz-2026-11-25-session-01-q07"></a>

#### Q07 — Versioned production assets; medium; single-answer; S01-U01; S

Prompt: Which deployment configuration follows the article's production recommendation for model and environment references? Select one answer.
- A. Reference registered names and versions — For example, model azureml:pricing-model:2 and environment azureml:pricing-env:5.
- B. Reference local folders only — Keep both artifacts as local-path specifications for every release.
- C. Record versions only in a comment — Do not specify versioned asset references in the configuration.
- D. Change instance_count to select a version — Use compute instance count to choose the model and environment.

Initial learner selections: A. Reference registered names and versions
Correct set: A
Outcome: correct
Explanation: Explicit registered names and versions identify the intended assets. Local paths are supported but are not the production recommendation here; comments and instance count do not select asset versions. Source: S.
Follow-up: None.

<a name="quiz-2026-11-25-session-01-q08"></a>

#### Q08 — Rollback priority; hard; single-answer; S01-U01; S

Prompt: Green serves 10% of live traffic and begins returning errors. Blue remains healthy and has enough capacity. What should you do first to stop ordinary requests reaching green? Select one answer.
- A. Delete the endpoint — Remove the client-facing endpoint and both deployment routes.
- B. Rebuild blue from its configuration — Recreate the healthy deployment before changing traffic.
- C. Increase green's live traffic — Collect more user-facing error samples.
- D. Route blue 100%, green 0% — Return ordinary requests to the healthy deployment.

Initial learner selections: D. Route blue 100%, green 0%
Correct set: D
Outcome: correct
Explanation: Restore routing to the available healthy deployment. Deleting the endpoint disrupts service, rebuilding blue delays recovery, and increasing green's share increases exposure. Tutor rollback application of source S's documented traffic controls.
Follow-up: None.

<a name="quiz-2026-11-25-session-01-q09"></a>

#### Q09 — Retaining rollback capacity; hard; multiple-answer; S01-U01; S

Prompt: Green now serves 100% of live traffic. You want a ready rollback route during further validation. Which two actions support that goal? Select two answers.
- A. Delete blue immediately — Remove the old deployment as soon as traffic reaches green 100%.
- B. Retain blue provisioned and healthy — Keep the old deployment available to receive requests again.
- C. Ensure blue can handle returning load — Maintain enough capacity for a return to blue 100%.
- D. Delete the endpoint but keep model assets — Retain registered models while removing the serving endpoint.

Initial learner selections: B. Retain blue provisioned and healthy; C. Ensure blue can handle returning load
Correct set: B, C
Outcome: correct
Explanation: A ready rollback needs an available deployment with sufficient capacity. Deleting blue removes that target; model assets alone do not preserve a running service. Retention has a compute-cost tradeoff. Tutor application of source S's traffic, scaling, and cleanup concepts.
Follow-up: None.

<a name="quiz-2026-11-25-session-01-q10"></a>

#### Q10 — Capacity versus routing scenario; hard; single-answer; S01-U01; S

Prompt: Blue has 100% routed traffic and green has 0%. An engineer increases green from one instance to three, then sends a CLI request without --deployment-name. Which outcome follows from these settings? Select one answer.
- A. Green receives the request — Its higher instance count overrides the traffic allocation.
- B. Blue receives the request — The ordinary request follows blue's 100% traffic allocation.
- C. Both return predictions to the client — More instances automatically enable mirrored client responses.
- D. The request changes green to 100% — An ordinary invocation automatically promotes the larger deployment.

Initial learner selections: B. Blue receives the request
Correct set: B
Outcome: correct
Explanation: An ordinary request follows blue's 100% allocation. Instance count does not override routing, enable mirroring, or promote green. Source: S.
Follow-up: None.

Strengths: endpoint/deployment roles, direct invocation, shadow versus live traffic, asset version references, compute/routing separation, rollback priority and retained capacity.

Misconceptions and remaining gaps: [Q06](#quiz-2026-11-25-session-01-q06) selected mutually conflicting destination claims and omitted the 50% cap. Correction was tutor-supplied, not independently rechecked. Remaining lesson scope and unexecuted examples are documented under [S01-U01](notes.md#s01-u01--safe-rollout-for-online-endpoints).

Review proposal: S01-U01 mirroring limits, 2026-11-26; an independent check should distinguish the 50% cap, single destination, and unsupported Kubernetes feature. Offer with learner agreement; no review was delivered after the correction.

<a name="quiz-2026-11-25-session-02"></a>

### Optional tutor quiz — 2026-11-25-session-02

- Date: 2026-11-25
- Units: [S01-U01](notes.md#s01-u01--safe-rollout-for-online-endpoints)
- Verified sources: https://learn.microsoft.com/en-us/azure/machine-learning/how-to-safely-rollout-online-endpoints (article retrieval truncated after the initial mirroring CLI example); https://github.com/Azure/azureml-examples/blob/main/cli/deploy-safe-rollout-online-endpoints.sh (official script fetched in full). Both fetched 2026-11-25.
- Participation: declined
- Requested/planned: Not applicable; learner selected Skip quiz from the optional end-of-session offer.
- Presented / valid answered: 0 / 0
- Count scope: S01 only; module-local counts equal session-wide counts. No quiz items were generated or delivered; no score or answer keys apply.
- Evidence provenance: current-conversation question-tool selection. Ordinary lesson-check answers and scaffolded corrections are separate evidence in the memory session, not optional quiz items.

<a name="quiz-2026-11-25-session-03"></a>

### Optional tutor quiz — 2026-11-25-session-03

- Date: 2026-11-25
- Units: [S01-U01](notes.md#s01-u01--safe-rollout-for-online-endpoints)
- Verified sources: https://learn.microsoft.com/en-us/azure/machine-learning/how-to-safely-rollout-online-endpoints (retrieved creation, scoring, direct REST/Python invocation and mirroring content; truncated after the first CLI mirroring command); https://learn.microsoft.com/en-us/azure/machine-learning/reference-yaml-endpoint-online; https://learn.microsoft.com/en-us/azure/machine-learning/reference-yaml-deployment-kubernetes-online; https://nodejs.org/api/globals.html#fetch (relevant fetch section retrieved before later truncation). Fetched 2026-11-25.
- Participation: declined
- Requested/planned: Not applicable; learner selected Skip quiz from the optional end-of-session offer.
- Presented / valid answered: 0 / 0
- Count scope: S01 only; module-local counts equal session-wide counts. No optional quiz items were generated or delivered; no score or answer keys apply.
- Evidence provenance: actual current-conversation question-tool selection. Ordinary checks and scaffolded recovery belong in the memory session and are not optional quiz items. No Azure or local code execution occurred.
