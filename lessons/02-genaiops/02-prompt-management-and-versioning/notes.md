# Manage prompts for agents in Microsoft Foundry with GitHub

- Module ID: G02
- Source: https://learn.microsoft.com/en-us/training/modules/prompt-versioning-genaiops/
- Curriculum verified: 2026-10-28
- Exam objectives: D3 prompt versioning and source control.

## Overview and learning goals

Planned source goals: manage prompts as versioned code assets, understand Foundry agent/prompt integration, organize a GitHub repository, and design safe testing/deployment workflows.

## Notes by Microsoft Learn unit

### G02-U01 — Introduction
Source: https://learn.microsoft.com/en-us/training/modules/prompt-versioning-genaiops/1-introduction

Source fetched: 2026-11-26; page updated 2026-11-04. The safeguards below follow the Microsoft Learn introduction; the regression-test example is tutor-created and illustrative, not executed.

#### Treat prompt edits as behavior changes

A system prompt is a software asset: editing its wording can change an agent's production behavior. In the source scenario, a friendlier support prompt led to inconsistent technical responses, and the team could not identify the change or quickly restore the working prompt.

Four safeguards address different risks:

- **Version control:** track what changed and recover an earlier version.
- **Approval workflows:** review proposed changes before release.
- **Testing:** check whether a change harms important behaviors.
- **Knowledge management:** preserve context and reasoning rather than relying on memory.

Git makes changes traceable; it does not establish their quality. Likewise, rollback restores a selected version, not proof of accuracy. Quality can differ between versions and needs supporting test evidence.

#### Test behavior, not just wording

**Tutor example:** A friendlier prompt passes review but starts inventing troubleshooting steps. A regression test could ask about a known software error and check that the steps match approved documentation. Approval alone does not demonstrate technical accuracy.

**Learner-suggested design measures:** grounding through RAG and prompt guardrails can help constrain responses. Using RAG does not itself guarantee grounded answers; test whether the agent uses retrieved evidence correctly and avoids unsupported instructions.

### G02-U02 — Apply version control to prompts
Source: https://learn.microsoft.com/en-us/training/modules/prompt-versioning-genaiops/2-version-control-for-prompts

Source fetched: 2026-11-26; page updated 2026-11-04. The DevOps safeguards follow Microsoft Learn; the deployment path and password regression test below are illustrative tutor examples, not executed.

#### Keep deployed prompts aligned with approved versions

A prompt is production configuration: its wording influences accuracy, tone, safety, and cost. No compilation step is needed for an edit to affect behavior when the running agent uses the updated prompt.

| Safeguard | Purpose |
| --- | --- |
| Git version history | Identify changes, preserve their rationale, and recover earlier text. |
| Review before deployment | Examine the intended behavior change and the complete diff. |
| Separate development and production | Validate a candidate before exposing production users. |
| Rollback capability | Restore a previously deployed working configuration. |

Storing a prompt in GitHub is insufficient if someone can independently edit the live prompt in Foundry. Development and production can then use different configurations: **environment drift**. Git should be the authoritative source for the release process; the agent need not fetch the prompt from GitHub at runtime. A deployment workflow can read the approved revision and configure the agent.

**Tutor deployment example:** edit on a branch → pull request and review → validate in development → deploy the approved version. Record the deployed Git revision for traceability. Direct production edits bypass this path; restoring a Git file alone does not necessarily update the live agent.

#### Review behavior and preserve intent

Review both regression results and everything included in the PR. No failed tests is not proof of safety when the suite misses the behavior affected by the change.

**Tutor test example:** before removing “Never request a customer's password,” check that the agent does not request credentials even when a user offers to share them. This tests a safety behavior rather than merely checking the prompt's wording. The reviewer should also inspect why the instruction existed and whether the tests cover that risk.

Commit messages and PR explanations preserve **why** a safeguard exists, helping prevent lost knowledge. Version history supports recovery and diagnosis; testing assesses quality. Neither version control nor rollback alone establishes accuracy or safety.

### G02-U03 — Understand Microsoft Foundry agents and prompt versioning
Source: https://learn.microsoft.com/en-us/training/modules/prompt-versioning-genaiops/3-foundry-agents-prompt-versioning

Source fetched: 2026-11-26; page updated 2026-11-04. Agent components, prompt storage options, and version comparisons follow Microsoft Learn. Hiking scenarios and release-traceability guidance below are illustrative tutor examples, not executed.

#### Version the configuration, not only the prompt

An agent combines its name and metadata, system instructions, selected model, and optional tools. Identical prompt files do not imply identical agents: changing the model or tools can change behavior. Even an unchanged configuration can produce different individual responses; one comparison does not establish configuration drift.

**Tutor example:** adding a weather tool to a hiking assistant changes its access to current forecasts without changing its prompt. Tool availability does not guarantee correct tool use.

Git revisions identify source configurations; deployed agent versions identify configurations available in Foundry. Associate a deployed version with the approved Git revision containing its prompt and deployment configuration. A filename such as `v2_instructions.txt` is not proof of what is running.

#### Compare versions under controlled conditions

Use the same test requests across candidate versions to compare relevant quality and safety behaviors and identify regressions. To isolate a prompt change, keep the model, tools, and test conditions consistent. Define acceptance thresholds before promotion; a higher aggregate quality score must not hide a failed required safety check.

**Tutor example:** a hiking prompt offers better personalization but omits essential safety guidance. Hold back promotion if that omission fails a release requirement, even if other scores improve.

#### Separate prompt review from deployment logic

| Storage approach | Useful when |
| --- | --- |
| Prompt strings embedded in Python | A small project prioritizes simplicity. |
| Separate `.txt` or `.md` files | Reviewers need readable prompt-only diffs without inspecting deployment code. |
| YAML or JSON configuration | Releases need structured metadata and configuration. |

A `prompts/` folder in GitHub can serve as a simple prompt library. The deployment process reads the selected instructions and configures the agent; Git tracks both prompt content and deployment logic. Proposed, untested changes can be committed on a branch; review and testing gate release, not initial storage.

**Learner-derived design consideration:** separating these files separates prompt-review concerns from deployment-script concerns. Readable files do not solve missing GitHub permissions or unfamiliarity with its workflow; reviewers still need an accessible process and appropriate access. A library organizes prompts, while Git supplies committed change history.

The source includes a Python SDK deployment illustration. Its API/package compatibility was not verified and the code was not run; a supported deployment recipe remains pending rather than being presented as executable guidance.

### G02-U04 — Organize prompts in GitHub repositories
Source: https://learn.microsoft.com/en-us/training/modules/prompt-versioning-genaiops/4-github-repository-structure

Source fetched: 2026-11-26; page updated 2026-11-04. Format choices and repository organization follow Microsoft Learn; the simplified layout and deployment-evidence clarification below are tutor examples, not executed.

#### Separate instructions, configuration, and documentation

Choose the simplest format that meets the need:

| Need | Suitable format |
| --- | --- |
| Simple, static system instructions | `.txt` |
| Instructions with headings and lists | `.md` |
| Structured deployment settings and metadata | `.yaml` or `.json` |
| Dynamic content with substitutions | A template, such as Jinja2 |

Markdown is useful for human-readable deployment guides; YAML or JSON fits named settings that deployment code must parse, such as model selection and a prompt-file path. Deployment code must read the file and supply the intended instructions or parse its configuration: an extension alone does not configure Foundry. Readable prompt files also do not grant reviewers repository access.

#### Make related assets easy to find

Group each agent's prompts beside its deployment script, while separating source, behavior tests, infrastructure, and documentation. Consistent, descriptive names make ownership and purpose clear; the exact folder names are less important than those relationships.

Simplified tutor layout; no runtime prerequisites or execution involved:

```text
src/
  agents/
    support_agent/
      deploy.py
      prompts/
        instructions.txt
tests/
  test_support_agent.py
docs/
  prompt-guidelines.md
.github/
  workflows/
    test-agents.yml
    deploy-agents.yml
```

This layout lets reviewers inspect instructions separately from deployment logic and find the tests that protect behavior. It illustrates organization, not an implemented deployment workflow.

#### Connect Git revisions to actual deployments

The source illustrates versioned prompt filenames and Git tags for release tracking. A filename identifies a prompt file, a tag identifies a repository revision, and a deployed agent version identifies a configuration available in Foundry. Their relationship must be recorded rather than assumed from matching version numbers.

**Tutor application:** if `v3_instructions.txt` exists in GitHub but production still uses version 2, verify the production agent version and its recorded mapping to the Git revision containing the deployed prompt and configuration. A filename, tag, or README statement alone is not deployment evidence. Creating a tag does not deploy an agent; checking out an old tag does not by itself roll back the running agent.

### G02-U05 — Develop safe prompt deployment workflows
Source: https://learn.microsoft.com/en-us/training/modules/prompt-versioning-genaiops/5-prompt-workflow-development

Source fetched: 2026-11-26; page updated 2026-11-04. Lifecycle stages follow Microsoft Learn; deployment-evidence and rollback scenarios below are illustrative tutor applications, not executed.

#### Isolate development in Git and in the target environment

Use development for experimentation with representative inputs; production serves real users and receives validated, approved changes. Progress through draft → test → refine → validate → review → deploy → monitor.

A feature branch isolates repository changes, not the running agent. A deployment script run from that branch must target a development agent to avoid exposing production users to unvalidated changes. Updating production outside the approved release path can also create environment drift: the live configuration diverges from the approved, recorded configuration.

#### Validate behavior, then approve the release

Validation checks functional, quality, and performance requirements against defined baselines. Review examines the diff, rationale, and test evidence and grants release approval. Passing tests does not grant approval; approval does not establish quality.

**Tutor example:** a shorter support prompt improves average quality but starts requesting passwords. A required safety-check failure should block promotion despite the higher aggregate score.

After approval, merge, tag for traceability, and deploy the approved configuration. A merge or tag does not itself update production unless an explicitly configured workflow performs deployment. Begin automation with behavior tests; add deployment, monitoring alerts, and rollback as the workflow matures.

#### Verify production and retain a live rollback path

If production still uses the old prompt, inspect whether the deployment workflow ran, passed its gates, authenticated successfully, and targeted the intended agent. Check both deployment logs and the production configuration/version mapped to the approved Git revision. A successful test job alone is not deployment evidence.

Monitor production behavior against release baselines. A deployment can succeed technically while its prompt degrades response quality. Restore the previous approved live configuration while investigating a serious regression; reverting the Git file alone does not update the running agent.

**Learner-suggested rollback architecture:** route users back to blue if the application has separately deployed blue/green configurations and routing controls. This is conditional application-level architecture, not a built-in Foundry blue/green workflow established by this unit. Retain a usable previous deployment before relying on that rollback route.

### G02-U06 — Exercise - Develop prompt and agent versions
Source: https://learn.microsoft.com/en-us/training/modules/prompt-versioning-genaiops/6-exercise

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this unit in lesson selection, teaching, checks, and review scheduling; it is excluded from tutor completion and TLDR readiness. No website confirmation is required.

### G02-U07 — Knowledge check
Source: https://learn.microsoft.com/en-us/training/modules/prompt-versioning-genaiops/6-knowledge-check

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this closing unit; it is excluded from tutor completion, review scheduling, and TLDR readiness. No website confirmation is required.

### G02-U08 — Summary
Source: https://learn.microsoft.com/en-us/training/modules/prompt-versioning-genaiops/7-summary

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this closing unit; it is excluded from tutor completion, review scheduling, and TLDR readiness. No website confirmation is required.

<a id="key-concepts-and-decision-points"></a>
<a id="python-examples"></a>
<a id="javascript-examples"></a>
<a id="azure-cli-commands"></a>
<a id="related-configuration-yaml-bicep-or-github-actions"></a>
<a id="worked-examples-and-practice"></a>
<a id="common-pitfalls-and-clarifications"></a>

## Remaining study and examples

- G02-U05: independent confirmation of deployed-revision checks and why a Git-only revert does not restore production would strengthen transfer; these details were supplied in feedback. Practical workflow implementation remains unverified.
- G02-U03: verify a current supported SDK deployment example, including agent-version behavior, authentication, package requirements, and expected outcome. Practical deployment remains unverified.
- Python, JavaScript, Azure CLI, and YAML/Bicep/GitHub Actions examples remain pending; relevance is not yet assessed. Record prerequisites, versions, expected outcomes, and execution status where applicable.

## Microsoft Learn search terms
- Microsoft Foundry prompt versioning GitHub
- prompts as code repository structure
- prompt variants deployment testing workflows

[Optional quiz history](quizzes.md)
