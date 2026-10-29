# AI-300 exam coverage

Source: [Official AI-300 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-300). Verified: **2026-10-28**.

This is a curriculum mapping, not a record of learner mastery. Mapped units are starting points based on verified module outlines; unit content must be fetched during teaching. An objective absent from an outline is marked for supplemental verification rather than assumed covered. Resolve all such items before claiming complete exam preparation.

## D1 — Design and implement an MLOps infrastructure (15–20%)

| Objective group and study-guide skills | Core unit starting points | Supplemental verification / study |
| --- | --- | --- |
| Workspace resources: create/manage workspaces, datastores, compute; workspace identity/access management | M01-U03–U05 | Workspace/datastore/compute administration and RBAC need hands-on coverage beyond service selection |
| Workspace assets: create/manage data assets, environments, components; share assets across workspaces with registries | M05-U02–U04; M06-U02 | Verify data/environment lifecycle and cross-workspace registries; components are explicit in M05 |
| IaC: secure GitHub integration; provision workspaces/resources with Bicep/CLI; automate provisioning with Actions; restrict networking; manage Git source control | M06-U02–U06 | Add Bicep/CLI resource provisioning and private networking; M06 explicitly covers Git, validation, OIDC, and job triggers |

## D2 — Implement machine learning model lifecycle and operations (25–30%)

| Objective group and study-guide skills | Core unit starting points | Supplemental verification / study |
| --- | --- | --- |
| Training: MLflow tracking, AutoML, notebooks, hyperparameter tuning, training scripts, distributed training, pipelines, job comparison | M02-U02–U08; M03-U02–U07; M04-U02–U06; M05-U02–U05; M06-U06 | Distributed training for large/deep models is not explicit in these outlines; add focused coverage |
| Registration/versioning: package feature retrieval specification with model artifact; register MLflow models; responsible AI evaluation; lifecycle/archiving | M02-U07; M07-U02 | Feature retrieval specification packaging needs supplemental verification; other skills are explicit module goals |
| Production deployment: real-time/batch managed endpoints, testing/troubleshooting, progressive rollout and rollback | M01-U06; M07-U03–U07 | M07 explicitly targets managed online deployment; verify/add managed batch deployment and testing |
| Production monitoring: data drift, production performance, retraining/alert threshold triggers | M07-U06 | Verify hands-on drift analysis and threshold-triggered alerts/retraining, beyond recognizing monitoring signals |

## D3 — Design and implement a GenAIOps infrastructure (20–25%)

| Objective group and study-guide skills | Core unit starting points | Supplemental verification / study |
| --- | --- | --- |
| Foundry platform: resources/projects, managed identities/RBAC, private networking, Bicep/CLI infrastructure | G01-U04–U05 as lifecycle context | Add dedicated Foundry provisioning, identity, networking, and IaC lessons |
| Foundation models: serverless API/managed compute deployment, model selection, versioning/production strategy, provisioned throughput units | G01-U03 for design/model selection | Verify deployment types, model version strategy, and PTU capacity planning in dedicated sources |
| Prompts: design/develop prompts, variants/performance comparison, Git version control | G02-U02–U06; G03-U02–U05 | Verify prompt-authoring and variant comparison evidence when studying these units |

## D4 — Implement generative AI quality assurance and observability (10–15%)

| Objective group and study-guide skills | Core unit starting points | Supplemental verification / study |
| --- | --- | --- |
| Evaluation: test datasets/data mapping; groundedness, relevance, coherence, fluency; risk/safety evaluation; automated built-in/custom metrics | G03-U02–U05; G04-U02–U07 | Verify every named quality metric, data mapping, harmful-content/risk evaluation, and custom metrics against the actual units; add missing exercises |
| Observability: continuous Foundry monitoring; latency/throughput/response time; token/resource/cost tracking; detailed logs/tracing/debugging | G05-U02–U07; G06-U02–U07 | Core outlines explicitly cover monitoring and tracing; verify production continuous monitoring and resource/cost interpretation in practice |

## D5 — Optimize generative AI systems and model performance (10–15%)

| Objective group and study-guide skills | Core unit starting points | Supplemental verification / study |
| --- | --- | --- |
| RAG: similarity thresholds/chunk sizes/retrieval strategies; embedding selection/fine-tuning; hybrid semantic/keyword search; relevance metrics/A/B tests | G01-U03; G03-U02–U05 provide general design/evaluation foundations | Add dedicated RAG/retrieval, embeddings, hybrid search, and A/B evaluation coverage; foundations do not establish coverage |
| Fine-tuning: advanced methods, synthetic training data, performance optimization, development-to-production lifecycle | No dedicated core module in the linked paths | Add verified fine-tuning lessons and practice; synthetic evaluation data in G04 is not equivalent to fine-tuning data |

## Supplemental backlog

These items are curriculum recommendations derived from the guide/outline comparison, not Microsoft Learn module titles. No supplemental unit content has been fetched or seeded yet. The build agent should find official sources and explicitly assign supplemental IDs when adding them to [PLAN.md](PLAN.md).

1. AML workspace, datastore, compute, identity, data/environment assets, and registries administration (D1).
2. AML Bicep/CLI provisioning, Actions automation, and private networking (D1).
3. Distributed training and feature-retrieval specification packaging (D2).
4. Managed batch endpoints, drift analysis, and alert/retraining triggers (D2).
5. Foundry resources/projects, identities, private networking, and Bicep/CLI deployment (D3).
6. Foundation model endpoint options, versioning, and PTU capacity planning (D3).
7. Evaluation coverage check: data mapping, named quality metrics, risk/safety, and custom evaluators (D4).
8. RAG retrieval tuning, embeddings, hybrid search, and relevance/A/B evaluation (D5).
9. Advanced fine-tuning, synthetic training data, monitoring, and production lifecycle (D5).

## Final readiness evidence

- All core tutor-study units completed with saved evidence. Website-only Module assessment, Knowledge check, and Summary closing units are excluded from tutor completion; use their Microsoft Learn links independently without required confirmation.
- Supplemental verification items resolved with source links, lessons, and exercise evidence.
- Cross-domain scenarios practiced and demonstrated gaps reviewed.
- Official practice assessment attempted when available; record actual results and follow-up gaps in memory. Tutor checks are not official assessment passes.
