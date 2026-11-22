# Inferential Statistics: CLT, Confidence Intervals, Hypothesis Testing & A/B Tests

Notes distilled from chapter 8–12 materials covering the Central Limit Theorem, confidence intervals, Z-tests, t-tests, chi-squared tests, and practical A/B testing.

## Central Limit Theorem (CLT)

Even if the population distribution is skewed (e.g., electricity bills), the **sampling distribution of the sample mean** approaches a normal distribution as the sample size grows.

- Practical demonstration: survey of monthly bills across many cities → original data right-skewed, sampling distribution of means is approximately normal.
- Enables use of normal-based inference even when the underlying data is not normal (provided samples are large enough).

## Confidence Intervals

A range that is likely to contain the true population parameter (usually the mean) with a given confidence level (commonly 95%).

- Example: daily miles driven by a car (population data available). Take a random sample, compute CI for the mean, and compare to the known population mean.
- Formula (large sample / known σ):

$$ \bar{x} \pm z_{\alpha/2} \cdot \frac{\sigma}{\sqrt{n}} $$

- Useful for quantifying uncertainty around estimates from samples.

## Hypothesis Testing with Z-Test

### One-Tailed Test Example (Housing Inflation)
- **H₀**: Inflation = 10%
- **H₁**: Inflation > 10%
- Significance level α = 0.05
- Decision rules:
  - Rejection region: if test statistic > critical value → reject H₀
  - p-value: if p < α → reject H₀

### Two-Sample / A/B Testing Examples
1. **Drug effectiveness** — Control vs new drug; test whether mean recovery time decreases.
2. **Website design** — Current design vs new design; test whether average time spent increases (right-tailed two-sample Z-test).

### General Workflow
1. State H₀ and H₁
2. Choose α (usually 0.05)
3. Compute test statistic (Z)
4. Decide via critical value **or** p-value
5. Interpret in context

## T-Test (Small Samples / Unknown σ)

Used when the sample size is small or the population standard deviation is unknown (uses sample standard deviation and t-distribution).

### Example: New Teaching Method
- Historical population mean exam score = 72
- Pilot sample of 20 students
- **H₀**: New method does not increase average score
- **H₁**: New method increases average score
- Decision: if t-statistic > critical value (or p < α) → reject H₀

## Chi-Squared Tests

### 1. Goodness of Fit
Tests whether observed frequencies match expected frequencies.

- Example: phone sales across 4 models — do actual sales match expected proportions?
- If p ≥ α → fail to reject H₀ (expected numbers are consistent with observed)

### 2. Test of Independence
Tests whether two categorical variables are associated.

- Example: phone preference (iPhone vs Samsung) vs age group (<30 vs ≥30)
- **H₀**: No association between phone preference and age group
- **H₁**: There is an association
- If χ² > critical value or p < α → reject H₀ (variables are dependent)

**Note**: Rejection region and p-value methods are two ways of reaching the same decision.

## Practical Exercises Covered

| Exercise / Material | Focus |
|---------------------|-------|
| Retail store sales | Confidence intervals |
| Employees work hours | Mean, std, Z-score outlier removal |
| Housing inflation | One-tailed Z-test |
| Drug A/B test | Two-sample Z-test |
| Website design A/B | Two-sample Z-test on time spent |
| Operational costs / monthly sales | Additional Z-test and p-value practice |
| Exam scores | One-sample t-test |
| Phone sales | Chi-squared goodness of fit & independence |
| Solar panel bills | CLT demonstration |

## Relation to Data Science / NLP Workflows

- CLT justifies normality assumptions in many evaluation metrics.
- Confidence intervals communicate uncertainty around model performance or survey results.
- Hypothesis tests and A/B tests decide whether a new model, feature, or campaign produces a statistically significant improvement.
- Chi-squared tests are useful for categorical feature analysis and contingency tables.
- Outlier handling (Z-score) remains relevant when preparing numeric features or evaluation scores.
