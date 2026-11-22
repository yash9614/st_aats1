# Conceptual Interview Answers

Concise answers to the high-priority questions in [statistics_interview_questions.md](statistics_interview_questions.md).

## Central Limit Theorem

The sampling distribution of the sample mean becomes approximately normal as n increases, with mean = population mean and standard error = σ/√n. This holds even if the population is not normal (roughly n ≥ 30 is a common rule of thumb for skewed data). It justifies normal-based inference for means and proportions.

## p-value

The probability of observing a result at least as extreme as the one obtained, assuming the null hypothesis is true. A smaller p-value indicates stronger evidence against H₀. With a larger sample size the standard error shrinks, so the same effect size produces a smaller p-value (higher power), but the interpretation of any given p-value remains the same.

## Type I / Type II Errors & Power

- Type I: reject true H₀ (false positive). Probability = α.
- Type II: fail to reject false H₀ (false negative). Probability = β.
- Power = 1 − β = probability of correctly detecting a real effect.

## Margin of Error & Sample Size

Margin of error is proportional to 1/√n. To reduce it by a factor of 10 you need approximately 100 times as many samples.

## Multicollinearity

High linear correlation among predictors. It inflates standard errors of coefficients and makes individual p-values unreliable. Detect with pairwise correlations (|r| > ~0.75–0.8) or VIF (VIF > 5–10 is concerning). VIFⱼ = 1/(1−R²ⱼ).

## Mean vs Median

Prefer the median when the distribution is skewed or contains outliers (e.g., income, age in some populations, session length). In a right-skewed distribution the mean is pulled higher than the median.

## Outlier Detection

- Z-score: |z| > 3 (assumes approximate normality).
- IQR: outside [Q1 − 1.5·IQR, Q3 + 1.5·IQR].
- Modified z-score (MAD): more robust; |0.6745·(x−median)/MAD| > 3.5.

## A/B Testing Trustworthiness

Random assignment, consistent assignment per unit, pre-specified primary metric, adequate power, SRM check passes, practical significance considered, and interference either absent or properly accounted for (cluster randomization, switchback, etc.).

## Network Effects

When one unit’s treatment affects others (social feeds, marketplaces), simple user-level randomization violates SUTVA and biases results. Remedies include cluster randomization, graph-cluster randomization, switchback designs, and interference-aware estimators.

## Bayes’ Theorem

P(A|B) = P(B|A)P(A) / P(B). Bayesian approaches update prior beliefs with data; frequentist approaches treat probabilities as long-run frequencies.

---

For full treatments see the topic notes and [ab_testing.md](ab_testing.md). Coding solutions are in [practical_interview_solutions.md](practical_interview_solutions.md).
