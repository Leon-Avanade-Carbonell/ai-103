# Perform hyperparameter tuning with Azure Machine Learning

- Module ID: M04
- Source: https://learn.microsoft.com/en-us/training/modules/perform-hyperparameter-tuning-azure-machine-learning-pipelines/
- Curriculum verified: 2026-10-28
- Exam objectives: D2 automate hyperparameter tuning.

## Overview and learning goals

Planned source goals: define a search space, configure sampling, select an early-termination policy, and run a sweep job.

## Notes by Microsoft Learn unit

### M04-U01 — Introduction
Source: https://learn.microsoft.com/en-us/training/modules/perform-hyperparameter-tuning-azure-machine-learning-pipelines/1-introduction

Source fetched: 2026-11-05. The following concepts reflect the official introduction, with tutor illustrations labeled separately.

#### Parameters and hyperparameters

- **Parameters** are values learned from training data, such as model weights.
- **Hyperparameters** configure training behavior rather than being learned within the training run. Examples include learning rate, batch size, and regularization strength.
- Hyperparameter choices can significantly affect predictive performance. Tuning seeks useful settings for the particular data and performance goal.

#### Tuning, sweep jobs, and trials

The official introduction describes training multiple models with the same algorithm and training data but different hyperparameter values, evaluating each against a target performance metric, and selecting the best-performing model. In Azure Machine Learning, a **sweep job** coordinates the search; each **trial** runs a parameterized training script for a hyperparameter combination and logs the target metric.

For a fair comparison, keep the algorithm, training data, and evaluation setup consistent and use the same metric and optimization direction. Hyperparameters deliberately vary, and each trial learns its own model parameters: fair comparison does not require identical learned weights.

**Tutor illustration — metric direction:** If trial A has validation loss 0.30 and trial B has validation loss 0.45, a goal of minimizing validation loss favors A. This is a conceptual worked example, not an executed experiment. Testing learning rates 0.01 and 0.1 requires separate training trials, rather than merely changing weights in one already-trained model.

The module's upcoming goals are search-space definition, sampling, early termination, and running a sweep job; their detailed treatment belongs to subsequent units.

### M04-U02 — Define a search space
Source: https://learn.microsoft.com/en-us/training/modules/perform-hyperparameter-tuning-azure-machine-learning-pipelines/2-define-search-space

Source fetched: 2026-11-06. Distribution definitions below reflect Microsoft Learn; applications are tutor illustrations, not executed experiments.

#### Candidate values: discrete and continuous

A **search space** specifies the allowed candidate hyperparameter values. It does not require trying every possible value; sampling and trial limits are separate decisions covered in later units.

- **Discrete:** `Choice(values=[16, 32, 64])` allows exactly those three values. The source also accepts a Python range or tuple for `values`.
- **Continuous:** `Uniform(min_value=0.001, max_value=0.1)` samples along a numerical interval, including intermediate values rather than just its endpoints.

Choose a definition that respects the training script's accepted inputs. For a batch size restricted to 16, 32, or 64, an explicit Choice is preferable to rounding samples to multiples of 16: rounding over that span can also produce the unaccepted value 48.

#### Linear and logarithmic sampling

`Uniform(a, b)` gives equal-width linear intervals equal probability. `LogUniform(a, b)` returns `exp(Uniform(a, b))`, giving equal-width intervals in logarithmic space equal probability.

**Tutor illustration:** Learning-rate bands 0.0001–0.001, 0.001–0.01, and 0.01–0.1 each span a factor of 10. Their linear widths are 0.0009, 0.009, and 0.09. Uniform sampling favors the highest band because it is widest; LogUniform gives these three bands equal probability when configured for this overall range.

Azure ML's LogUniform bounds are in **natural-log space**: use `ln(0.0001)` and `ln(0.1)` to obtain output values from 0.0001 to 0.1. Passing the raw numbers instead yields outputs between `exp(0.0001)` and `exp(0.1)`, not the intended range.

#### Normal, log-normal, and quantized distributions

- `Normal(mu, sigma)` uses mean `mu` and standard deviation `sigma`. Neither is a hard bound; a positive mean does not guarantee positive samples.
- `LogNormal(mu, sigma)` returns `exp(Normal(mu, sigma))`; its output is strictly positive. Here `mu` and `sigma` describe the underlying normal distribution, not directly the output's mean and standard deviation.
- LogUniform also produces positive values, with bounded logarithmic sampling. Use it for exploration across orders of magnitude; LogNormal supports positive values concentrated around a typical scale without hard bounds.
- Quantized distributions round samples to multiples of a step `q`: for example, `QUniform(a, b, q)` returns values like `round(Uniform(a, b) / q) * q`. The source also lists QLogUniform, QNormal, and QLogNormal, applying this rounding to their corresponding distributions. Quantization creates discrete values but does not automatically enforce an arbitrary list of accepted choices.

**Source-example caveat:** The page illustrates `learning_rate=Normal(mu=10, sigma=3)` to show API syntax. This is not a general learning-rate recommendation and does not enforce positivity. Check parameter semantics and algorithm constraints rather than copying illustrative numbers as defaults.

### M04-U03 — Configure a sampling method
Source: https://learn.microsoft.com/en-us/training/modules/perform-hyperparameter-tuning-azure-machine-learning-pipelines/3-configure-sampling-method

Source fetched: 2026-11-06. Method descriptions and supported expressions reflect Microsoft Learn; numerical scenarios below are tutor illustrations, not executed sweeps.

#### Search space versus sampling and coverage

The search space defines allowed candidate values; sampling determines which combinations to try. A trial tests one combination. Staying within allowed choices is not the same as covering all combinations.

- **Grid:** systematically tries every combination in a discrete search space. Every hyperparameter must be discrete. Exhaustive coverage also requires enough trials and time to finish the grid.
- **Random:** selects values from the search space, which can mix discrete and continuous hyperparameters. It does not guarantee exhaustive coverage or a distinct combination on every trial.
- **Sobol:** the unit describes this as a random-sampling variation that spreads samples more evenly. Configure it with `RandomSamplingAlgorithm(rule="sobol", seed=4)` for seeded, reproducible sampling.
- **Bayesian:** uses previous trial performance to guide subsequent choices toward promising combinations. Every hyperparameter expression must be **Choice, Uniform, or QUniform**; Normal is not supported for this method.

**Tutor illustration — coverage:** Four batch-size choices and five learning-rate choices make 4 × 5 = 20 combinations. Ten trials cannot cover all twenty. Random sampling within that budget still cannot guarantee full coverage; repeated combinations can reduce unique coverage further.

#### What a sampling seed does—and does not do

The SDK reference accepts an integer seed and `rule="random"` or `rule="sobol"`: https://learn.microsoft.com/en-us/python/api/azure-ai-ml/azure.ai.ml.sweep.randomsamplingalgorithm?view=azure-python (fetched 2026-11-06).

With batch-size choices `[3, 10, 15]`, `seed=4` controls the sampling sequence; it does not set batch size to 4, set a trial count of 4, or change distribution bounds. Changing only the seed to 99 can change sampled combinations and their order, but batch size must still be 3, 10, or 15. To permit batch size 99, edit the Choice list instead, and confirm the training script accepts that value.

The sampling sequence covers all tunable hyperparameters: a changed seed can affect both batch-size and learning-rate selections. A learning rate configured as fixed rather than included in the search space remains fixed. The exact first sampled combination cannot be inferred from the seed number alone.

Reproducible sampling under the same seed and configuration is not a guarantee of identical trained models: training can have other randomness and execution dependencies. A sampling seed does not control all those factors.

### M04-U04 — Configure early termination
Source: https://learn.microsoft.com/en-us/training/modules/perform-hyperparameter-tuning-azure-machine-learning-pipelines/4-configure-early-termination

Source fetched: 2026-11-06. Policy descriptions reflect Microsoft Learn; numerical applications below are tutor illustrations, not executed sweeps.

#### Individual trial stopping versus sweep limits

An early-termination policy stops underperforming **individual trials** based on their reported primary metric while other trials can continue. A maximum trial count or overall sweep timeout instead limits the complete search. Stopping weak trials can save compute, particularly in expensive searches; a small six-trial discrete grid may not need a stopping policy. Continuous search spaces contain many candidates, and random or Bayesian searches can start unpromising trials.

Early performance need not predict final performance: a slow-starting configuration could be useful later. Delay the first evaluation when initial progress is not yet informative. This allows more training progress and metric reports; it does not necessarily collect additional training-data samples or choose the primary metric.

#### Reporting intervals are not epochs or completed trials

- `evaluation_interval` controls how often the stopping policy evaluates performance, measured in primary-metric reporting intervals. Each log of the primary metric counts as an interval.
- `delay_evaluation` gives **each trial** an initial number of metric-reporting intervals before its first policy evaluation. It does not wait for that many other trials to finish.
- An **epoch** is a pass through the training dataset. A script may evaluate and log its primary metric once per epoch, twice per epoch, or at another frequency. Model evaluation that computes a metric and stopping-policy evaluation that decides whether to cancel a trial are distinct operations.

**Tutor illustration:** With `delay_evaluation=4`, logging once per epoch takes four epochs to supply four reports; logging twice per epoch takes two epochs. Two reports per epoch over two epochs means **four reporting intervals**, not two. Three reports have not yet supplied four intervals, irrespective of epoch count. The source's `evaluation_interval=1` examples place the first stopping evaluation after the initial delay: the fifth report for delay 4 and sixth for delay 5.

**Source wording caveat:** The truncation example's prose says “a delay of four trials.” This conflicts with the page's parameter definition and fifth-reporting-interval explanation. Interpret the setting as a per-trial delay measured in primary-metric reporting intervals, not completed trials.

#### Compare the three policies

| Policy | Comparison and decision |
| --- | --- |
| Bandit | Stop trials too far behind the best-performing trial, using relative `slack_factor` or absolute `slack_amount`. |
| Median stopping | Compare a trial's running-average metric with the median of trial running averages; stop worse-performing trials. |
| Truncation selection | Rank active trials and cancel the lowest-performing configured `truncation_percentage` at eligible evaluations. |

Respect the primary metric's optimization direction: low loss may be good, whereas high accuracy may be good. These comparisons are not all fixed minimum-accuracy tests.

**Tutor illustrations — maximize accuracy:**

- Bandit: best accuracy 0.90 and `slack_amount=0.20` gives a threshold of 0.70. At an eligible evaluation, a trial with best reported accuracy 0.68 stops; 0.75 remains within slack. If the best trial improves, the threshold can change. With best 0.88 and slack 0.10, accuracy 0.80 remains above the 0.78 threshold.
- Median: if the median running-average accuracy is 0.82, a trial with running-average accuracy 0.79 is stopped at an eligible evaluation. The comparison uses running averages, not just a single last report.
- Truncation: with ten active trials and `truncation_percentage=20`, cancel the lowest-performing two at an eligible evaluation. A ranked percentage differs from a Bandit margin or a median comparison.

### M04-U05 — Use a sweep job for hyperparameter tuning
Source: https://learn.microsoft.com/en-us/training/modules/perform-hyperparameter-tuning-azure-machine-learning-pipelines/5-use-sweep-job-hyperparameter-tuning

Pending study.

### M04-U06 — Exercise - Run a sweep job
Source: https://learn.microsoft.com/en-us/training/modules/perform-hyperparameter-tuning-azure-machine-learning-pipelines/6-exercise-run-sweep-job

Pending exercise. Add the studied task and worked solution with execution context; label any equivalent substitute. Preserve learner outcomes in memory.

### M04-U07 — Module assessment
Source: https://learn.microsoft.com/en-us/training/modules/perform-hyperparameter-tuning-azure-machine-learning-pipelines/7-knowledge-check

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this closing unit; it is excluded from tutor completion, review scheduling, and TLDR readiness. No website confirmation is required.

### M04-U08 — Summary
Source: https://learn.microsoft.com/en-us/training/modules/perform-hyperparameter-tuning-azure-machine-learning-pipelines/8-summary

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this closing unit; it is excluded from tutor completion, review scheduling, and TLDR readiness. No website confirmation is required.

## Key concepts and decision points
- M04-U01: a sweep coordinates trials; each trial trains with a hyperparameter combination and logs the shared target metric.
- M04-U02: use Choice for an exact list, Uniform for linear-range coverage, and LogUniform for balanced coverage across orders of magnitude. Match generated values to script constraints; Normal does not enforce positivity.
- M04-U03: grid suits small finite spaces; random supports mixed distributions; Sobol supports more even seeded exploration; Bayesian uses performance feedback but restricts distribution expressions. Seeds control sampling, not allowed values or trial budgets.
- M04-U04: early termination stops weak individual trials; Bandit compares with the best, median stopping compares running averages, and truncation removes a ranked percentage. Delay and frequency count primary-metric reports, not epochs or finished trials.
- Sweep integration and execution remain pending in M04-U05 and M04-U06.

## Python examples
### M04-U02 — Search-space expressions

Tutor illustration using the distribution APIs shown in the verified source. Prerequisites: Python with the Azure Machine Learning SDK v2 package `azure-ai-ml`; a specific installed package version was not inspected. No Azure authentication is needed merely to construct these expressions. This snippet was **not run** and does not submit a sweep job.

```python
from math import log
from azure.ai.ml.sweep import Choice, Uniform, LogUniform

linear_space = {
    "batch_size": Choice(values=[16, 32, 64]),
    "learning_rate": Uniform(min_value=0.001, max_value=0.1),
}

log_space = {
    "batch_size": Choice(values=[16, 32, 64]),
    "learning_rate": LogUniform(
        min_value=log(0.0001), max_value=log(0.1)
    ),
}
```

Expected outcome: dictionaries of search-space expressions, not sampled values or trained models. Integration into a parameterized command job and job submission remain pending for M04-U05.

### M04-U03 — Seeded Sobol configuration objects

Tutor illustration using the verified unit and SDK reference above. Prerequisites: Python and Azure ML SDK v2 (`azure-ai-ml`); no installed version was inspected. This snippet was **not run**. Constructing these objects requires no Azure authentication and does not submit a job.

```python
from azure.ai.ml.sweep import Choice, Uniform, RandomSamplingAlgorithm

search_space = {
    "batch_size": Choice(values=[3, 10, 15]),
    "learning_rate": Uniform(min_value=0.001, max_value=0.1),
}
sampling = RandomSamplingAlgorithm(rule="sobol", seed=4)
```

Expected outcome: a dictionary of search-space expressions and a Sobol sampling configuration. Each eventual trial must choose batch size 3, 10, or 15 and a learning rate within the specified interval; the code does not print or generate an actual trial sequence. Complete sweep integration remains pending for M04-U05. Values are illustrative, not recommended defaults.

### M04-U04 — Truncation policy configuration

Verified unit API example, with explanatory context. Prerequisites: Python and Azure ML SDK v2 (`azure-ai-ml`) with an existing `sweep_job` object; no installed package version was inspected. This snippet was **not run** and does not submit a job.

```python
from azure.ai.ml.sweep import TruncationSelectionPolicy

sweep_job.early_termination = TruncationSelectionPolicy(
    truncation_percentage=20,
    delay_evaluation=4,
    evaluation_interval=1,
)
```

Expected outcome: attach a policy that cancels the lowest-performing 20% at eligible checks, allowing each trial four initial primary-metric reporting intervals and evaluating every interval afterward. Use the exact parameter name `truncation_percentage`, not `truncation_percent`. Complete sweep construction and submission remain pending in M04-U05; this is configuration, not execution evidence.

## JavaScript examples
Pending study. Use relevant supported examples only.

## Azure CLI commands
Pending study. Record CLI/extension prerequisites and expected outcomes.

## Related configuration: YAML, Bicep, or GitHub Actions
Pending study.

## Worked examples and practice
### M04-U03 — Budget and method selection

Tutor-created conceptual exercises; no environment setup required and no code executed.

- **Task:** Three batch-size choices and four learning-rate choices: how many trials cover the full grid? **Worked solution:** 3 × 4 = 12, assuming each combination is tested once without failures.
- **Task:** Six batch-size choices and eight learning-rate choices, but only twelve expensive trials. Both use Choice, and previous results should guide later settings. **Worked solution:** Bayesian matches this priority and supports both expressions. A full grid needs 48 trials; Sobol offers more even exploration but does not adapt to performance.
- **Task:** A Bayesian proposal uses Choice for batch size and Normal for learning rate. **Worked solution:** Replace Normal with a supported expression such as Uniform over a model-appropriate interval; seeds and larger budgets do not fix distribution incompatibility.

Sweep execution and the official M04-U06 exercise remain pending; these conceptual exercises are not substitutes for the practical lab.

[Optional quiz history](quizzes.md)

## Common pitfalls and clarifications
- A positive Normal mean does not prevent negative samples. LogNormal and LogUniform produce positive outputs through exponentiation.
- Equal probability per linear interval differs from equal probability per multiplicative band.
- LogUniform accepts log-space bounds, not raw output bounds.
- Quantized values are discrete, but may still include choices the script rejects; use Choice for an exact permitted list.
- A finite grid's combination count is the product of candidate counts, not their sum; a smaller budget cannot provide exhaustive coverage.
- A sampling seed neither becomes a hyperparameter value nor guarantees identical model-training results.
- Bayesian's expression restrictions apply to every tuned hyperparameter, not just batch size.
- Stopping-policy intervals count primary-metric reports. An epoch and an interval coincide only when the script logs that metric exactly once per epoch; neither counts completed trials.
- Early termination evaluates existing metric evidence to stop individual trials. It neither chooses the metric nor stops the entire sweep merely because one trial underperforms.

## Microsoft Learn search terms
- Azure Machine Learning sweep job search space
- hyperparameter sampling random grid Bayesian Azure
- Azure Machine Learning early termination policies
