# Statistical Inference

Statistical inference is the discipline of using data from a sample to learn about a larger population. It gives analysts a formal way to estimate unknown quantities, quantify uncertainty, and evaluate whether observed patterns are likely to reflect real effects or random variation.

In practice, inference helps answer questions such as:

* Is customer satisfaction actually improving, or is the change just noise?
* Does a new checkout flow increase conversion?
* Is the average delivery time different across regions?
* How large is the likely effect, and how certain are we?

Inference does not eliminate uncertainty. It measures and manages it.

---

## Why Statistical Inference Matters

Most analysts do not observe an entire population. Instead, they work with a subset:

* a sample of customers
* a set of transactions from a period
* survey responses from selected participants
* users exposed to an experiment

Because samples vary, conclusions based on them also vary. Statistical inference provides the framework to:

* estimate population parameters from sample data
* express uncertainty around estimates
* test claims about differences or relationships
* distinguish signal from random fluctuation

Without inference, analysts may overreact to noise or miss real effects.

---

## Populations and Samples

A **population** is the full set of entities or outcomes of interest.

Examples:

* all customers of a company
* all orders placed this year
* all website sessions from mobile users
* all voters in a district

A **sample** is a subset drawn from that population.

Examples:

* 2,000 surveyed customers
* 50,000 sampled transactions
* a random subset of A/B test users

### Parameters vs Statistics

A **parameter** is a numerical characteristic of a population.

Examples:

* population mean revenue per customer
* true conversion rate
* true proportion of defective products

A **statistic** is a numerical characteristic computed from a sample.

Examples:

* sample mean revenue
* sample conversion rate
* sample defect rate

The goal of inference is to use sample statistics to learn about population parameters.

### Census vs Sample

A **census** measures the entire population. A **sample** measures only part of it.

A census is not always feasible because it may be:

* too expensive
* too slow
* operationally impossible
* still subject to measurement error

In many analytical settings, sampling is the only realistic approach.

### Representative Sampling

Inference is most reliable when the sample represents the population well. Common issues include:

* **selection bias**: the sample systematically excludes some groups
* **nonresponse bias**: some people are less likely to respond
* **convenience sampling**: data is collected from whoever is easiest to reach
* **survivorship bias**: only successful or retained cases are observed

A large sample does not fix a biased sample. Good inference requires both sufficient size and sound sampling design.

---

## Sampling Distributions

A core idea in inference is that a sample statistic is not fixed across all possible samples. If we repeatedly sampled from the same population, the statistic would vary from sample to sample.

The distribution of a statistic across repeated samples is called its **sampling distribution**.

### Example

Suppose the true average order value in a population is $50. If you repeatedly draw random samples of 100 orders and compute the sample mean each time:

* some sample means might be $48
* some might be $51
* some might be $49.5

These sample means form a sampling distribution around the true population mean.

### Why Sampling Distributions Matter

They allow us to answer questions such as:

* How much do estimates typically vary?
* How close is a sample estimate likely to be to the truth?
* Is an observed difference larger than what random sampling would usually produce?

### Standard Error

The **standard error** measures the variability of a statistic across repeated samples.

It is distinct from the standard deviation:

* **standard deviation** describes variability in the data itself
* **standard error** describes variability in the sample estimate

A smaller standard error means more precise estimates.

Standard errors generally decrease when sample size increases. Roughly, precision improves with the square root of sample size, which means doubling the sample does not halve the error.

### Central Limit Theorem

The **Central Limit Theorem** is one of the most important results in inference. It states that, under broad conditions, the sampling distribution of the sample mean becomes approximately normal as sample size grows, even if the underlying data is not normally distributed.

This matters because it lets analysts use normal-based methods for:

* confidence intervals
* hypothesis tests
* approximate probability calculations

The theorem is especially useful for means and proportions, though assumptions still matter.

---

## Confidence Intervals

A **confidence interval** gives a range of plausible values for a population parameter.

Instead of reporting only a point estimate, such as a mean of 12.4, analysts often report an interval such as:

12.4 ± 1.1, or from 11.3 to 13.5

This interval reflects sampling uncertainty.

### Interpretation

A **95% confidence interval** means that if we repeated the sampling process many times and built a confidence interval each time, about 95% of those intervals would contain the true parameter.

It does **not** mean:

* there is a 95% probability the true value is inside this one computed interval
* 95% of the data lies in the interval
* the estimate is correct with 95% certainty in a subjective sense

The correct interpretation refers to the long-run performance of the method.

### Structure of a Confidence Interval

A typical confidence interval has the form:

**estimate ± margin of error**

The margin of error depends on:

* the standard error
* the confidence level
* the method used

Higher confidence levels produce wider intervals.

For example:

* 90% interval → narrower
* 95% interval → wider
* 99% interval → wider still

### Practical Meaning

Confidence intervals are often more informative than binary significance decisions because they show:

* the likely range of effect sizes
* the precision of the estimate
* whether the effect could be practically small or large

### Example

Suppose an experiment estimates that a new recommendation engine increases average order value by $2.10, with a 95% confidence interval of $0.40 to $3.80.

A reasonable interpretation is:

* the data is consistent with a positive effect
* the true increase is plausibly modest or moderately large
* zero is not in the interval, so the result is statistically significant at the 5% level under standard assumptions

---

## Hypothesis Testing

**Hypothesis testing** is a formal procedure for evaluating evidence against a baseline claim.

### Null and Alternative Hypotheses

The **null hypothesis** ((H_0)) usually represents no effect, no difference, or status quo.

The **alternative hypothesis** ((H_1) or (H_a)) represents the effect or difference of interest.

Examples:

* (H_0): the new landing page has the same conversion rate as the old one
* (H_a): the new landing page has a different conversion rate

Or, in a one-sided test:

* (H_0): the new page does not improve conversion
* (H_a): the new page improves conversion

### Test Statistic

A **test statistic** summarizes how far the observed data is from what the null hypothesis would predict.

Examples include:

* z-statistics
* t-statistics
* chi-square statistics
* F-statistics

The larger the discrepancy, the stronger the evidence against the null, assuming the model is appropriate.

### Decision Framework

Hypothesis testing typically follows these steps:

1. State the null and alternative hypotheses.
2. Choose a significance level, often 0.05.
3. Compute a test statistic from the sample.
4. Compute the p-value or compare to a critical value.
5. Decide whether the evidence is strong enough to reject the null.

### Rejecting vs Failing to Reject

Analysts often say:

* **reject the null hypothesis**
* **fail to reject the null hypothesis**

It is important not to say “accept the null” unless the design truly supports that claim. Failing to reject does not prove no effect; it means the data did not provide strong enough evidence against the null.

---

## p-values

A **p-value** is the probability, assuming the null hypothesis is true, of observing a result at least as extreme as the one obtained.

This is a conditional probability:

* it assumes the null is true
* it measures how unusual the data would be under that assumption

### Interpretation

A small p-value indicates that the observed result would be relatively unlikely if the null hypothesis were true. That provides evidence against the null.

For example:

* p = 0.30 → the data is not unusual under the null
* p = 0.04 → the data would be somewhat unusual under the null
* p = 0.001 → the data would be very unusual under the null

### Common Misinterpretations

A p-value is **not**:

* the probability that the null hypothesis is true
* the probability that the alternative hypothesis is true
* the size or importance of an effect
* the probability the result occurred “by chance” in a casual sense

A p-value only measures compatibility between the data and the null model.

### p-value Thresholds

A common rule is:

* if p < 0.05, call the result statistically significant
* if p ≥ 0.05, do not call it statistically significant

This convention is widely used but often overemphasized. A result with p = 0.049 is not meaningfully different from one with p = 0.051. Inference should consider effect size, uncertainty, design quality, assumptions, and context.

---

## Statistical Significance vs Practical Significance

A result can be **statistically significant** without being **practically significant**.

### Statistical Significance

A result is statistically significant when the observed data provides sufficient evidence, under a chosen threshold, to reject the null hypothesis.

This speaks to whether an effect is distinguishable from random variation.

### Practical Significance

A result is practically significant when the effect is large enough to matter in real decision-making.

This depends on context:

* business value
* operational impact
* cost of implementation
* risk
* stakeholder priorities

### Example

Suppose an experiment finds a 0.15% increase in conversion with p < 0.001.

This may be statistically significant because the sample is huge. But whether it matters depends on:

* scale of the business
* engineering cost
* downstream revenue impact
* maintenance burden

Conversely, a large effect in a small sample may fail to reach statistical significance, yet still deserve attention and follow-up.

### Good Analytical Practice

Always report and interpret:

* the estimated effect size
* the confidence interval
* the p-value if relevant
* the business or operational implications

Avoid reducing conclusions to “significant” or “not significant.”

---

## Type I and Type II Errors

Hypothesis testing can produce two main types of mistakes.

### Type I Error

A **Type I error** occurs when the null hypothesis is true, but we reject it.

This is a **false positive**.

Example:

* concluding a new feature improves retention when it actually does not

The probability of a Type I error is controlled by the significance level, often denoted by **alpha** ((\alpha)).

If (\alpha = 0.05), the procedure tolerates a 5% false positive rate in repeated testing under the null.

### Type II Error

A **Type II error** occurs when the alternative hypothesis is true, but we fail to reject the null.

This is a **false negative**.

Example:

* failing to detect that a new fraud model genuinely reduces fraud losses

The probability of a Type II error is denoted by **beta** ((\beta)).

### Power

**Power** is the probability of correctly rejecting the null when a real effect exists.

Power = (1 - \beta)

Higher power means a lower chance of missing a real effect.

### Trade-offs

Type I and Type II errors are often in tension.

If you make it easier to reject the null:

* fewer false negatives
* more false positives

If you make it harder to reject the null:

* fewer false positives
* more false negatives

The right balance depends on context.

Examples:

* In medical screening, missing a serious disease may be costly.
* In product experimentation, launching ineffective changes repeatedly may also be costly.
* In fraud detection, both false alarms and missed fraud matter, but their costs differ.

Inference should be aligned to decision costs, not just conventions.

---

## Power and Sample Size Basics

**Power analysis** asks whether a study is likely to detect an effect of interest if that effect is truly present.

### What Determines Power

Power depends on several factors:

* **effect size**: larger true effects are easier to detect
* **sample size**: larger samples reduce standard error
* **variability**: noisier data makes detection harder
* **significance level**: higher alpha increases power, but also false positives
* **test design**: paired designs and better controls can improve efficiency

### Minimum Detectable Effect

The **minimum detectable effect** (MDE) is the smallest effect size that a study is designed to detect with a chosen level of power.

In experimentation, this is often a crucial planning concept. If the experiment is underpowered, meaningful but modest effects may go unnoticed.

### Sample Size Intuition

Larger samples improve precision, but gains are gradual:

* to cut standard error roughly in half, you need about four times the sample size
* extremely small effects may require very large samples

This is why analysts should define what effect size matters before collecting data.

### Why Underpowered Studies Are Problematic

An underpowered study can lead to:

* non-significant results even when important effects exist
* unstable effect estimates
* exaggerated reported effects among the few studies that do show significance
* wasted time and resources

### Why Overpowered Studies Can Also Mislead

A very large sample can make trivial effects statistically significant. This is another reason to evaluate practical significance, not just p-values.

### Rule-of-Thumb Practice

Before running a study or experiment, define:

* the outcome metric
* the minimum effect worth detecting
* the acceptable false positive rate
* the desired power, often 80% or 90%
* the estimated baseline rate and variability

Then determine whether the required sample is feasible.

---

## One-Sided vs Two-Sided Tests

A **two-sided test** checks for any difference in either direction.

Example:

* is the mean conversion rate different?

A **one-sided test** checks for a difference in only one direction.

Example:

* is the new experience better?

Two-sided tests are more conservative if deviations in either direction matter. One-sided tests should be chosen only when a difference in the opposite direction would not change the decision and the direction was specified in advance.

Changing from two-sided to one-sided after seeing the data is not valid practice.

---

## Assumptions Behind Inference

Statistical methods depend on assumptions. Common assumptions include:

* observations are independent
* the sampling process is appropriate
* the model form matches the problem
* measurement is reliable
* the distributional approximation is reasonable

Violations can distort p-values, intervals, and conclusions.

Examples of issues:

* clustered data treated as independent
* repeated measures ignored
* non-random missingness
* heavy skew with small samples
* multiple testing without adjustment

Inference is never just about formulas. It is about whether the data-generating process supports the method.

---

## Multiple Testing and False Discoveries

When many hypotheses are tested, some will appear significant by chance alone.

For example, testing 100 independent null hypotheses at the 5% level can produce around 5 false positives on average even if none are true.

This matters in:

* dashboard slicing across many segments
* feature screening
* exploratory analysis
* large-scale experimentation

Analysts should account for multiplicity when needed, using approaches such as:

* Bonferroni-style adjustments
* false discovery rate control
* pre-registration of key hypotheses
* separation of exploratory and confirmatory analysis

Unadjusted repeated testing can create misleading certainty.

---

## Confidence Intervals and Hypothesis Tests as Related Ideas

Confidence intervals and hypothesis tests are closely connected.

For many standard tests:

* if the null value is outside the 95% confidence interval, the result is significant at the 5% level
* if the null value is inside the interval, the result is not significant at that level

The interval often communicates more because it shows plausible effect sizes, not just a decision threshold.

---

## Example: A/B Test on Conversion Rate

Suppose a team runs an A/B test:

* Control conversion rate: 8.0%
* Treatment conversion rate: 8.8%
* Estimated uplift: 0.8 percentage points
* 95% confidence interval: 0.1 to 1.5 percentage points
* p-value: 0.02

A sound interpretation is:

* the data provides evidence that treatment outperforms control
* plausible uplift ranges from small to moderate
* the effect is statistically significant at the 5% level
* whether the change should be rolled out depends on business impact, implementation cost, and downstream effects

If the sample were much smaller and the interval were -0.3 to 1.9 percentage points:

* the estimate would still suggest improvement
* but uncertainty would be too high to conclude confidently
* the result would likely not be statistically significant
* more data might be needed

---

## Common Analytical Mistakes

### Treating p < 0.05 as proof

A small p-value is evidence against the null under a model, not proof of a theory.

### Ignoring effect size

A tiny effect can be statistically significant in a large dataset.

### Ignoring uncertainty

Point estimates alone hide how imprecise results may be.

### Confusing non-significance with no effect

A non-significant result may reflect low power, noisy data, or poor design.

### Testing many hypotheses without adjustment

This inflates false positives.

### Using inference on biased samples

Formal statistics cannot rescue fundamentally unrepresentative data.

### Forgetting assumptions

Methods only work well when their assumptions are at least approximately reasonable.

---

## Practical Guidance for Analysts

When presenting inferential results:

1. State the population and sampling process clearly.
2. Report the estimate, not just the p-value.
3. Include a confidence interval.
4. Interpret both statistical and practical significance.
5. Note important assumptions and limitations.
6. Consider whether the study had adequate power.
7. Be careful with multiple comparisons and exploratory analyses.

A credible inferential statement is not merely “the result is significant.” It is a structured argument about what the data suggests, how uncertain that conclusion is, and how much the finding matters.

---

## Summary

Statistical inference allows analysts to move from sample data to broader conclusions about populations and processes. Its main tools include:

* **populations and samples** to define what is being studied
* **sampling distributions** to describe how estimates vary
* **confidence intervals** to express plausible ranges
* **hypothesis testing** to evaluate claims
* **p-values** to measure how unusual data would be under the null
* **Type I and Type II errors** to frame decision risk
* **power and sample size** to plan reliable studies

Used well, inference supports disciplined decision-making. Used poorly, it can create false certainty. Strong analysts focus not only on whether an effect exists, but also on how large it is, how certain they are, and whether it matters.

---

## Key Takeaways

* Samples vary, so estimates vary.
* Inference quantifies that uncertainty.
* Confidence intervals are often more informative than binary significance labels.
* p-values do not measure effect size or the probability that a hypothesis is true.
* Statistical significance and practical significance are different questions.
* Type I errors are false positives; Type II errors are false negatives.
* Power depends on effect size, sample size, variability, and significance level.
* Good inference depends on sound sampling, valid assumptions, and thoughtful interpretation.
