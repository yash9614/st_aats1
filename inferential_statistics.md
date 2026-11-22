# Inferential Statistics: CLT, Confidence Intervals, Hypothesis Testing & A/B Tests

## Central Limit Theorem (CLT)

Even when the population distribution is skewed, the **sampling distribution of the sample mean** approaches a normal distribution as the sample size increases.

- Demonstration: monthly electricity bills are right-skewed; the distribution of sample means becomes approximately normal.
- Justifies normal-based methods for sufficiently large samples.

## Confidence Intervals

A range that is likely to contain the true population parameter at a chosen confidence level (commonly 95%).

Large-sample formula (known $\sigma$):

$$ \bar{x} \pm z_{\alpha/2} \cdot \frac{\sigma}{\sqrt{n}} $$

Example: daily miles driven — draw a sample from known population data, compute a CI for the mean, and compare it with the population value.

## Hypothesis Testing Workflow

1. State $H_0$ (no effect / no difference) and $H_1$ (effect exists).
2. Choose significance level $\alpha$ (usually 0.05).
3. Compute the test statistic.
4. Decide using the **critical value** (rejection region) **or** the **p-value** (the two methods agree).
5. Interpret the result in context.

### One-Tailed Z-Test

- Example: housing inflation.
- $H_0$: inflation = 10%; $H_1$: inflation > 10%.
- Reject $H_0$ if the Z-statistic exceeds the critical value or if $p < \alpha$.

### Two-Sample / A/B Z-Tests

- Drug effectiveness: control versus new treatment (recovery time).
- Website design: current versus new design (time spent on page).

For a full treatment of A/B testing (including production model versioning, experiment design requirements, and trustworthiness conditions), see the dedicated note:

**[A/B Testing](ab_testing.md)**

### T-Test (Small Samples or Unknown $\sigma$)

- Uses the sample standard deviation and the t-distribution.
- Example: new teaching method evaluated on a pilot class of 20 students; historical mean score = 72.
- Reject $H_0$ if the t-statistic exceeds the critical value or if $p < \alpha$.

### Chi-Squared Tests

| Test | Question Answered | Example |
|------|-------------------|---------|
| Goodness of Fit | Do observed frequencies match expected frequencies? | Phone sales across four models |
| Independence | Are two categorical variables associated? | Phone preference versus age group |

Decision rule: reject $H_0$ if $\chi^2$ exceeds the critical value or if $p < \alpha$.

## Sampling Bias

Valid inference requires a representative sample. Common threats:

- **Sample bias** — sample does not reflect the population.
- **Participation bias** — volunteers differ systematically from non-participants.
- **Survivorship bias** — only successes are observed.
- **Language bias** — wording influences responses.

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
- Chi-squared tests are useful for categorical feature analysis.

See also: [ab_testing.md](ab_testing.md) for production A/B testing of model versions.
