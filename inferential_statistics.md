# Inferential Statistics: CLT, Confidence Intervals, Hypothesis Testing & A/B Tests

## Central Limit Theorem (CLT)

Even when the population distribution is skewed, the **sampling distribution of the sample mean** approaches a normal distribution as the sample size increases.

Key statements:
- The mean of the sampling distribution equals the population mean.
- The standard deviation of the sampling distribution (standard error) is σ/√n.
- For non-normal populations, n ≥ 30 is usually sufficient for the approximation to hold.

This justifies normal-based confidence intervals and z-tests for means and proportions with large samples.

**StrataScratch reference**: Central Limit Theorem (ID 2386).

## Confidence Intervals

A range that is likely to contain the true population parameter at a chosen confidence level (commonly 95%).

Large-sample formula for a mean (known σ):

$$ \bar{x} \pm z_{\alpha/2} \cdot \frac{\sigma}{\sqrt{n}} $$

For a proportion:

$$ \hat{p} \pm z_{\alpha/2} \cdot \sqrt{\frac{\hat{p}(1-\hat{p})}{n}} $$

**Margin of error** scales with 1/√n. To reduce the margin of error by a factor of 10, you need roughly 100× the sample size.

Common interview angles: Tesla (CI for binomial proportion), Google (samples needed to shrink margin of error).

## Hypothesis Testing Workflow

1. State H₀ (no effect / no difference) and H₁ (effect exists).
2. Choose significance level α (usually 0.05).
3. Compute the test statistic.
4. Decide using the critical value (rejection region) **or** the p-value.
5. Interpret the result in context.

### p-value

The probability of observing a result at least as extreme as the one obtained, **assuming H₀ is true**.

- Small p-value (< α) → reject H₀.
- Larger sample size reduces standard error, which tends to make the test statistic larger and the p-value smaller (more power).

**StrataScratch / interview references**: State Farm, Amazon.

### Type I and Type II Errors

| Error | Definition | Probability |
|-------|------------|-------------|
| Type I (false positive) | Reject true H₀ | α |
| Type II (false negative) | Fail to reject false H₀ | β |
| Power | Correctly reject false H₀ | 1 − β |

### One-Tailed Z-Test

Example: housing inflation. H₀: inflation = 10%; H₁: inflation > 10%.

### Two-Sample / A/B Z-Tests

Drug effectiveness, website design, conversion-rate comparisons.

For full A/B testing (including production model versions, network effects, and trustworthiness conditions), see:

**[A/B Testing](ab_testing.md)**

### T-Test (Small Samples or Unknown σ)

Uses the sample standard deviation and the t-distribution.

### Chi-Squared Tests

| Test | Question Answered |
|------|-------------------|
| Goodness of Fit | Do observed frequencies match expected? |
| Independence | Are two categorical variables associated? |

## Multicollinearity

When two or more predictors in a regression are highly linearly correlated.

Effects:
- Coefficient estimates become unstable.
- Standard errors inflate.
- p-values for individual predictors become unreliable.

Detection:
- Pairwise correlation matrix (flag |r| > 0.75–0.8).
- **Variance Inflation Factor (VIF)**: VIFⱼ = 1 / (1 − R²ⱼ). Values > 5–10 indicate a problem.

**StrataScratch reference**: Assessing Multicollinearity (ID 2380).

Implementation: see [practical_interview_solutions.md](practical_interview_solutions.md).

## Sampling Bias

Valid inference requires a representative sample. Common threats:
- Sample bias
- Participation bias
- Survivorship bias
- Language bias

## Exercises Covered

| Material | Primary Focus |
|----------|---------------|
| Retail sales | Confidence intervals |
| Work hours | Z-score outlier removal |
| Housing inflation | One-tailed Z-test |
| Drug and website A/B tests | Two-sample Z-test |
| Exam scores | One-sample t-test |
| Phone sales | Chi-squared goodness of fit and independence |
| Solar-panel bills | CLT demonstration |

## Connection to Applied Work

- CLT underpins many assumptions about evaluation metrics.
- Confidence intervals communicate uncertainty.
- Hypothesis and A/B tests determine whether an observed difference is statistically significant.
- Multicollinearity checks protect feature-selection decisions.

See also: [ab_testing.md](ab_testing.md) for production A/B testing of model versions.
