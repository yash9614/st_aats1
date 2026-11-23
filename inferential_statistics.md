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

## Hypothesis Testing

Hypothesis testing is a statistical technique for decision-making or inferring population characteristics from sample data.

### Null vs Alternative Hypothesis

- **Null Hypothesis (H₀)**: Represents a statement of no effect or no difference. It serves as the benchmark (default assumption) in hypothesis testing.
- **Alternative Hypothesis (Hₐ or H₁)**: Proposes a new effect or difference, challenging the null hypothesis. This is what we hope to find evidence for.

### Z-Test

A statistical test used to determine if there's a significant difference between sample and population means (or between two samples), typically when the sample size is large (n > 30) and the population standard deviation is known (or can be estimated reliably).

**Key elements**:
- **Significance Level (α / Alpha)**: Defines the threshold for rejecting the null hypothesis, commonly set at 0.05 (5%). Formula: α = 1 − confidence level.
- **Critical Z-Value (Z_crit)**: The cut-off point in a Z-test that distinguishes the rejection region for the null hypothesis.
- **Rejection Region**: The area beyond the critical Z-value (Z_crit) where, if the Z-score falls, the null hypothesis is rejected due to significant evidence.

### p-Value

The p-value is the probability of obtaining results as extreme as (or more extreme than) those observed, **assuming the null hypothesis is correct**.

- If the p-value is less than the chosen significance level (e.g., 0.05), it suggests strong evidence against the null hypothesis, leading to its rejection.
- Small p-value (< α) → reject H₀.
- Larger sample size reduces standard error, which tends to make the test statistic larger and the p-value smaller (more power).

**StrataScratch / interview references**: State Farm, Amazon.

### One-Tailed vs Two-Tailed Test

- **One-Tail Test**: Checks if a parameter is significantly different in one direction (greater than or less than).
- **Two-Tail Test**: Evaluates if a parameter is significantly different in any direction (greater or less).

### Type I and Type II Errors

| Error | Definition | Also known as | Probability |
|-------|------------|---------------|-------------|
| **Type I** | Incorrectly reject a true null hypothesis | False positive | α |
| **Type II** | Fail to reject a false null hypothesis | False negative | β |
| **Power** | Correctly reject a false null hypothesis | True positive rate | 1 − β |

**Beta (β)**: The probability of making a Type II error (false negative).

**Statistical Power**: The probability of correctly rejecting a false null hypothesis, equal to 1 − β.

Balancing Type I and Type II errors is crucial in statistical analysis. Lowering α reduces Type I error but increases Type II error (and vice versa). Increasing sample size improves power without raising α.

### Statistical Power & Effect Size

- **Statistical power** (1 − β): Probability of correctly rejecting a false null hypothesis.
- **Effect size**: Quantifies the magnitude of the difference or relationship between two groups or variables in a study (e.g., Cohen’s d, difference in proportions).

Larger effect sizes and larger sample sizes both increase statistical power.

### One-Sample vs Two-Sample Tests

- **One-Sample Test**: Used to check if a sample significantly differs from a known population parameter.
- **Two-Sample Test**: Compares two independent sample data sets to identify significant differences between their means or proportions.

### When to Use Z-Test vs T-Test

- Use the **Z-test** when the sample size is > 30 (and σ is known or well-estimated).
- Use the **T-test** when the sample size is ≤ 30 (or when σ is unknown and we use the sample standard deviation).

## A/B Testing

A/B testing compares two versions (A and B) to find which performs better based on user engagement and relevant metrics.

- **Control group**: Baseline for comparing experimental effects (the current version, A).
- **Test group** (Treatment): Subjects exposed to the experimental treatment for evaluation (the new version, B).

Most A/B tests are two-sample hypothesis tests (often a two-proportion z-test for conversion rates).

For full A/B testing details (including production model versions, network effects, sample size/power calculations, and trustworthiness conditions), see:

**[A/B Testing](ab_testing.md)**

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
