---
description: Summarize module notes into sibling tldr.md; unfinished modules receive a partial summary.
agent: tldr
subtask: true
---

Generate or refresh a concise module reference in `mode: manual` using the tldr agent instructions and `templates/lesson-tldr.md`.

Requested notes path: $ARGUMENTS

Use the specified existing `lessons/**/notes.md`; if no path is supplied, resolve the current module from memory/TOLEARN.md or request clarification if ambiguous. Write only sibling tldr.md. Derive content from studied notes, preserve existing useful snippets and their prerequisites/execution status, and link important concepts to units and sources. Label unfinished work Partial and list what remains. Preserve clearly marked user additions. Do not create a learning session or update progress. Return the saved path or the specific blocker.
