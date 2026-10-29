# Study notebook conventions

## Purpose and sources

This project prepares the learner for AI-300, not AI-103. Follow `lessons/PLAN.md` and the official study guide linked in `lessons/EXAM-COVERAGE.md`. Fetch the relevant Microsoft Learn unit before teaching it; distinguish source material from learner conclusions and tutor examples. If a source is unavailable, record the limitation and do not invent its contents.

## Ownership

- `tutor` is the primary study agent and writes only `lessons/**/notes.md` and sibling `lessons/**/quizzes.md`.
- `memory-agent` is a subagent and writes only `memory/**`.
- `tldr` is a subagent and writes only `lessons/**/tldr.md`, derived from the sibling `notes.md`.
- Tutor delegates progress reads/recommendations and session updates to memory-agent via the task tool.
- Tutor delegates concise module summaries to tldr via the task tool after the completion/readiness checks below. `/tldr` also supports manual summaries.
- Shared documentation, templates, curriculum, coverage, and configuration are maintained using the build agent when the user requests changes. Study agents report needed curriculum changes rather than silently changing it.
- Study agents read `lessons/PLAN.md`, `lessons/EXAM-COVERAGE.md`, and the templates as necessary.

## IDs and progress

Module IDs are M01–M07 and G01–G06. Unit IDs append `-U` and a two-digit ordinal in displayed source order. Never derive ordinals from unit URL prefixes. Preserve IDs if source titles change; map new units explicitly when maintaining the curriculum.

`TOLEARN.md` tracks module status plus unit-level records for units actually touched. Unlisted units are `not-started`. Use exactly `not-started`, `in-progress`, and `completed`. Keep review state separate from completion. All timestamps and review dates use ISO dates; use the actual session date, not the curriculum verification date.

A tutor-study unit may be completed after a relevant exercise or a short explanation/application check demonstrates its goals. Introductions can use a short recap check. Record prompts, actual learner responses/results, feedback, and remaining gaps in the session handoff and persisted memory session. Do not imply the learner passed an official Microsoft assessment based on tutor questions. A module is completed only when all its tutor-study units have completion evidence. Deferred labs remain in progress unless an equivalent exercise demonstrates the relevant goals; label that substitute explicitly.

Closing Microsoft Learn units titled Module assessment, Knowledge check, or Summary are website-only, as listed in `lessons/PLAN.md`. Preserve their stable IDs, headings, and source links with a website-only notice. Skip them in tutor lesson selection, teaching, checks, review scheduling, completion denominators, and TLDR readiness; learners use their source links independently. Do not require website confirmation or mark these units completed merely because they are excluded. Optional tutor quizzes on studied units and generated `tldr.md` references remain available. Preserve any existing historical evidence; voluntarily reported official outcomes may be recorded as learner-reported without becoming a completion prerequisite.

## Notes and examples

Follow `templates/lesson-notes.md`. Keep each unit's ID, heading, and source link. Write a readable notebook organized by unit and concept: explanations, decision rules, worked examples, and conceptual pitfalls. Merge repeated explanations across sessions while preserving useful studied content, learner insights, source attribution, and context for corrections. Seeded learning goals are planned content, not evidence of learning; do not fill unstudied units with generic textbook content.

Keep session IDs/headings, exact learner answers, grading/scores, completion proposals, personal preferences, review schedules, and next-session recommendations in `memory/sessions/` and `memory/TOLEARN.md`, not notes. Notes may retain useful exercise tasks and worked solutions, with prerequisites and execution status, but not response histories. Express corrected misconceptions as reusable conceptual explanations rather than dated accounts of learner mistakes. Source verification dates and technical execution context may remain where relevant. Preserve historical evidence in memory before removing its only copy from notes; repair links when reorganizing headings.

Add Python, JavaScript, Azure CLI, and YAML/Bicep/GitHub Actions examples when relevant. Record SDK/CLI versions or prerequisites and expected outcomes. Distinguish illustrative code from code actually run. Mark a section `Not applicable` only after determining no relevant example exists; otherwise leave it pending. Never invent a JavaScript SDK equivalent for Python-only functionality.

## Session handoff

Use the fields in `templates/session-summary.md`: session ID/date, module and unit IDs, mode, source URLs, notes paths, topics, evidence, optional quiz participation/results, per-unit status proposals, reflections, gaps, review proposals, and next-step recommendation.

Save notebook content and applicable quizzes before handing off to memory-agent. Consolidate changes to each file into one patch operation per call, then read back the changed sections; a successful tool result is not sufficient verification. Check that studied content is under the intended unit, all intended quiz session/items and initial responses survived, counts/score agree, and linked files/anchors exist. Include the verified paths, anchors, and any blockers in the handoff. Link notes by stable unit headings for technical context; supply full ordinary lesson-check evidence in the handoff for validation and persistence in the memory session, without requiring duplicate learner answers in notes. A read/recommendation call does not update memory. Start a write handoff only for actual learner activity or an explicit correction. On a repeated handoff with the same session ID, update the existing record rather than adding duplicate evidence/reviews. If a write fails, report the failed step and retry it without claiming completion. Memory-agent verifies the summary, TOLEARN.md, and memory/sessions/README.md together, including the same session IDs and counts in both indexes.

Session filenames use `YYYY-MM-DD-session-NN.md`; ask memory-agent in read-only mode for the next unused number for the actual session date and reserve the ID in the conversation before delivering a quiz or saving any session-keyed record. Reuse that ID on retries. A read-only lookup does not reserve a file; if the ID is later found to belong to different activity, reconcile the identity before writing rather than overwriting it. Prefer due reviews, then resume unfinished units, then advance in plan order, unless the learner asks otherwise. Suggest review dates based on demonstrated gaps; 1, 3, and 7 days are useful starting intervals, not evidence of mastery.

## Optional quizzes

Tutor offers an optional quiz once at the end of an actual lesson/session and loads `lesson-quiz` only on acceptance or explicit request. The skill owns question generation/delivery/grading instructions; tutor still saves notes and memory-agent still persists memory. Quizzes have at most 10 questions, varied difficulty where appropriate, and interactive single/multiple-answer choices based on studied, verified source content.

Record initial responses, answer keys, explanations, and per-unit evidence. Multiple-answer scoring requires an exact match; skipped/invalid/unanswered items are excluded from the score denominator. Participation states are separate from unit status. A decline is not a failed check, a percentage is not mastery evidence, and tutor quizzes are not official Microsoft assessment passes. Save detailed quiz results in `quizzes.md` beside the related `notes.md`, following `templates/lesson-quizzes.md`, and preserve them in the session summary. Notes retain reusable learning takeaways and worked examples; quiz participation, item evidence, and scores belong in quizzes and memory. A single sibling quiz-history link may be included for navigation; do not add session/item evidence mappings to notes. Create quizzes.md only for actual quiz participation or a decline/unavailability during a learning session; do not seed empty histories or write learner activity for setup checks.

One optional quiz belongs to each session. Q01–Q10 are unique within that session; a resume/retry preserves the original IDs, initial responses, and total cap rather than restarting at Q01. A distinct quiz after session closure is actual new learning activity with a new reserved session ID. Use explicit HTML named anchors before quiz headings: `quiz-<session-ID>` for a session and `quiz-<session-ID>-q01` through `-q10` for items. Keep existing display headings/legacy anchors when adding these stable targets; verify links and repair references through the file owners. Declines/unavailability get a session anchor and participation record, with no fabricated items or score; an unknown historical planned count remains unknown.

## Requested maintenance and repair

For an explicit repair request, tutor may restore/reorganize its notes/quizzes and delegate `mode: maintenance/repair` to memory-agent for existing memory records and indexes. Build maintains shared instructions/templates/configuration and may repair notebook files as part of a requested maintenance change. Memory-agent remains the writer for memory. Supply repair date, target existing session IDs/files, authoritative evidence and its provenance, exact changes, and verification results/blockers. This mode does not require or create a new learning-session summary. Preserve original session dates, initial responses, keys, scores, historical corrections, and evidence before removing its only copy; do not change progress, reviews, or learning-session counts unless the user separately requested an evidenced progress correction. Preserve each original lesson/review/correction mode; record maintenance within the existing record.

Distinguish **persistence completeness** from **evidence provenance**. Backfilling a quiz from a tutor-reported memory handoff repairs its storage and links, but does not independently corroborate historical responses. Label the origin, repair date, and remaining evidentiary limits in both quiz and memory records; never claim a fresh source fetch or learner check for a backfill. If fields are missing, retain known evidence and record the limitation rather than inventing it. When a repair resolves a current blocker, update current indexes/references and retain a dated account of the original failure. Verify both sides before reporting repair complete.

## Concise module summaries

Follow `templates/lesson-tldr.md`. Summaries are derived references, not new learning or completion evidence. Use only studied content in notes.md; retain unit/source links, important decisions, corrected misconceptions, and useful existing code/CLI/configuration snippets with prerequisites and execution status. Do not invent examples, source contents, or learner mastery, and do not copy quizzes into tldr.md.

After saving the session and memory-agent confirms that every tutor-study unit in the module is completed, tutor checks the current notes for unresolved planned study, lab, and example sections within that scope. Website-only closing units are not readiness blockers. Resolve relevant examples through actual study or explicitly document why none is applicable; do not clear pending work merely to trigger a summary. Inspect current section state, including variants such as `Pending study`, `pending-study`, and `Pending assessment`; historical records of earlier gaps do not block a summary when later evidence resolves them. If ready, call tldr in automatic mode for each eligible touched module, including after later corrections/reviews change a completed module's notes. If blocked, report the remaining work and defer generation. Tldr verifies the same prerequisites before an automatic write.

Manual `/tldr <notes-path>` can summarize an unfinished module; label it partial and list remaining work. Refresh the existing generated file rather than appending duplicate summaries, preserve clearly marked user-authored additions, and report any persistence failure. Summary generation alone never creates a memory session or changes learning progress.
