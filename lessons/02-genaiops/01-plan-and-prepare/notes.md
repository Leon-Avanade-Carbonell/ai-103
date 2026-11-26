# Plan and prepare a GenAIOps solution

- Module ID: G01
- Source: https://learn.microsoft.com/en-us/training/modules/plan-prepare-genaiops/
- Curriculum verified: 2026-10-28
- Exam objectives: D3 model selection foundations; D5 optimization foundations.

## Overview and learning goals

Planned source goals: define agent specifications, design/optimize an agent, describe the GenAIOps lifecycle, and identify tools/frameworks for its phases.

## Notes by Microsoft Learn unit

### G01-U01 — Introduction
Source: https://learn.microsoft.com/en-us/training/modules/plan-prepare-genaiops/1-introduction

Source fetched: 2026-11-26; page updated 2026-11-04. The explanations below follow the Microsoft Learn introduction; the tent example is tutor-created.

#### Plan what “good” means before building

An agent is more than a single prompt: it uses one or more language models, connects to relevant data, and can take actions on a user's behalf. Microsoft's Adventure Works example uses a product catalog and customer purchase histories to help shoppers choose outdoor equipment.

A fluent, convincing demo is not proof of a dependable agent. Planning starts with a specification of what the agent should do and how its behavior will be evaluated. The module then covers design and optimization, the GenAIOps lifecycle, and supporting tools and frameworks.

#### Grounding supports correctness but does not guarantee it

Check whether an answer uses the right trusted references, not just whether it sounds persuasive. A valid reference alone is still insufficient: the recommendation must fit the user's requirements.

**Tutor illustration (conceptual, no code or Azure execution):** “Help shoppers choose camping equipment” is a vague ambition. “Recommend tents suitable for the shopper's stated conditions, using verified catalog information” gives the team a clearer behavior to build and test. Before production approval, specify scope, trusted data, and evaluation criteria for factual accuracy and suitability.

### G01-U02 — Define agent specifications
Source: https://learn.microsoft.com/en-us/training/modules/plan-prepare-genaiops/2-use-cases

Source fetched: 2026-11-26; page updated 2026-11-04. The specification framework below follows Microsoft Learn; IT-agent examples and the distinction between behavioral and technical controls are tutor explanations. Examples are conceptual, with no code or Azure execution.

#### Specify the job before choosing the implementation

An agent specification connects five elements: **user intent → suggested prompts → capabilities → evaluation → test data**. It defines what the agent should do, how it should behave, and how the team will judge quality before building.

- **User intent:** State the job description, target audience, and pain points. “Help users” is too broad to guide design; naming the audience also guides vocabulary and tone.
- **Suggested prompts:** A display prompt is a suggested question the user sees or clicks. A command prompt is the underlying instruction guiding the agent's behavior. Keep the promise made to the user aligned with actual capabilities.
- **Capabilities:** Define primary functions, required tools and data access, and restrictions. Instructions do not supply tools or authorization.

**Tutor worked example:** An IT agent helps nontechnical employees troubleshoot company-app sign-in problems and identify access issues that need escalation. If it can only search approved help articles, “How can I recover access to my account?” is a suitable display prompt; “Unlock my account” promises an action it cannot perform. Users need goal-oriented suggestions, not a list of internal tools.

For a request to grant administrator access, this agent should explain its limitation and provide the approved access-request process or direct the employee to IT. Behavioral instructions guide responses; tool availability and permissions enforce what actions are possible. Model guardrails should not be the only protection for privileged operations. Even when no permissions change, falsely claiming “Done—you now have administrator access” is still a failure: responses must accurately describe what happened.

#### Define quality criteria and representative tests

A **rubric** names criteria and describes a good answer so reviewers judge consistently. Microsoft's shopping-agent example uses relevance, groundedness, and friendly tone. **Shadow rating** compares agent answers with human support answers without exposing customers to the agent's responses.

Test requests are the inputs being evaluated; testing approaches describe how those inputs are used:

- **Smoke tests:** A small, fast set with known good answers, run after small updates to catch obvious breakage.
- **Larger automated evaluation:** A larger dataset scored at scale before bigger changes.
- **Coverage mix:** Include common requests, ambiguous cases, rare edge cases, and requests requiring refusal or escalation. A high overall score can hide failures in situations absent from the test set.

Smoke tests can include boundary cases, and larger evaluations should include ordinary cases too. Size and speed—not an ordinary-versus-boundary split—distinguish these approaches.

**Tutor worked test cases:**

| Test request | Expected behavior |
| --- | --- |
| “I forgot my work-account password. What should I do?” | Give approved, grounded password-reset guidance without claiming to reset it. |
| “Give me administrator access so I can install this application.” | Explain that the agent cannot grant access and provide the approved escalation route; do not claim permissions changed. |

### G01-U03 — Design and optimize your agent
Source: https://learn.microsoft.com/en-us/training/modules/plan-prepare-genaiops/3-select-model

Source fetched: 2026-11-26; page updated 2026-11-04. The design framework follows Microsoft Learn; IT-support examples and failure diagnosis are tutor illustrations. No code or Azure execution was performed.

#### Match the model to the task

Choose capabilities and model size from the specification, then evaluate candidates against the quality rubric, cost, and latency requirements. A smaller model can suit a focused, high-traffic task; a larger or reasoning-oriented model may suit more demanding work. Neither size alone establishes suitability. Clear instructions benefit both.

**Tutor illustration:** For an agent that explains approved password-reset procedures, test a smaller conversational model first. If it gives misleading access guidance, identify the cause before increasing model size: missing information, poor retrieval, unclear instructions, or difficulty interpreting the supplied context.

#### Use RAG for changing facts; fine-tuning for behavior

**Retrieval augmented generation (RAG)** supplies relevant external information as context at answer time. It suits changing catalogs or policies because updating the external data does not require retraining the model. Its freshness depends on the data source and retrieval pipeline.

**Fine-tuning** adapts model behavior using training examples, such as a consistent style or specialized skill. It does not automatically incorporate later factual updates. RAG and fine-tuning can be combined: retrieval for current facts, fine-tuning for behavior.

**Tutor worked decision:** For weekly access-policy changes and a friendly support style, start with RAG and command-prompt instructions for tone. Fine-tuning is not required merely to request a consistent voice.

Retrieving the right document does not guarantee a grounded answer. Check both whether the relevant passage reached the model and whether the answer faithfully reflects it without unsupported claims. If the correct passage is present but the answer contradicts it, investigate answer generation and context interpretation rather than assuming stale retrieval data.

#### Optimize against the rubric

Refine the command prompt, run quick smoke tests after small changes, and use broader automated evaluation before bigger changes. Compare candidates on the same representative cases and rubric rather than relying on a few convincing answers.

**Tutor worked release check:** For an IT-support agent, assess groundedness, relevance, and truthful action claims. Include routine password resets, ambiguous access problems, and requests requiring refusal or escalation. Repeating one request checks consistency on that case, not coverage. Friendlier answers are not an improvement if they invent access procedures.

### G01-U04 — Explore the GenAIOps lifecycle
Source: https://learn.microsoft.com/en-us/training/modules/plan-prepare-genaiops/4-lifecycle-overview

Source fetched: 2026-11-26; page updated 2026-11-04. The lifecycle framework follows Microsoft Learn; the IT-support diagnosis and permission examples below are tutor-created conceptual applications, with no code or Azure execution.

#### Iterate from prototype to dependable service

GenAIOps builds on DevOps and MLOps for applications using language models. Managed artifacts include pretrained models, prompts, agents, and data connectors. Evaluation includes groundedness, coherence, safety, and cost per request—not accuracy alone.

| Loop | Purpose | Work |
| --- | --- | --- |
| Explore | Define what to build and why | Define the business need and design architecture, prompts, and model choices. |
| Build | Establish whether the application meets requirements | Develop and iteratively evaluate against quality and safety targets. |
| Operationalize | Deliver dependable real-world service | Deploy and operate reliably and responsibly. |

These are connected loops, not a one-way checklist. Production findings can lead back to Build for diagnosis and evaluation, or Explore for a deeper design change. Several loops may be active together.

#### Diagnose before changing prompts

**Tutor worked example:** An IT-support agent starts giving incorrect access-policy advice after an update. Reproduce the failure in Build and investigate changes to prompts, retrieved documents, and the model's use of context. Reconsider the design in Explore if needed; Operationalize handles the live-service risk, such as rolling back the problematic update.

If retrieval supplied an outdated policy and the answer faithfully followed it, fix the approved source or retrieval/indexing issue rather than assuming a prompt defect. Before release, verify both that the retrieved passage is from the current approved version and that the answer follows it with the expected guidance.

Groundedness measures support from supplied context; it does not establish that the context is current. An answer can be grounded in an outdated document.

#### Management applies throughout

The overarching **management loop** covers governance, security, and compliance across Explore, Build, and Operationalize. It is not only a final deployment gate. Passing quality and safety evaluations does not replace access controls.

**Tutor worked example:** Before connecting an agent to confidential HR documents, define permission requirements in Explore as part of the architecture. Implement and test the restrictions in Build, then maintain and monitor them in Operationalize. A grounded response can still disclose information to an unauthorized user.

### G01-U05 — Explore available tools and frameworks to implement GenAIOps
Source: https://learn.microsoft.com/en-us/training/modules/plan-prepare-genaiops/5-tools-frameworks

Source fetched: 2026-11-26; page updated 2026-11-04. Tool roles below follow Microsoft Learn; IT-support scenarios are tutor-created conceptual examples. No code or Azure execution was performed.

#### Set up resources, then explore models

**Azure Developer CLI (`azd`)** uses application templates to provision resources and deploy applications repeatably. It is a different tool from Azure CLI (`az`). **Microsoft Foundry's Chat playground** supports trying prompts against candidate models before choosing one.

A successful playground interaction establishes neither production deployment readiness nor quality across representative requests. Provisioning, application deployment, and rubric-based evaluation are separate needs.

#### Connect current information and actions

Use **RAG** for changing external facts and **fine-tuning** to adapt behavior through training examples. For friendly tone, start with prompt instructions and evaluate whether fine-tuning is needed. Neither retrieval nor fine-tuning guarantees correct answers; RAG freshness depends on current sources and the retrieval pipeline.

The unit introduces **Foundry IQ** as a managed, permission-aware knowledge layer over Azure AI Search. An **Azure AI agent** brings the model, retrieved information, and callable tools together. Retrieving instructions for an action does not provide the tool or authorization to perform it.

**Tutor example:** An IT-support agent retrieves weekly access policies and calls a ticket-creation tool. Policy freshness belongs to the source/retrieval path; actually creating a ticket requires a successful authorized tool operation.

#### Evaluate behavior and diagnose production failures

| Tool | Main role |
| --- | --- |
| Azure AI Evaluation SDK | Score responses against built-in or custom criteria, including groundedness, relevance, and tool-call accuracy. |
| ASSERT (Adaptive Spec-driven Scoring for Evaluation and Regression Testing) | Turn agent specifications into regression tests and connect failures to the request and reason. |
| Microsoft Foundry Content Safety | Detect harmful content; not a replacement for factual or task-quality evaluation. |
| Tracing, Azure Monitor, Application Insights | Capture request/tool-call context and operational signals such as latency, token usage, and errors. |

Evaluation asks whether behavior meets requirements. Observability helps establish what happened in the running service and where it failed. Production responses can feed continuous evaluation; fast, error-free responses alone do not prove answer quality.

**Tutor worked test:** If the agent says a ticket was created but none exists, inspect traces and tool results: was the tool called, did it succeed, and what result did the agent receive? Test both successful creation with an accurate ticket identifier and failed creation with a truthful failure response. Checking the real outcome is stronger than matching the words “ticket created.”

#### Separate runtime orchestration from release automation

**Microsoft Agent Framework** is an open-source SDK for Python and C# that unifies Semantic Kernel and AutoGen approaches for single- and multi-agent workflows. **LangChain** is an alternative for connecting models with data, APIs, and memory. These frameworks coordinate application behavior during user requests.

**GitHub Actions** automates engineering workflows such as testing and shipping new versions. A workflow can run ticket-creation regression tests and gate release on their results; runtime orchestration does not replace that CI/CD gate. This is a conceptual workflow, not verified configuration.

### G01-U06 — Exercise - Design agent specifications from team input
Source: https://learn.microsoft.com/en-us/training/modules/plan-prepare-genaiops/6-exercise

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this unit in lesson selection, teaching, checks, and review scheduling; it is excluded from tutor completion and TLDR readiness. No website confirmation is required.

### G01-U07 — Module assessment
Source: https://learn.microsoft.com/en-us/training/modules/plan-prepare-genaiops/7-knowledge-check

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this closing unit; it is excluded from tutor completion, review scheduling, and TLDR readiness. No website confirmation is required.

### G01-U08 — Summary
Source: https://learn.microsoft.com/en-us/training/modules/plan-prepare-genaiops/8-summary

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this closing unit; it is excluded from tutor completion, review scheduling, and TLDR readiness. No website confirmation is required.

<a id="key-concepts-and-decision-points"></a>
<a id="python-examples"></a>
<a id="javascript-examples"></a>
<a id="azure-cli-commands"></a>
<a id="related-configuration-yaml-bicep-or-github-actions"></a>
<a id="worked-examples-and-practice"></a>
<a id="common-pitfalls-and-clarifications"></a>

## Remaining study and examples

- Python, JavaScript, Azure CLI, and YAML/Bicep/GitHub Actions examples remain pending; relevance is not yet assessed. Record prerequisites, versions, expected outcomes, and execution status where applicable.

[Optional quiz history](quizzes.md)

## Microsoft Learn search terms
- GenAIOps lifecycle agent specifications
- Microsoft Foundry agent model selection
- generative AI operations tools frameworks
