---
name: lesson-quiz
description: Use when the learner accepts an optional end-of-lesson or session quiz, or explicitly requests a quiz on studied AI-300 units. Generates and delivers up to 10 source-grounded multiple-choice questions and summarizes learning evidence.
---

# Lesson quiz

The tutor loads this skill after quiz acceptance and runs it in the same conversation. It is not a subagent. Follow AGENTS.md; the tutor owns lesson notes and sibling quizzes.md files and delegates memory persistence to memory-agent.

## Inputs and scope

Use the learner's selected question count, session module/unit IDs, topics actually studied, verified Microsoft Learn unit content/URLs, existing notes, and observed gaps. Default to 5 questions for a short quiz or 10 for a full quiz. Honor a custom positive integer, capped at 10. Clarify invalid counts before starting.

Require a session ID reserved through a read-only memory-agent lookup before delivering questions or saving session-keyed evidence. Use one optional quiz per session; Q01–Q10 are unique within it. Resume/retry the same quiz without resetting initial responses, question IDs, or the total cap. A distinct quiz after session closure requires a new reserved ID for that actual learning activity, not a repair session.

If the learner has already requested a quiz, treat that as acceptance; do not offer it again. Otherwise the tutor offers Short quiz (up to 5), Full quiz (up to 10), or Skip quiz through the question tool. Skipping is optional participation, not a failed assessment or a new knowledge gap.

Quiz only the studied units and concepts. Fetch relevant source pages if their content is not already available in the conversation. Existing learner notes alone are not authoritative for technical answer keys. If a source is unavailable, use previously fetched content or learner-supplied source text and record the limitation; otherwise exclude that topic. If no grounded questions can be produced, explain why and return `unavailable` without assigning a score.

## Generate a question set

1. Produce at most the selected count and never more than **10 questions per quiz**. Use fewer for a narrow lesson rather than padding with repetition. Tell the learner the actual count and intended difficulty mix.
2. Vary difficulty where the covered material supports it:
   - Easy: concepts, definitions, or recognition.
   - Medium: applying a concept or choosing an appropriate service/configuration.
   - Hard: scenario tradeoffs, troubleshooting, or interpreting code/CLI/configuration.
   - A full quiz can aim for 3 easy, 4 medium, and 3 hard; smaller quizzes should include a mix when relevant. Do not introduce untaught topics to manufacture difficulty.
3. Mix single-answer and multiple-answer questions when the material supports both. Use 3–5 plausible choices with short stable labels such as `A. <choice>` and neutral descriptions. Avoid ambiguous stems, trick wording, implausible distractors, and cues from option length/position. Vary correct-answer positions.
4. Decide the correct answer set, explanation, unit ID(s), concept/goal, difficulty, and source URL(s) before presenting each question. For multiple-answer items, have at least two correct options and at least one incorrect option. State the number to select explicitly. Do not display answer keys, explanations, hints, or correctness cues before the learner answers.
5. Check that each key follows from the cited material and that alternatives are incorrect under the stated scenario. Reword or drop an ambiguous item. Feedback on an earlier question must not give away a later question; revise later items if needed within the original count.

## Deliver interactively

- Use the question tool, one question per call, and wait for its returned learner selection before continuing. Do not batch the whole quiz.
- Include `Question n/N`, difficulty, and `Select one answer` or `Select two/three answers` in the question text. Use a short header such as `Quiz 1/5`.
- For a single-answer item, set `multiple: false`; for a multiple-answer item, set `multiple: true`. Pass the choice labels/descriptions in `options`. Do not mark an option Recommended or reveal correctness in its description.
- Explain at the start that the learner may type **skip** or **stop** using the tool's custom-answer option or send those messages in chat. Do not add Skip/Stop as selectable choices to a multiple-answer item, where they could be selected alongside answers.
- Match returned labels to their stable option letters. A custom response consisting of letters can be graded if unambiguous. If the response is unclear, request clarification without revealing the key; never infer an answer from silence, a dismissed prompt, or tool failure.
- `skip` records the item as skipped and moves on. `stop` ends immediately; the current unanswered item and remaining items stay unasked/unanswered. A cancellation or tool failure pauses/ends the quiz without inventing responses. Honor an early-stop request rather than pushing to reach the planned count.

## Grade and explain

- Single-answer: correct only when the selected answer matches the key.
- Multiple-answer: use exact-set scoring. All correct choices and no incorrect choices are required for one point; otherwise zero. Explain missing correct choices and incorrectly selected distractors. No partial credit.
- After a valid answer, state correct/incorrect, reveal the key, and briefly explain why each choice fits or does not fit. Tie feedback to the source and the lesson concept. Then proceed to the next question.
- Preserve the initial scored response if the learner retries after feedback; record retries separately as follow-up learning, not as replacements that inflate the original score.
- If an item is discovered to be ambiguous or its key unsupported, mark it invalid, explain the correction, and exclude it from the score. Do not penalize the learner or silently change the key to match their answer.

## Summarize and return evidence

At the end, report correct / valid answered questions, incorrect count, skipped count, invalid count, and unasked/unanswered count against the planned total. The score denominator includes only valid answered items; if it is zero, report **No scored answers**, not 0% or a pass/fail. Label a stopped quiz partial so a small answered subset is not presented as full-quiz mastery.

Use this evidence format in a session-dated section of **quizzes.md** beside the related module notes, following `templates/lesson-quizzes.md`, and in the **Optional lesson quiz** section of the session summary. Notes.md retains reusable learning takeaways and worked examples, with at most a sibling quiz-history navigation link. Keep quiz participation, session/item mappings, questions, choices, keys, responses, and scores in quizzes and memory; ordinary lesson-response histories also belong in memory:

- Participation: `completed` when the planned set was delivered and each presented item answered/skipped/invalidated; `partial` when stopped, paused, cancelled, or interrupted before finishing; `declined` when the learner skips the offer; `unavailable` when accepted but no grounded questions can be produced; or `not-offered` when no offer/request occurred. These are quiz states, separate from unit status.
- Requested/planned count; presented count; valid answered count; correct/incorrect, skipped, invalid, and unasked/unanswered counts.
- Score: `<correct>/<valid answered>` or `No scored answers`.
- Per item: stable ID `Q01`…`Q10` within the session quiz, unit IDs, topic/goal, difficulty, single/multiple-answer type, full question and labeled choices, initial learner selections, correct answer set, outcome (`correct`, `incorrect`, `skipped`, `invalid`, or `unanswered`), explanation, and source URLs. Record actual presented items; do not fabricate responses for remaining questions.
- Stable links: insert `<a name="quiz-<session-ID>"></a>` before the session heading and `<a name="quiz-<session-ID>-qNN"></a>` before each presented item heading, using lowercase qNN. Link these explicit targets from memory; preserve existing headings/legacy links when migrating. Declines/unavailability have a session target only.
- Strengths, misconceptions, follow-up explanation/exercise results, and proposed reviews linked to item/unit IDs. Link back to the related notes unit headings. If a quiz spans modules, save each module's applicable items in its sibling quizzes.md and reference every quizzes file from the single session summary. Preserve original session/question IDs; label session-wide counts separately from module-local counts so memory-agent does not multiply totals.

Return this evidence to the tutor for normal save-and-handoff processing. Tutor saves notes and applicable quizzes.md before memory-agent receives the update. Append a new session section or update the same session on retries without duplicate items; preserve initial responses and historical corrections. Create quizzes.md only after learner participation or a decline/unavailability during an actual learning session; configuration verification is not learning activity. A declined/unavailable quiz has no item evidence or score.

Consolidate edits to each file into one patch operation per call, then read back the saved session/items. Verify participation, all presented IDs and initial selections, keys/outcomes, counts/score, existing content preservation, and local link targets. Repair and reverify before handoff; report a named blocker if any required record cannot be saved. A tool success message alone is not proof. Preserve supplied evidence and distinguish incomplete persistence from a learner gap.

For explicitly requested historical backfills, follow AGENTS.md's maintenance workflow rather than generating or administering a quiz. Preserve the original session/item IDs, dates, prompts, choices and initial responses as recorded; label origin and repair date. Unknown historical fields remain unknown. Copying tutor-reported handoff details repairs persistence, not independent evidence corroboration; retain that limitation in quizzes and the memory maintenance handoff. Do not create a learning session or change progress/reviews for the repair.

Questions are tutor-created formative checks, not an official Microsoft assessment. A score alone neither completes units nor reopens completed ones; assess the goals actually demonstrated and unresolved gaps alongside other session evidence. Declining an optional quiz does not override understanding already demonstrated through relevant checks/exercises. Deferred practical labs still need goal-equivalent exercise evidence.
