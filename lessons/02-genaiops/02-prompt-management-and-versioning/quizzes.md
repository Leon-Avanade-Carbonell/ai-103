# Quizzes — Manage prompts for agents in Microsoft Foundry with GitHub

- Module ID: G02
- Notes: [Lesson notes](notes.md)
- Source: https://learn.microsoft.com/en-us/training/modules/prompt-versioning-genaiops/
- Evidence identity: session ID plus question ID; one optional quiz per session.

Tutor-created formative quizzes, not official Microsoft assessments.

## Quiz history

<a name="quiz-2026-11-26-session-08"></a>

### Optional tutor quiz — 2026-11-26-session-08

- Date: 2026-11-26
- Units: [G02-U01 — Introduction](notes.md#g02-u01--introduction)
- Verified source: https://learn.microsoft.com/en-us/training/modules/prompt-versioning-genaiops/1-introduction (fetched 2026-11-26)
- Participation: declined; learner selected **Skip quiz** when offered the optional end-of-lesson quiz.
- Requested/planned: not applicable; no quiz count selected.
- Presented / valid answered: 0 / 0.
- Count scope: this session covered G02 only. No quiz items or score.
- Evidence provenance: current-conversation question-tool response. The ordinary lesson checks are separate evidence retained in the memory session.

<a name="quiz-2026-11-26-session-09"></a>

### Optional tutor quiz — 2026-11-26-session-09

- Date: 2026-11-26
- Units: [G02-U02 — Apply version control to prompts](notes.md#g02-u02--apply-version-control-to-prompts)
- Verified source: https://learn.microsoft.com/en-us/training/modules/prompt-versioning-genaiops/2-version-control-for-prompts (fetched 2026-11-26)
- Participation: declined; learner selected **Skip quiz** when offered the optional end-of-lesson quiz.
- Requested/planned: not applicable; no quiz count selected.
- Presented / valid answered: 0 / 0.
- Count scope: this session covered G02 only. No quiz items or score.
- Evidence provenance: current-conversation question-tool response. Ordinary lesson checks are separate evidence retained in the memory session; this decline does not imply a blanket preference.

<a name="quiz-2026-11-26-session-10"></a>

### Optional tutor quiz — 2026-11-26-session-10

- Date: 2026-11-26
- Units: [G02-U03 — Understand Microsoft Foundry agents and prompt versioning](notes.md#g02-u03--understand-microsoft-foundry-agents-and-prompt-versioning)
- Verified source: https://learn.microsoft.com/en-us/training/modules/prompt-versioning-genaiops/3-foundry-agents-prompt-versioning (fetched 2026-11-26)
- Participation: declined; learner replied “no” to the optional end-of-lesson quiz offer.
- Requested/planned: not applicable; no quiz count selected.
- Presented / valid answered: 0 / 0.
- Count scope: this session covered G02 only. No quiz items or score.
- Evidence provenance: current-conversation learner response. Ordinary lesson checks are separate evidence retained in the memory session; this decline does not imply a blanket preference.

<a name="quiz-2026-11-26-session-11"></a>

### Optional tutor quiz — 2026-11-26-session-11

- Date: 2026-11-26
- Units: [G02-U04 — Organize prompts in GitHub repositories](notes.md#g02-u04--organize-prompts-in-github-repositories)
- Verified source (S): https://learn.microsoft.com/en-us/training/modules/prompt-versioning-genaiops/4-github-repository-structure (fetched 2026-11-26; updated 2026-11-04).
- Participation: completed.
- Requested/planned: Short quiz (up to 5) / 4 questions; narrowed to studied scope.
- Presented / valid answered: 4 / 4.
- Correct / incorrect / skipped / invalid / unasked or unanswered: 4 / 0 / 0 / 0 / 0.
- Score: 4/4.
- Difficulty mix: 1 easy, 3 medium; exact-set scoring for the multiple-answer item.
- Count scope: session-wide and G02-local counts are identical; only G02-U04 was quizzed.
- Evidence provenance: current-conversation question-tool selections; no retries or practical execution reported. Questions are tutor-created from S and the studied deployment-traceability application.

<a name="quiz-2026-11-26-session-11-q01"></a>

#### Q01 — Simple instruction format; easy; single-answer; G02-U04; S

Prompt: A team needs simple, static system instructions with no metadata or variable substitution. Which format is the simplest suitable starting point? Select one answer.
- A. JSON — Store the instructions in a structured object.
- B. Plain text (.txt) — Store the instructions as text.
- C. Jinja2 — Store the instructions in a template.

Initial learner selections: B. Plain text (.txt).
Correct set: B.
Outcome: correct.
Explanation: Plain text meets the need without extra structure. JSON supports structured data; Jinja2 supports substitutions, neither required here. Source: S.

<a name="quiz-2026-11-26-session-11-q02"></a>

#### Q02 — Asset organization; medium; multiple-answer; G02-U04; S

Prompt: Which repository organization choices support finding and reviewing an agent's assets? Select two answers.
- A. Group prompts by agent — Put each agent's prompts beside its deployment script.
- B. Embed tests in prompt files — Keep automated test code inside system instructions.
- C. Separate tests from source — Keep behavior tests in a dedicated tests directory.
- D. Combine all agents' files — Put every prompt and script into one undifferentiated folder.

Initial learner selections: A. Group prompts by agent; C. Separate tests from source.
Correct set: A, C.
Outcome: correct (exact set).
Explanation: Grouping related assets aids discovery and separating tests clarifies their purpose. B mixes executable tests with agent instructions; D obscures ownership and relationships. Source: S.

<a name="quiz-2026-11-26-session-11-q03"></a>

#### Q03 — Structured deployment configuration; medium; single-answer; G02-U04; S

Prompt: Engineers need deployment code to read a model identifier and a prompt-file path as named configuration fields. Which format best fits that requirement? Select one answer.
- A. Markdown deployment guide — Describe the settings in documentation prose.
- B. Plain instruction text — Mix the settings into the system prompt.
- C. YAML or JSON — Represent the settings as structured configuration.

Initial learner selections: C. YAML or JSON.
Correct set: C.
Outcome: correct.
Explanation: YAML or JSON provides named fields for deployment code to parse. A is documentation for people; B mixes deployment settings with agent instructions. Source: S.

<a name="quiz-2026-11-26-session-11-q04"></a>

#### Q04 — Release traceability; medium; single-answer; G02-U04; S

Prompt: A release tag points to a Git revision containing a new prompt. What is the strongest evidence that production uses that release? Select one answer.
- A. The prompt's filename — Its filename contains the latest version number.
- B. A verified deployment mapping — The production agent version is linked to that revision and its deployed configuration.
- C. The tag's existence — The release tag is visible in GitHub.
- D. A documentation update — The README calls the new prompt the production version.

Initial learner selections: B. A verified deployment mapping.
Correct set: B.
Outcome: correct.
Explanation: A verified mapping connects the running agent to released source and configuration. A filename, tag, or README statement alone does not demonstrate what was deployed. Source: S, with the tutor's studied deployment-evidence clarification.

Strengths: appropriate format selection (Q01, Q03), asset separation (Q02), and release traceability (Q04).
Misconceptions and remaining gaps: no unresolved misconception demonstrated in this quiz. Practical deployment is unverified; G02-U03's supported SDK recipe and other module examples remain pending, separately from this quiz.
Review proposals: no new gap-specific review; existing reviews remain separate.

<a name="quiz-2026-11-26-session-12"></a>

### Optional tutor quiz — 2026-11-26-session-12

- Date: 2026-11-26
- Units: [G02-U05 — Develop safe prompt deployment workflows](notes.md#g02-u05--develop-safe-prompt-deployment-workflows)
- Verified source: https://learn.microsoft.com/en-us/training/modules/prompt-versioning-genaiops/5-prompt-workflow-development (fetched 2026-11-26; updated 2026-11-04).
- Participation: declined; learner selected **Skip quiz** in the question tool.
- Requested/planned: not applicable; no quiz count selected.
- Presented / valid answered: 0 / 0.
- Count scope: session-wide and G02-local counts are identical. No quiz items or score.
- Evidence provenance: current-conversation question-tool response. Ordinary application-check answers are retained separately in the memory session; this decline is not a failed check or blanket preference.
