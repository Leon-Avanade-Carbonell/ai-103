# AI-300 AI-Assisted Study Notebook

A Markdown study notebook for **Microsoft Certified: Machine Learning Operations Engineer Associate**, supported by an interactive OpenCode tutor, a memory subagent, and a concise-summary subagent.

The certification target is **AI-300**. The existing `ai-103` directory name is retained.

## Start studying

1. Quit and restart OpenCode after installing or changing project configuration, agents, or skills.
2. From this directory, run `opencode --agent tutor` (the tutor is also the project default).
3. Say **“Start my next lesson”**, **“Review what is due”**, or **“Resume my current lesson.”**
4. When finished, say **“End the session and save my notes and progress.”**

The tutor asks `memory-agent` for your next lesson, teaches a Microsoft Learn unit interactively, updates its module notes and applicable quizzes, and hands the session evidence back to `memory-agent`. The memory subagent updates progress and saves a dated session summary. Once a module is completed and its notes are ready, tutor delegates a concise reference to `tldr`. Your existing OpenCode provider/model configuration is used.

No lessons are marked learned initially. The first session begins with a short prerequisite check and `M01-U01`.

Closing **Module assessment / Knowledge check** and **Summary** units are website-only. Use their Microsoft Learn links in the notes independently; the tutor skips them and requires no website confirmation. Across 13 modules, the plan contains **84 tutor-study units** and **26 website-only closing units** (110 official source units).

## Optional lesson quizzes

At the end of a lesson/session, the tutor offers **Short quiz (up to 5 questions)**, **Full quiz (up to 10 questions)**, or **Skip quiz**. You can also say **“Quiz me on this session with 7 questions.”**

On acceptance, the tutor loads [the lesson-quiz skill](.opencode/skills/lesson-quiz/SKILL.md). It asks one multiple-choice question at a time, mixing single/multiple-answer formats and easy, medium, and hard questions when appropriate to the material studied. Multiple-answer questions state how many answers to select. Each response receives an explanation; type **skip** or **stop** to skip an item or end early.

Detailed results are saved in **quizzes.md beside the related notes.md** and preserved in the memory session summary. Notes retain reusable explanations and worked examples; exact lesson-check responses, feedback, and progress evidence go in memory sessions. Multiple-answer questions require the exact correct set for credit. Skipped/invalid/unanswered items are reported separately; the score is correct / valid answered questions. Declining the quiz does not override understanding demonstrated through other exercises or checks. These are tutor-created practice questions.

## Concise lesson references

The `tldr` subagent generates **tldr.md beside notes.md**, highlighting important concepts, decisions, pitfalls, source pointers, and useful existing code/CLI/configuration snippets with their prerequisites and execution status.

Tutor automatically requests a summary after memory-agent confirms all tutor-study units in the module are completed, and the current notes have no unresolved planned study, lab, or example work within that scope. Website-only closing units do not block generation. Relevant examples must be studied or explicitly addressed as not applicable; historical resolved gaps do not block generation. Later corrections/reviews refresh eligible summaries.

For a manual summary, run:

```text
/tldr lessons/01-mlops/01-get-started-with-machine-learning/notes.md
```

With no path, `/tldr` uses your current module when it can identify it. Unfinished modules receive a **Partial** summary with remaining work. Summaries derive only from studied notes and never update learning progress. Refreshing preserves clearly marked user-authored additions, such as a `## User additions` section.

## Project structure

```text
.
├── README.md
├── AGENTS.md                     # Shared study conventions and ownership
├── opencode.json                 # Tutor as the default primary agent
├── .opencode/agents/
│   ├── tutor.md
│   ├── memory-agent.md
│   └── tldr.md
├── .opencode/commands/
│   └── tldr.md                   # Manual /tldr command
├── .opencode/skills/
│   └── lesson-quiz/
│       └── SKILL.md              # Question generation, delivery, and grading
├── memory/
│   ├── TOLEARN.md                # Progress, reflections, gaps, and review queue
│   └── sessions/                # Dated learning evidence
├── templates/
│   ├── lesson-notes.md
│   ├── lesson-quizzes.md
│   ├── lesson-tldr.md
│   └── session-summary.md
└── lessons/
    ├── PLAN.md                   # Two learning paths, 13 modules, 110 units
    ├── EXAM-COVERAGE.md          # Objective mapping and supplemental backlog
    ├── 01-mlops/                # Seven module directories, each with notes.md
    └── 02-genaiops/              # Six module directories, each with notes.md
```

Open [the lesson plan](lessons/PLAN.md), [exam coverage](lessons/EXAM-COVERAGE.md), or [your learning memory](memory/TOLEARN.md).

Chapters follow learning paths; subchapters follow modules. Each module's `notes.md` has a separate heading and source URL for every Microsoft Learn unit page. Notes read like a notebook: topic-organized explanations, decision rules, Python/JavaScript examples where relevant, Azure CLI, configuration, worked exercises, conceptual pitfalls, and Microsoft Learn search terms. Later sessions enrich the relevant topics rather than adding session logs.

`memory/sessions/` preserves dated prompts, actual learner responses, feedback, reflections, and progress decisions. `memory/TOLEARN.md` tracks personal progress, preferences, gaps, reviews, and next steps. Quiz history goes in sibling `quizzes.md` when applicable; generated concise references go in sibling `tldr.md`.

## Tracking conventions

- Module IDs: `M01`–`M07` for MLOps; `G01`–`G06` for GenAIOps.
- Unit IDs: `M01-U01`, `G02-U07`, etc., following displayed page order rather than Microsoft's sometimes irregular URL numbering.
- Status: `not-started`, `in-progress`, or `completed`; review needs are tracked separately.
- Tutor-study completion requires recorded explanation/application-check or exercise evidence. Reading alone does not imply completion. Module completion covers all tutor-study units; website-only closing units are excluded rather than marked completed.
- `lessons/PLAN.md` defines the curriculum; `memory/TOLEARN.md` records personal progress.
- Supplemental topics in the coverage file require verified sources before adding lesson folders and IDs.

## Official resources

- [AI-300 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-300)
- [Certification](https://learn.microsoft.com/en-us/credentials/certifications/operationalizing-machine-learning-and-generative-ai-solutions/)
- [Course AI-300T00](https://learn.microsoft.com/en-us/training/courses/ai-300t00)
- [Operationalize machine learning models (MLOps)](https://learn.microsoft.com/en-us/training/paths/build-first-machine-operations-workflow/)
- [Operationalize generative AI applications (GenAIOps)](https://learn.microsoft.com/en-us/training/paths/operationalize-gen-ai-apps/)

Curriculum links and unit lists verified on **2026-10-28**. Recheck official sources when curriculum or exam objectives change.
