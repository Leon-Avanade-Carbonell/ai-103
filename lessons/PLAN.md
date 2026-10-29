# AI-300 lesson plan

Curriculum verified: **2026-10-28**. Source: [AI-300T00 course](https://learn.microsoft.com/en-us/training/courses/ai-300t00), linked from the [certification](https://learn.microsoft.com/en-us/credentials/certifications/operationalizing-machine-learning-and-generative-ai-solutions/).

There are **13 modules and 110 official source units: 84 tutor-study units and 26 website-only closing units**. Each notes file below enumerates every unit with its stable ID and full source URL. Study tutor-study units in displayed order, not URL-number order. Personal progress lives in [TOLEARN.md](../memory/TOLEARN.md).

## Website-only closing units

The closing **Module assessment** (also titled **Knowledge check**) and **Summary** units are for independent use on Microsoft Learn. The tutor skips their teaching, checks, and review scheduling. They are excluded from tutor module-completion denominators and automatic TLDR readiness; no website confirmation is required. Their IDs, headings, and source links remain in notes, and exclusion does not mark them completed. Optional tutor quizzes on studied units and generated `tldr.md` references remain available.

| Module | Tutor-study units | Website-only assessment / knowledge check | Website-only summary |
| --- | --- | --- | --- |
| M01 | M01-U01–M01-U06 | M01-U07 | M01-U08 |
| M02 | M02-U01–M02-U08 | M02-U09 | M02-U10 |
| M03 | M03-U01–M03-U07 | M03-U08 | M03-U09 |
| M04 | M04-U01–M04-U06 | M04-U07 | M04-U08 |
| M05 | M05-U01–M05-U05 | M05-U06 | M05-U07 |
| M06 | M06-U01–M06-U07 | M06-U08 | M06-U09 |
| M07 | M07-U01–M07-U07 | M07-U08 | M07-U09 |
| G01 | G01-U01–G01-U06 | G01-U07 | G01-U08 |
| G02 | G02-U01–G02-U06 | G02-U07 | G02-U08 |
| G03 | G03-U01–G03-U05 | G03-U06 | G03-U07 |
| G04 | G04-U01–G04-U07 | G04-U08 | G04-U09 |
| G05 | G05-U01–G05-U07 | G05-U08 | G05-U09 |
| G06 | G06-U01–G06-U07 | G06-U08 | G06-U09 |

The module tables below count all official source units, including the website-only links.

## Before starting

Check Python basics, ML training/evaluation concepts, Azure resource/workspace basics, Git, and CLI familiarity. Before GenAIOps, check foundational generative AI/agent concepts; the official path recommends [Generative AI fundamentals](https://learn.microsoft.com/en-us/training/paths/introduction-generative-ai/). Record prerequisite gaps in memory and use focused refreshers before advancing. A source module may declare no prerequisites even when the overall path assumes experience.

## Chapter 01 — Operationalize machine learning models (MLOps)

[Official learning path](https://learn.microsoft.com/en-us/training/paths/build-first-machine-operations-workflow/)

| ID | Module and unit index | Source units | Prerequisite / recommended preparation | Exam domains |
| --- | --- | --- | --- | --- |
| M01 | [Get started with machine learning in Azure](01-mlops/01-get-started-with-machine-learning/notes.md) | 8 | Module: none; perform overall prerequisite check | D1, D2 |
| M02 | [Experiment with Azure Machine Learning](01-mlops/02-experiment-with-azure-machine-learning/notes.md) | 10 | Module: none; recommend M01 | D2 |
| M03 | [Run training scripts and track models with MLflow in Azure Machine Learning](01-mlops/03-training-scripts-and-mlflow/notes.md) | 9 | Recommend M02 and Python scripting | D2 |
| M04 | [Perform hyperparameter tuning with Azure Machine Learning](01-mlops/04-hyperparameter-tuning/notes.md) | 8 | Module: none; recommend M03 | D2 |
| M05 | [Run pipelines in Azure Machine Learning](01-mlops/05-machine-learning-pipelines/notes.md) | 7 | Module: none; recommend M03–M04 | D1, D2 |
| M06 | [Automate model training with GitHub Actions](01-mlops/06-automate-training-with-github-actions/notes.md) | 9 | Model training, AML workspaces/jobs, GitHub branches/PRs; recommend M05 | D1, D2 |
| M07 | [Deploy and monitor a model in Azure Machine Learning](01-mlops/07-deploy-and-monitor-models/notes.md) | 9 | Python/R, model training, AML jobs/models/endpoints, GitHub/CI/CD; recommend M06 | D2 |

## Chapter 02 — Operationalize generative AI applications (GenAIOps)

[Official learning path](https://learn.microsoft.com/en-us/training/paths/operationalize-gen-ai-apps/)

| ID | Module and unit index | Source units | Prerequisite / recommended preparation | Exam domains |
| --- | --- | --- | --- | --- |
| G01 | [Plan and prepare a GenAIOps solution](02-genaiops/01-plan-and-prepare/notes.md) | 8 | Generative AI concepts/services in Azure | D3, D5 |
| G02 | [Manage prompts for agents in Microsoft Foundry with GitHub](02-genaiops/02-prompt-management-and-versioning/notes.md) | 8 | Generative AI fundamentals; recommend G01 and Git | D3 |
| G03 | [Evaluate and optimize AI agents through structured experiments](02-genaiops/03-evaluate-and-optimize-agents/notes.md) | 7 | AI agents/LLMs, Git workflows, Foundry experience; recommend G02 | D4, D5 |
| G04 | [Automate AI evaluations with Microsoft Foundry and GitHub Actions](02-genaiops/04-automated-evaluations/notes.md) | 9 | Generative AI fundamentals; Python/GitHub workflows recommended; recommend G03 | D4 |
| G05 | [Monitor your generative AI application](02-genaiops/05-monitor-generative-ai-applications/notes.md) | 9 | Software development, AI, and Azure basics; recommend G04 | D4 |
| G06 | [Analyze and debug your generative AI app with tracing](02-genaiops/06-tracing-and-debugging/notes.md) | 9 | Python, AI/generative AI, Azure/Foundry basics; recommend G05 | D4 |

## Exam preparation after the core paths

Use [EXAM-COVERAGE.md](EXAM-COVERAGE.md) throughout study, then resolve its supplemental backlog before treating the curriculum as complete exam preparation. The five domain labels describe related objectives, not a guarantee that each module covers every objective in a domain.

Add supplemental lessons only after checking official source pages and updating the plan, notes, coverage mapping, and memory records together through the build agent. Use `S01`, `S02`, etc. for new modules, with `S01-U01` for units. Finish with cross-domain scenarios, due reviews, and official practice assessment resources linked from the certification page. Record actual assessment results rather than assumed readiness.
