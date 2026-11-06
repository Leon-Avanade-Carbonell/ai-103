# Quizzes — Perform hyperparameter tuning with Azure Machine Learning

- Module ID: M04
- Notes: [Lesson notes](notes.md)
- Source: https://learn.microsoft.com/en-us/training/modules/perform-hyperparameter-tuning-azure-machine-learning-pipelines/
- Evidence identity: session ID plus question ID; one optional quiz per session, Q01–Q10 unique within that session.

Tutor-created formative quizzes are not official Microsoft assessments. Ordinary lesson checks are recorded in memory, separately from optional quiz participation.

## Quiz history

<a name="quiz-2026-11-05-session-06"></a>

### Optional tutor quiz — 2026-11-05-session-06

- Date: 2026-11-05
- Units: [M04-U01 — Introduction](notes.md#m04-u01--introduction)
- Verified source: https://learn.microsoft.com/en-us/training/modules/perform-hyperparameter-tuning-azure-machine-learning-pipelines/1-introduction (fetched 2026-11-05).
- Participation: declined. The learner selected **Skip quiz** from the end-of-lesson offer.
- Requested/planned questions: Not applicable; no quiz accepted or planned.
- Presented / valid answered: 0 / 0.
- Count scope: M04 only; also the entire session's optional quiz.
- Evidence provenance: current-session choice recorded through the question tool. No optional quiz items were delivered; no score or item records apply. The decline does not undo ordinary lesson-check evidence or establish a blanket preference.

<a name="quiz-2026-11-06-session-01"></a>

### Optional tutor quiz — 2026-11-06-session-01

- Date: 2026-11-06
- Units: [M04-U02 — Define a search space](notes.md#m04-u02--define-a-search-space)
- Verified sources: **S1** = https://learn.microsoft.com/en-us/training/modules/perform-hyperparameter-tuning-azure-machine-learning-pipelines/2-define-search-space (fetched 2026-11-06). All items cite S1.
- Participation: completed.
- Requested/planned: Full quiz (up to 10) / 8; focused scope, without padding.
- Presented / valid answered: 8 / 8.
- Correct / incorrect / skipped / invalid / unasked or unanswered: 8 / 0 / 0 / 0 / 0.
- Score: 8/8.
- Difficulty mix: 2 easy, 4 medium, 2 hard. Multiple-answer items use exact-set scoring, no partial credit.
- Count scope: M04 only; also session-wide counts.
- Evidence provenance: current-session initial selections returned by the question tool; tutor-created formative items, not an official assessment. No code or Azure sweep execution occurred.

<a name="quiz-2026-11-06-session-01-q01"></a>

#### Q01 — Search-space definition; easy; single-answer; M04-U02; S1

Prompt: What does a hyperparameter search space define? Select one answer.
- A. The best values already found — The final tuning result.
- B. The candidate values allowed — The possibilities available to the tuning process.
- C. The number of concurrent trials — How many training runs execute simultaneously.

Initial learner selections: B.
Correct set: B.
Outcome: correct.
Explanation: The search space defines candidate values, not the result of tuning (A) or concurrency limits (C). Source: S1.
Follow-up: None.

<a name="quiz-2026-11-06-session-01-q02"></a>

#### Q02 — Exact discrete choices; easy; single-answer; M04-U02; S1

Prompt: Which definition allows batch sizes of exactly 16, 32, or 64? Select one answer.
- A. Uniform(16, 64) — A continuous distribution between the bounds.
- B. Normal(mu=32, sigma=16) — A distribution centered at 32.
- C. Choice(values=[16, 32, 64]) — An explicit list of candidates.

Initial learner selections: C.
Correct set: C.
Outcome: correct.
Explanation: Choice permits only the listed values. Uniform allows intermediate values; Normal allows values outside the list and has no hard bounds. Source: S1.
Follow-up: None.

<a name="quiz-2026-11-06-session-01-q03"></a>

#### Q03 — Positivity through exponentiation; medium; multiple-answer; M04-U02; S1

Prompt: Which distributions produce strictly positive values by exponentiating sampled values? Select two answers.
- A. LogNormal — A logarithmic distribution.
- B. Normal — An ordinary normal distribution.
- C. Uniform with bounds −1 and 1 — A continuous bounded distribution.
- D. LogUniform — Another logarithmic distribution.

Initial learner selections: A, D.
Correct set: A, D.
Outcome: correct (exact set).
Explanation: LogNormal and LogUniform exponentiate samples. Normal can produce nonpositive values, and the stated Uniform range includes them. Source: S1.
Follow-up: None.

<a name="quiz-2026-11-06-session-01-q04"></a>

#### Q04 — Equal multiplicative bands; medium; single-answer; M04-U02; S1

Prompt: A learning rate should have equal probability of falling in each band: 0.0001–0.001, 0.001–0.01, and 0.01–0.1. Which definition fits? Select one answer.
- A. Uniform(0.0001, 0.1) — Uniform sampling in linear space.
- B. LogUniform(ln(0.0001), ln(0.1)) — Uniform sampling in natural-log space.
- C. Choice(values=[0.0001, 0.001, 0.01, 0.1]) — Sampling only four listed values.

Initial learner selections: B.
Correct set: B.
Outcome: correct.
Explanation: These factor-of-10 bands have equal widths in log space. Uniform favors the widest linear band; Choice limits values to four points instead of sampling throughout the bands. Source: S1.
Follow-up: None.

<a name="quiz-2026-11-06-session-01-q05"></a>

#### Q05 — Linear interval probability; medium; single-answer; M04-U02; S1

Prompt: You use Uniform(min_value=0.001, max_value=0.1). Which interval has the greatest probability of receiving a sample? Select one answer.
- A. 0.001–0.01 — The lower interval.
- B. Both intervals equally — Equal probability for each interval.
- C. 0.01–0.1 — The upper interval.

Initial learner selections: C.
Correct set: C.
Outcome: correct.
Explanation: The upper interval is ten times wider in linear space (0.09 versus 0.009), so has ten times the probability. Equal probability for these bands would describe log-space sampling, not Uniform. Source: S1.
Follow-up: None.

<a name="quiz-2026-11-06-session-01-q06"></a>

#### Q06 — Normal parameters; medium; multiple-answer; M04-U02; S1

Prompt: What do mu and sigma specify in Normal(mu, sigma)? Select two answers.
- A. mu is the hard minimum — A lower bound on all sampled values.
- B. sigma is the standard deviation — The distribution's spread.
- C. mu is the mean — The distribution's center.
- D. sigma is the quantization step — The spacing between discrete values.

Initial learner selections: C, B (returned order); set B, C.
Correct set: B, C.
Outcome: correct (exact set).
Explanation: mu is the mean, not a hard bound; sigma is the standard deviation. Quantized distributions use q as their step. Source: S1.
Follow-up: None.

<a name="quiz-2026-11-06-session-01-q07"></a>

#### Q07 — Script constraints and quantization; hard; single-answer; M04-U02; S1

Prompt: A proposed batch-size search rounds samples to multiples of 16 over a range that includes 16 through 64. The script accepts only 16, 32, or 64. What is the best correction? Select one answer.
- A. Use Choice(values=[16, 32, 64]) — Declare the accepted values explicitly.
- B. Keep rounding to multiples of 16 — Retain the proposed quantized search.
- C. Use Uniform(16, 64) — Replace rounding with continuous sampling.

Initial learner selections: A.
Correct set: A.
Outcome: correct.
Explanation: Choice enforces the exact constraint. Rounding can produce 48; Uniform allows other intermediate values. Source: S1, applied tutor scenario.
Follow-up: None.

<a name="quiz-2026-11-06-session-01-q08"></a>

#### Q08 — LogUniform bounds troubleshooting; hard; single-answer; M04-U02; S1

Prompt: Azure ML defines LogUniform(a, b) as exp(Uniform(a, b)). A developer passes a=0.001 and b=0.1, expecting learning rates between 0.001 and 0.1. What is actually the issue? Select one answer.
- A. LogUniform can return negative values — Exponentiation may change the sign.
- B. It returns only the two bounds — Intermediate values cannot be sampled.
- C. The output is between exp(0.001) and exp(0.1) — Raw positive bounds were supplied instead of their natural logarithms.

Initial learner selections: C.
Correct set: C.
Outcome: correct.
Explanation: LogUniform exponentiates its uniformly sampled log-space values. Supply ln(0.001) and ln(0.1) for the intended output range. Outputs are positive and span a continuous range, ruling out A and B. Source: S1.
Follow-up: None.

Strengths: Correct candidate-space definition, exact Choice constraints, positivity, linear/logarithmic probabilities, Normal parameters, quantization constraints, and log-space bounds (Q01–Q08).

Misconceptions and remaining gaps: The ordinary lesson check initially proposed Normal for a positive-only parameter; tutor feedback and a scaffolded retry preceded this quiz. Q03 and Q06 now support the distinction, but no sweep was executed. Exact ordinary responses are retained in the memory session, not notes.

Review proposal: M04-U02, 2026-11-09, independently select a positive-valued distribution in a fresh scenario and explain its bounds. Quiz success supports reinforcement rather than an unresolved conceptual failure.

<a name="quiz-2026-11-06-session-02"></a>

### Optional tutor quiz — 2026-11-06-session-02

- Date: 2026-11-06
- Units: [M04-U03 — Configure a sampling method](notes.md#m04-u03--configure-a-sampling-method)
- Verified sources: **S1** = https://learn.microsoft.com/en-us/training/modules/perform-hyperparameter-tuning-azure-machine-learning-pipelines/3-configure-sampling-method ; **S2** = https://learn.microsoft.com/en-us/python/api/azure-ai-ml/azure.ai.ml.sweep.randomsamplingalgorithm?view=azure-python . Both fetched 2026-11-06. Abbreviations in this session refer to these sources only.
- Participation: completed.
- Requested/planned: Full quiz (up to 10) / 8; focused scope without padding.
- Presented / valid answered: 8 / 8.
- Correct / incorrect / skipped / invalid / unasked or unanswered: 8 / 0 / 0 / 0 / 0.
- Score: 8/8.
- Difficulty mix: 2 easy, 4 medium, 2 hard. Multiple-answer scoring requires the exact set; no partial credit.
- Count scope: M04 only; also session-wide counts.
- Evidence provenance: current-session initial selections returned by the question tool. Tutor-created formative checks, not an official Microsoft assessment. All code was illustrative and not run.

<a name="quiz-2026-11-06-session-02-q01"></a>

#### Q01 — Search-space role; easy; single-answer; M04-U03; S1

Prompt: What does a hyperparameter search space define? Select one answer.
- A. The allowed candidate values — The values available for sampling.
- B. The order of trial execution — The sequence in which trials run.
- C. The number of trials — The trial budget for the sweep.

Initial learner selections: A.
Correct set: A.
Outcome: correct.
Explanation: Search space defines allowed values, not execution order (B) or trial limits (C). Source: S1.
Follow-up: None.

<a name="quiz-2026-11-06-session-02-q02"></a>

#### Q02 — Grid combination count; medium; single-answer; M04-U03; S1

Prompt: A grid has three batch-size choices and four learning-rate choices. With no repetitions or failed trials, how many trials are needed to test every combination? Select one answer.
- A. 7 — Seven trials.
- B. 4 — Four trials.
- C. 12 — Twelve trials.
- D. 3 — Three trials.

Initial learner selections: C.
Correct set: C.
Outcome: correct.
Explanation: Multiply 3 × 4 = 12. A adds counts; B and D count only one hyperparameter's choices. Source: S1, applied tutor scenario.
Follow-up: None.

<a name="quiz-2026-11-06-session-02-q03"></a>

#### Q03 — Grid/random constraints; medium; multiple-answer; M04-U03; S1

Prompt: Which statements about grid and random sampling are correct? Select two answers.
- A. Grid supports continuous intervals — A grid can exhaust an unrestricted continuous interval.
- B. Grid requires discrete hyperparameters — Each hyperparameter must have discrete candidates.
- C. Random guarantees exhaustive coverage — Every possible combination is guaranteed to be tested.
- D. Random supports mixed search spaces — Discrete and continuous hyperparameters can be combined.

Initial learner selections: D, B (returned order); set B, D.
Correct set: B, D.
Outcome: correct (exact set).
Explanation: Grid requires discrete candidates, while random supports mixed spaces. Grid cannot exhaust continuous intervals (A); random does not guarantee exhaustive coverage (C). Source: S1.
Follow-up: None.

<a name="quiz-2026-11-06-session-02-q04"></a>

#### Q04 — Results-guided method; easy; single-answer; M04-U03; S1

Prompt: Which sampling method uses earlier trial results to guide later hyperparameter choices? Select one answer.
- A. Grid — Systematic combination coverage.
- B. Bayesian — Results-guided selection.
- C. Sobol — More evenly spread sampling.

Initial learner selections: B.
Correct set: B.
Outcome: correct.
Explanation: Bayesian uses prior performance. Grid systematically covers combinations; Sobol spreads samples rather than adapting to performance. Source: S1. The option descriptions provide strong recognition cues, so this item is weaker evidence than the applied questions.
Follow-up: None.

<a name="quiz-2026-11-06-session-02-q05"></a>

#### Q05 — Changing the seed; medium; single-answer; M04-U03; S1/S2

Prompt: A Sobol sweep uses batch_size=Choice([3, 10, 15]) and learning_rate=Uniform(0.001, 0.1). You change only seed=4 to seed=99. What can change? Select one answer.
- A. The allowed batch sizes — The choices become 3, 10, 15, and 99.
- B. The learning-rate bounds — The upper bound becomes 99.
- C. The trial budget — The sweep now runs 99 trials.
- D. The sampled sequence — Different combinations may be selected within the same search space.

Initial learner selections: D.
Correct set: D.
Outcome: correct.
Explanation: A seed controls the sampling sequence, not allowed values (A), bounds (B), or trial count (C). Sources: S1/S2, applied tutor scenario; shorthand expressions in the prompt are conceptual.
Follow-up: None.

<a name="quiz-2026-11-06-session-02-q06"></a>

#### Q06 — Reproducibility scope; medium; multiple-answer; M04-U03; S1/S2

Prompt: Which statements about a seeded Sobol sweep are justified? Select two answers.
- A. Sampling can be reproduced — With the same seed and sampling configuration, the sampling sequence is reproducible.
- B. Training results must be identical — The sampling seed controls all randomness in model training.
- C. Fixed inputs remain fixed — A learning rate outside the search space and configured as fixed is not tuned.
- D. The seed fixes every batch size — Every trial uses a batch size numerically equal to the seed.

Initial learner selections: A, C.
Correct set: A, C.
Outcome: correct (exact set).
Explanation: Seeded sampling is reproducible and fixed inputs are not sampled. The seed does not control all training randomness (B) or become the batch size (D). Sources: S1/S2 with tutor clarification of sampling versus training reproducibility.
Follow-up: None.

<a name="quiz-2026-11-06-session-02-q07"></a>

#### Q07 — Bayesian incompatibility; hard; single-answer; M04-U03; S1

Prompt: You want Bayesian sampling with batch_size=Choice([16, 32, 64]) and learning_rate=Normal(mu=0.05, sigma=0.01). Which change satisfies the sampling-method constraint taught in this unit? Select one answer.
- A. Increase the trial budget — Keep both expressions and allow more trials.
- B. Add a sampling seed — Keep both expressions and configure a seed.
- C. Replace Normal with Uniform — Use learning_rate=Uniform(0.001, 0.1), assuming this range is appropriate for the model.
- D. Replace Choice with Normal — Use a Normal distribution for batch size too.

Initial learner selections: C.
Correct set: C.
Outcome: correct.
Explanation: Bayesian supports Choice, Uniform, and QUniform, not Normal. A/B do not fix an unsupported expression; D introduces another unsupported expression. Source: S1, applied tutor scenario; prompt uses conceptual shorthand.
Follow-up: None.

<a name="quiz-2026-11-06-session-02-q08"></a>

#### Q08 — Budget and results-guided selection; hard; single-answer; M04-U03; S1

Prompt: You have six batch-size choices, eight learning-rate choices, and a budget of twelve expensive trials. Your priority is to use observed trial performance to guide later selections, rather than exhaust the space. Both hyperparameters use Choice. Which method best matches that priority? Select one answer.
- A. Grid sampling — Use a grid over the specified candidates.
- B. Bayesian sampling — Use Bayesian sampling over the specified candidates.
- C. Sobol sampling — Use seeded Sobol sampling over the specified candidates.
- D. Random sampling — Use ordinary random sampling over the specified candidates.

Initial learner selections: B.
Correct set: B.
Outcome: correct.
Explanation: Bayesian uses performance feedback and supports both Choice expressions. A full grid requires 48 trials; Sobol and ordinary random sampling do not adapt to performance. Source: S1, applied tutor scenario.
Follow-up: None.

Strengths: Grid combination counting (Q02), method constraints (Q03/Q07), seed versus search space and reproducibility scope (Q05/Q06), and applied Bayesian selection (Q08).

Misconceptions and remaining gaps: Ordinary checks initially confused allowed choices with exhaustive coverage, suggested ten distinct random combinations, and left seed versus search-space changes uncertain. Tutor clarification preceded correct quiz applications. No unresolved conceptual error was observed in the quiz; practical sweep execution remains unverified. Q04's descriptions cued its answer and should not be treated as strong independent evidence.

Review proposal: M04-U03, 2026-11-09, fresh transfer scenario combining grid count, seed effects, and a Bayesian-compatible search space. Reinforcement after scaffolded clarification, not a claim that the 8/8 score establishes mastery.

<a name="quiz-2026-11-06-session-03"></a>

### Optional tutor quiz — 2026-11-06-session-03

- Date: 2026-11-06
- Units: [M04-U04 — Configure early termination](notes.md#m04-u04--configure-early-termination)
- Verified sources: **S1** = https://learn.microsoft.com/en-us/training/modules/perform-hyperparameter-tuning-azure-machine-learning-pipelines/4-configure-early-termination (fetched 2026-11-06). All items in this session cite S1.
- Participation: completed.
- Requested/planned: Short quiz (up to 5) / 5.
- Presented / valid answered: 5 / 5.
- Correct / incorrect / skipped / invalid / unasked or unanswered: 4 / 1 / 0 / 0 / 0.
- Score: 4/5.
- Difficulty mix: 1 easy, 3 medium, 1 hard. Multiple-answer items require an exact set, with no partial credit.
- Count scope: M04 only; also session-wide counts.
- Evidence provenance: current-session initial selections returned by the question tool. Follow-up chat responses are recorded separately without changing the initial score. Tutor-created formative checks, not an official Microsoft assessment; code was not run.

<a name="quiz-2026-11-06-session-03-q01"></a>

#### Q01 — Trial versus sweep stopping; easy; single-answer; M04-U04; S1

Prompt: What does an early-termination policy stop when it identifies an underperforming trial? Select one answer.
- A. The entire sweep — All trials stop, including promising trials.
- B. The individual trial — Other trials can continue running.
- C. Future trials only — Active trials continue without interruption.

Initial learner selections: B.
Correct set: B.
Outcome: correct.
Explanation: The policy stops an underperforming individual trial; it does not end the sweep (A) or only prevent future trials (C). Source: S1.
Follow-up: None.

<a name="quiz-2026-11-06-session-03-q02"></a>

#### Q02 — Reporting intervals and per-trial delay; medium; multiple-answer; M04-U04; S1

Prompt: A trial logs its primary metric twice per epoch. Which statements correctly describe early-termination timing? Select two answers.
- A. Each epoch counts once — An epoch is always one evaluation interval.
- B. Each metric report counts — Each primary-metric log is a reporting interval.
- C. Delay counts finished trials — Evaluation waits for other trials to finish.
- D. Delay is per trial — Each trial receives its own initial reporting period.

Initial learner selections: D, A (returned order); set A, D.
Correct set: B, D.
Outcome: incorrect (exact-set scoring).
Explanation: D was correctly selected, but B was omitted and A incorrectly selected. Primary-metric reports count as intervals, so two logs per epoch produce two reporting intervals. The delay is per trial, not based on completed trials (C). Source: S1, applied tutor scenario.
Follow-up: After the quiz, the tutor asked, “If a trial logs its primary metric twice per epoch, how many reporting intervals has it produced after two epochs?” Initial follow-up: “it will have logged 4 primary metrics over two intervals.” The tutor clarified four reports = four reporting intervals across two epochs. Asked whether four reporting intervals had been supplied, the learner replied, “epochs is when we do evaluations, right? I assume that delay_evaluation is in epochs. So it will need two more epochs before the logic is applied?” The tutor distinguished epochs, metric logging, and stopping-policy checks, explained that two epochs already supplied four reports in this example, and that the source places the first check at the fifth report for delay 4 with interval 1. Final scaffolded check: “A trial has logged its primary metric only three times. Has it supplied the four reporting intervals required by delay_evaluation=4 yet?” Response: “no. you need one more log report of the primary metric”. Correct scaffolded recovery; independent epoch-to-report transfer remains to review. Initial quiz answer and score are unchanged.

<a name="quiz-2026-11-06-session-03-q03"></a>

#### Q03 — Absolute Bandit slack; medium; single-answer; M04-U04; S1

Prompt: You maximize validation accuracy with a Bandit policy and slack_amount=0.10. At an eligible evaluation, the best trial has accuracy 0.88. Another trial's best reported accuracy is 0.80. What happens to that other trial? Select one answer.
- A. It is terminated — Its accuracy is below the allowed threshold.
- B. The sweep ends — Its result stops every trial.
- C. It continues — Its accuracy is within the allowed margin.
- D. It must reach 0.98 — The required accuracy is best plus slack.

Initial learner selections: C.
Correct set: C.
Outcome: correct.
Explanation: The threshold is 0.88 − 0.10 = 0.78; 0.80 is acceptable. A would apply below the threshold; B confuses trial and sweep stopping; D adds instead of subtracting slack for this maximization example. Source: S1, applied tutor scenario.
Follow-up: None.

<a name="quiz-2026-11-06-session-03-q04"></a>

#### Q04 — Median comparison; medium; single-answer; M04-U04; S1

Prompt: You maximize accuracy and want to stop trials whose running-average accuracy is below the median of trial running averages. Which policy matches? Select one answer.
- A. Truncation selection — Use a truncation-selection policy.
- B. Median stopping — Use a median-stopping policy.
- C. Bandit — Use a Bandit policy.

Initial learner selections: B.
Correct set: B.
Outcome: correct.
Explanation: Median stopping uses the stated running-average comparison. Truncation removes a ranked percentage; Bandit compares with the best trial using allowed slack. Source: S1. Recognition of “median” in the stem is weaker evidence than independent policy application.
Follow-up: None.

<a name="quiz-2026-11-06-session-03-q05"></a>

#### Q05 — Truncation configuration; hard; single-answer; M04-U04; S1

Prompt: You want to cancel the lowest-performing 20% of active trials, allow each trial four primary-metric reporting intervals before its first evaluation, and evaluate every reporting interval afterward. Which configuration matches? Select one answer.
- A. BanditPolicy(slack_amount=0.20) — delay_evaluation=4, evaluation_interval=1.
- B. TruncationSelectionPolicy, delay=1 — truncation_percentage=20, delay_evaluation=1, evaluation_interval=4.
- C. MedianStoppingPolicy, delay=4 — delay_evaluation=4, evaluation_interval=1.
- D. TruncationSelectionPolicy, delay=4 — truncation_percentage=20, delay_evaluation=4, evaluation_interval=1.

Initial learner selections: D.
Correct set: D.
Outcome: correct.
Explanation: D supplies the correct policy, percentage, delay, and frequency. A uses a margin instead of a ranked percentage; B swaps timing settings; C compares against a median. Source: S1, applied tutor scenario. Matching configuration is supported, but Q02 and its follow-up reveal that independent timing interpretation is not yet secure.
Follow-up: None.

Strengths: Individual-trial stopping (Q01), absolute Bandit threshold application (Q03), median policy recognition (Q04), and truncation configuration matching (Q05).

Misconceptions and remaining gaps: Q02 and follow-up explanations repeatedly equated reporting intervals with epochs. A final report-only check was correct after explicit tutoring; independent transfer with different logging frequencies remains unverified. The source's inconsistent “four trials” wording was explicitly clarified. No Azure execution occurred; practical sweep construction and the M04-U06 lab remain pending.

Review proposal: M04-U04, 2026-11-07, independently distinguish epochs, primary-metric reporting intervals, delay, and evaluation frequency in a fresh logging-frequency scenario. Final recovery was scaffolded and does not replace Q02's initial response.
