# Inferential Statistics: CLT, Confidence Intervals, Hypothesis Testing & A/B Tests

Notes distilled from chapters 8–12 materials.

## Central Limit Theorem (CLT)

Even if the population is skewed, the **sampling distribution of the sample mean** approaches normality as sample size grows.

- Example: electricity bill survey → original data right-skewed, sampling distribution of means approximately normal.
- Justifies normal-based inference for large samples.

## Confidence Intervals

Range likely to contain the true population parameter (usually the mean) at a chosen confidence level (commonly 95%).

Large-sample / known-σ formula:

$$ \bar{x} \pm z_{\alpha/2} \cdot \frac{\sigma}{\sqrt{n}} $$

Example: daily miles driven — sample from population data, compute CI, compare to known population mean.

## Hypothesis Testing — General Workflow

1. State **H₀** (no effect / no difference) and **H₁** (effect exists).
2. Choose significance level α (usually 0.05).
3. Compute test statistic.
4. Decide via **critical value** (rejection region) **or** **p-value** (both methods agree).
5. Interpret in context.

### One-Tailed Z-Test (Housing Inflation)
- H₀: inflation = 10%
- H₁: inflation > 10%
- Reject H₀ if Z > critical value or p < α.

### Two-Sample / A/B Z-Tests
- Drug effectiveness: control vs new drug (recovery time).
- Website design: current vs new design (time spent).

### T-Test (Small Samples / Unknown σ)
- Uses sample standard deviation and t-distribution.
- Example: new teaching method, pilot of 20 students, historical mean = 72.
- Reject H₀ if t > critical value or p < α.

### Chi-Squared Tests

| Test | Purpose | Example |
|------|---------|---------|
| Goodness of Fit | Observed frequencies match expected | Phone sales across 4 models |
| Independence | Association between two categorical variables | Phone preference vs age group |

Decision: if χ² > critical value or p < α → reject H₀.

## Sampling Bias (Important for Valid Inference)

- **Sample bias**: sample not representative of population.
- **Participation bias**: volunteers differ from non-participants.
- **Survivorship bias**: looking only at successes.
- **Language bias**: wording influences responses.

Samples and trial participants must be representative.

## Practical Exercises Covered

| Material | Focus |
|----------|-------|
| Retail sales | Confidence intervals |
| Work hours | Z-score outliers |
| Housing inflation | One-tailed Z-test |
| Drug / website A/B | Two-sample Z-test |
| Exam scores | One-sample t-test |
| Phone sales | Chi-squared goodness of fit & independence |
| Solar bills | CLT demonstration |

## Relation to Data Science / NLP

- CLT underpins many evaluation metric assumptions.
- Confidence intervals communicate uncertainty.
- Hypothesis and A/B tests decide whether a change is statistically significant.
- Chi-squared useful for categorical feature analysis.
