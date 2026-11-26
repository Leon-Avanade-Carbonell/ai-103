# Safe rollout for online endpoints

- Module ID: S01 (supplemental documentation lesson, not an official training module)
- Source: https://learn.microsoft.com/en-us/azure/machine-learning/how-to-safely-rollout-online-endpoints
- Curriculum verified: 2026-11-16
- Exam objectives: D2 production deployment testing, progressive rollout, and rollback.
- Source context: Azure Machine Learning API v2; Azure CLI ml extension v2 and Python SDK azure-ai-ml v2.

## Overview and learning goals

Planned goals, derived from the verified official article, with a tutor-created rollback application of its traffic controls:

- Define a managed online endpoint and blue/green deployments, including model, scoring code, environment, and compute configuration.
- Confirm and scale the existing deployment, then create a green candidate without routed live traffic.
- Test a deployment directly and distinguish direct invocation, mirrored traffic, and live traffic allocation.
- Understand managed-endpoint mirroring limits and relevant Kubernetes endpoint differences.
- Shift a limited share of live traffic, promote fully, roll back to the retained blue deployment if needed, and retire the old deployment after validation.

## Notes by source unit

### S01-U01 — Safe rollout for online endpoints

Source: https://learn.microsoft.com/en-us/azure/machine-learning/how-to-safely-rollout-online-endpoints

Source verified for planning: 2026-11-16; fetched for study: 2026-11-25, Azure Machine Learning API v2. This single tutor-study unit maps to the whole article. Both article retrievals were truncated after the initial CLI mirroring example; the [official rollout script](https://github.com/Azure/azureml-examples/blob/main/cli/deploy-safe-rollout-online-endpoints.sh), fetched separately on 2026-11-25, verified mirror reset, staged/full promotion, and deployment/endpoint deletion commands. Later article content is not claimed as retrieved. No Azure commands or SDK code were executed.

The article covers direct testing, mirroring, live promotion, and old-deployment removal. Rollback to retained blue is a tutor application of its traffic controls, not a separate article section.

#### Define the endpoint and deployment

Official source: an endpoint holds the client-facing address, authentication settings, and traffic-routing rules. Deployments beneath it host the model, scoring code, environment, and compute that perform inference. Blue and green are deployment names, not separate client-facing endpoints.

Creating a candidate deployment and promoting it are separate operations. Blue can retain all ordinary routed traffic while green exists with zero allocated live traffic. Provisioned green instances can still incur compute costs.

For production, the article recommends registered model and environment names with explicit versions. These asset references are separate from compute configuration and traffic allocation.

The 2026-11-25 retrieval included creation YAML and Python, scoring-script requirements, and the REST direct-invocation header. Supplemental references fetched that day: [online endpoint YAML](https://learn.microsoft.com/en-us/azure/machine-learning/reference-yaml-endpoint-online), [Kubernetes deployment YAML](https://learn.microsoft.com/en-us/azure/machine-learning/reference-yaml-deployment-kubernetes-online), and [Node.js fetch](https://nodejs.org/api/globals.html#fetch). The Node response was truncated after the relevant fetch documentation. All examples are unexecuted.

#### Scoring contract and creation versus promotion

In the article's custom Python scoring-script pattern, `init()` initializes scoring, for example loading the model into memory; `run()` handles each request, interprets inputs, invokes the model, and returns a response. The model artifact, scoring code, and runtime dependencies have distinct roles. Explicit registered model/environment versions do not automatically version the scoring source; preserve that source reproducibly in Git as well (tutor operational guidance).

If scoring code expects `features` but clients send `data`, inspect request parsing and the actual payload contract. Increasing `instance_count` cannot repair an incompatible input format. Successful provisioning, including an SDK operation completing with `.result()`, is not prediction-quality evidence.

The article creates green without `--all-traffic`, leaving its allocated live traffic at zero. Adding that flag assigns all endpoint traffic to the newly created deployment: it is a promotion decision, not a prerequisite for direct testing. In Python, deployment provisioning and updating `endpoint.traffic` are separate operations.

#### Kubernetes configuration differences

Official source/reference distinctions: use Kubernetes endpoint/deployment schemas and the `KubernetesOnlineEndpoint` / `KubernetesOnlineDeployment` Python classes rather than their managed counterparts. Endpoint `compute` selects an attached Kubernetes compute target; do not specify it for managed online inference. Kubernetes deployment `instance_type` selects a cluster-configured instance type, not necessarily a managed VM SKU. For manual scaling specify `scale_settings.type: default` with `instance_count`; the reference also supports `target_utilization` scaling. These are conceptual configuration distinctions, not an executed cluster setup.

Kubernetes does not support mirroring. Tutor application: direct sample invocation can test green before ordinary client exposure; a limited live share is a subsequent rollout option that returns green's predictions to some clients, not a shadow-testing substitute with identical safety properties.

#### Confirm your existing deployment; deploy a new model but don't send it traffic

Official source: invocation with a deployment name targets that deployment directly, bypassing ordinary traffic allocation. Without a deployment name, incoming requests follow the endpoint's traffic rules. Thus green at 0% routed traffic remains directly testable, and invoking green does not promote it.

#### Scale your existing deployment to handle more traffic

Official source: `instance_count` controls the number of deployment compute instances. It does not change the endpoint's `traffic` or `mirror_traffic` settings. The article recommends at least three instances for high availability. Capacity must be assessed separately from routing percentages.

#### Test the deployment with mirrored traffic

Official source: mirroring (shadowing) copies a percentage of ordinary live requests to a candidate for observation, such as latency and HTTP errors, without returning its predictions to those clients. With blue at 100% live traffic and green at 10% mirrored traffic, blue supplies client predictions and green receives request copies.

Mirroring supports only one destination deployment per endpoint and at most 50% of traffic. It is not supported for Kubernetes online endpoints. A deployment cannot receive both mirrored traffic and routed live traffic simultaneously. Direct invocation remains available while shadowing.

Explicitly targeting any deployment bypasses mirroring as well as ordinary routing. For example, a request naming blue is not copied to green; omit the deployment name to exercise ordinary routing and make the request eligible for shadowing. A percentage describes traffic distribution, not a guaranteed count in every small batch.

The article specifies mirroring support from Azure Machine Learning CLI (`ml` extension) 2.4.0 and Python package `azure-ai-ml` 1.0.0. These package numbers do not change the API-v2 designation. Updating an endpoint with older clients can remove mirror settings.

Shadow requests consume compute and endpoint bandwidth even though their predictions are not returned to ordinary clients. The article documents a default endpoint bandwidth quota of 5 MB/s and throttling when the allocated quota is exceeded. Before increasing the mirrored share, assess bandwidth headroom/throttling and green's processing capacity separately. Adding compute instances does not increase endpoint bandwidth quota.

#### Promotion, rollback, and retirement

The verified article overview specifies limited live traffic, full promotion to green, and deletion of unused blue. Unlike mirroring, limited live traffic lets green supply predictions to real clients. Remove green's mirror allocation before assigning it a live share.

Tutor application of the documented traffic controls: if green returns unacceptable errors, restore blue 100% and green 0% first. Retaining a healthy, provisioned blue deployment with sufficient capacity gives a ready rollback target. Rebuilding blue delays recovery; deleting green is not necessary to restore routing and can remove diagnostic context. Deleting blue after promotion removes the ready rollback target; retaining it temporarily trades compute cost for recovery readiness.

Blue must have capacity for returning load. Fewer instances reduce concurrency and throughput; overload can cause queueing, latency, timeouts, or rejected requests without necessarily slowing each inference computation. Routing and capacity readiness are separate.

After green passes validation at 100% live traffic, deleting blue removes its compute and ready rollback target but retains green and the shared endpoint. Endpoint deletion removes the service and its deployments. The validation window is an operational decision, not a fixed five-minute source rule.

Pending study: fuller Python endpoint/deployment object construction and rollout examples, including complete sample files and additional SDK rollout calls verified from available sources. Creation YAML, REST/JavaScript invocation applicability, and the relevant Kubernetes configuration differences are explained below. Detailed CLI promotion/cleanup commands were verified separately in the official script; later article retrieval remains limited as described above.

<a id="key-concepts-and-decision-points"></a>

## Python examples

S01-U01 source-derived SDK pattern, not executed. Prerequisites: Python 3.10+, Azure ML Python SDK v2 (`azure-ai-ml`), `azure-identity`, an authenticated `MLClient` named `ml_client`, appropriate workspace RBAC access, sufficient quota, `endpoint_name` set to an existing endpoint, and a configured `ManagedOnlineDeployment` object named `green_deployment`. The request file must exist and match green's scoring contract. Installed versions are unknown. These operations provision resources and, in the final block, change live routing; validate before promotion.

```python
# Provision green without assigning live traffic.
ml_client.online_deployments.begin_create_or_update(
    green_deployment
).result()

# Direct test: no live routing change.
response = ml_client.online_endpoints.invoke(
    endpoint_name=endpoint_name,
    deployment_name="green",
    request_file="sample-request.json",
)

# Separate promotion step, only after validation.
endpoint = ml_client.online_endpoints.get(name=endpoint_name)
endpoint.traffic = {"blue": 0, "green": 100}
ml_client.online_endpoints.begin_create_or_update(endpoint).result()
```

Expected outcomes: provisioning completes, a named invocation returns green's response, and the final endpoint update promotes green for ordinary clients. `.result()` waits for the operation; it is not a quality check. Pending study: full endpoint/deployment object construction, complete sample files, and further SDK rollout examples.

## JavaScript examples

S01-U01 tutor-created REST consumer applying the rollout article's documented HTTP pattern; this is not a JavaScript deployment-management SDK counterpart. Node.js 22+ with built-in `fetch`, an `.mjs` file, an existing key-authenticated endpoint, network access, `SCORING_URI` and `ENDPOINT_KEY` securely supplied through environment variables, and a defined compatible `payload` are required. Do not commit credentials. Built-in fetch is no longer experimental from Node 21 according to the fetched Node reference. Installed versions are unknown; not executed.

```javascript
const response = await fetch(process.env.SCORING_URI, {
  method: "POST",
  headers: {
    Authorization: `Bearer ${process.env.ENDPOINT_KEY}`,
    "Content-Type": "application/json",
    "azureml-model-deployment": "green",
  },
  body: JSON.stringify(payload),
});

const body = await response.text();
if (!response.ok) {
  throw new Error(`Scoring failed: ${response.status} ${body}`);
}
console.log(body);
```

Expected outcome: green processes this request without altering live allocation. Remove the `azureml-model-deployment` header to follow the endpoint's existing traffic rules. Changing endpoint `--traffic` updates routing policy globally; removing this request header stops bypassing that policy. These are separate controls.

## Azure CLI commands

S01-U01 tutor illustration, using the source's direct-invocation command pattern. Prerequisites: configured Azure CLI with ml extension v2, Bash or a compatible shell, workspace access, an existing green deployment, `ENDPOINT_NAME` set to the endpoint name, and a compatible `sample-request.json` file in the current directory. Not executed; installed versions are unknown. Expected outcome: green's scoring response, without changing ordinary routing.

```bash
az ml online-endpoint invoke \
  --name "$ENDPOINT_NAME" \
  --deployment-name green \
  --request-file sample-request.json
```

S01-U01 source-derived operational sequence, verified against the article and official script. Requires configured workspace/resource-group defaults (or explicit workspace/resource-group arguments), an existing endpoint with blue and green, appropriate RBAC permissions, sufficient compute quota, and Bash-compatible syntax. Use `ml` extension 2.4.0 or later for mirroring; installed versions are unknown. All commands are illustrative and unexecuted. These mutate serving resources/routing; promotion requires prior validation.

```bash
# Capacity only: three instances, not a traffic change
az ml online-deployment update \
  --name blue --endpoint-name "$ENDPOINT_NAME" --set instance_count=3

# Shadow observation; blue still supplies ordinary client predictions
az ml online-endpoint update \
  --name "$ENDPOINT_NAME" --mirror-traffic "green=10"

# Remove shadow allocation before green receives live traffic
az ml online-endpoint update \
  --name "$ENDPOINT_NAME" --mirror-traffic "green=0"

# Limited live rollout, then full promotion after validation
az ml online-endpoint update \
  --name "$ENDPOINT_NAME" --traffic "blue=90 green=10"
az ml online-endpoint update \
  --name "$ENDPOINT_NAME" --traffic "blue=0 green=100"

# Tutor rollback application: blue must remain healthy and sufficiently provisioned
az ml online-endpoint update \
  --name "$ENDPOINT_NAME" --traffic "blue=100 green=0"

# Retirement only after validation and acceptance of losing ready blue rollback
az ml online-deployment delete \
  --name blue --endpoint "$ENDPOINT_NAME" --yes --no-wait
```

Expected outcomes: scaling changes capacity only; mirror reset stops copies; live allocations change who supplies ordinary client predictions; deployment deletion retires blue while keeping the endpoint/green. `--no-wait` returns without waiting for deletion to complete, so command return is not confirmation of completed deletion. The three-instance value illustrates the article's high-availability recommendation, not a guarantee of workload capacity.

S01-U01 creation command using the full illustrative YAML below. Requires an existing endpoint named `pricing-endpoint`, configured workspace/resource-group defaults, referenced assets, scoring files and dependencies, permissions and compute quota. Use a current CLI `ml` v2 extension; not executed.

```bash
az ml online-deployment create \
  --name green \
  --endpoint-name pricing-endpoint \
  --file green-deployment.yml
```

Expected outcome: green is provisioned without allocated live traffic. Do not add `--all-traffic` merely to make it testable; that flag assigns 100% traffic to the new deployment. Complete runnable model/scoring/request sample files have not been assembled or executed.

## Related configuration: YAML, Bicep, or GitHub Actions

S01-U01 tutor-created endpoint and deployment YAML using the article's supported structure and production asset-reference recommendation. Requires a current CLI `ml` v2 extension, an existing workspace, the referenced registered assets, appropriate permissions, sufficient compute quota, and a `src/score.py` compatible with the model/environment. Paths are illustrative, not supplied files. The endpoint must exist before creating green; its name must be available in the region when creating it. Not executed; installed versions are unknown. The latest schema reference guarantees syntax for the latest extension, not all older extension versions.

`endpoint.yml`:

```yaml
$schema: https://azuremlschemas.azureedge.net/latest/managedOnlineEndpoint.schema.json
name: pricing-endpoint
auth_mode: key
```

`green-deployment.yml`:

```yaml
$schema: https://azuremlschemas.azureedge.net/latest/managedOnlineDeployment.schema.json
name: green
endpoint_name: pricing-endpoint
model: azureml:pricing-model:2
code_configuration:
  code: ./src
  scoring_script: score.py
environment: azureml:pricing-env:5
instance_type: Standard_DS3_v2
instance_count: 3
```

Expected meaning: the endpoint defines the shared service and key authentication; green selects model/environment versions, scoring code, and three compute instances. Neither file allocates green live or mirrored traffic. Endpoint traffic is configured after deployments exist. Three instances reflect the article's high-availability recommendation, not proven workload capacity. Kubernetes requires its own schemas/compute configuration rather than copying this managed example unchanged.

## Worked examples and practice

S01-U01 tutor-created conceptual practice; no Azure execution:

- With blue at 100% and green at 0%, a request explicitly targeting green reaches green; an ordinary request follows routing to blue. Remove a REST client's targeting header to follow an existing 90/10 split; do not change the endpoint policy to green 100%.
- Directly invoke an unvalidated green first. Mirroring observes request copies without returning green's predictions; a live share exposes clients. Requests explicitly naming blue bypass mirroring, so omit the deployment target to test shadowing. Kubernetes supports direct testing but not mirroring.
- If green fails at 10% live traffic and blue is healthy and sufficiently provisioned, restore blue 100%, green 0%, then investigate. Retaining adequate blue capacity trades cost for recovery readiness; retire blue after validation to stop its compute cost while keeping the endpoint.
- Instance count changes capacity, not routing. Check bandwidth and throttling separately before increasing mirroring; extra instances do not resolve bandwidth quota exhaustion. If payload fields disagree, inspect the scoring contract rather than instance count.
- `green=0` disables copies with `--mirror-traffic` but removes green's live share with `--traffic`. The 90/10 live update is client-facing promotion.

[Quiz history](quizzes.md)

<a id="common-pitfalls-and-clarifications"></a>

## Microsoft Learn search terms

- Azure Machine Learning managed online endpoint blue green safe rollout
- online endpoint direct invocation deployment name
- managed online endpoint mirror traffic shadow testing
- online endpoint traffic allocation rollback
