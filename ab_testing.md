# A/B Testing

## What is A/B Testing?

A/B testing (split testing or controlled experimentation) compares two or more versions of a product, feature, or model by randomly assigning units to variants and measuring the effect on a pre-specified metric.

- **A** = control (current version)
- **B** = treatment (new version)
- Goal: determine whether an observed difference is statistically significant and practically meaningful.

## Core Statistical Foundation

Most A/B tests reduce to a two-sample hypothesis test or a two-proportion z-test.

### Continuous metrics (time on page, revenue, latency)

$$ Z = \frac{\bar{x}_B - \bar{x}_A}{\sqrt{\frac{s_A^2}{n_A} + \frac{s_B^2}{n_B}}} $$

### Proportions (conversion rate, click-through rate)

Pooled proportion under $H_0$:

$$ p_{pool} = \frac{x_A + x_B}{n_A + n_B} $$

$$ SE = \sqrt{p_{pool}(1-p_{pool})\left(\frac{1}{n_A}+\frac{1}{n_B}\right)} $$

$$ z = \frac{p_B - p_A}{SE} $$

The two-sided p-value comes from the standard normal distribution. A working implementation is in [practical_interview_solutions.md](practical_interview_solutions.md).

## Sample Size / Power Calculation

Before launching, estimate the required sample size.

For a two-sided test on proportions (approximate):

$$ n \approx \frac{(z_{\alpha/2} + z_{\beta})^2 \cdot 2\bar{p}(1-\bar{p})}{\delta^2} $$

where
- $\delta$ = minimum detectable effect (absolute difference in rates),
- $\bar{p}$ = baseline rate (or average of the two rates),
- $z_{\alpha/2}$ ≈ 1.96 for α = 0.05,
- $z_{\beta}$ ≈ 0.84 for 80% power.

Underpowered experiments waste traffic and produce inconclusive results.

## Designing a Trustworthy Experiment

### Must-have conditions

| Requirement | Why it matters |
|-------------|----------------|
| Random assignment | Removes selection bias |
| Consistent assignment per unit (hashing) | Prevents contamination |
| Pre-specified primary metric & analysis plan | Avoids p-hacking / HARKing |
| Adequate power / sample size | Controls Type II error |
| No interference (or proper design for it) | Validates independence |
| SRM check passes | Detects assignment or logging bugs |
| Practical significance considered | Ensures the win is worth shipping |

### Additional best practices

- **Sample Ratio Mismatch (SRM)**: chi-squared test on observed vs expected traffic split. A significant mismatch indicates a bug.
- **Guardrail metrics**: latency, error rate, revenue, etc. Automatic rollback if they degrade.
- **Novelty / primacy effects**: users may react differently simply because an experience is new; consider longer run times or holdout groups.
- **Multiple testing**: when running many experiments or variants, apply corrections (Bonferroni, false-discovery rate) or use sequential methods properly.

## Variance Reduction Techniques

### CUPED (Controlled-experiment Using Pre-Experiment Data)

CUPED uses a pre-experiment covariate (e.g., user’s historical conversion rate) to reduce variance of the metric, increasing power without increasing sample size.

Adjusted metric for each unit:

$$ Y_{adjusted} = Y - \theta (X - \bar{X}) $$

where $X$ is the pre-experiment covariate and $\theta$ is chosen to minimize variance (essentially the regression coefficient).

### Stratification

Randomize within strata (country, device type, new vs returning user) and analyze with a stratified estimator. Improves precision when strata differ in baseline rates.

## A/B Testing Model Versions in Production

### System design checklist

1. **Deterministic assignment**  
   Hash user/session ID → consistent variant. Enables proper analysis and avoids cross-contamination.

2. **Traffic routing layer**  
   Low-latency service that routes requests to Model A or Model B.

3. **Logging & instrumentation**  
   Log assignment, features, model outputs, and downstream metric. Must be joinable by unit ID.

4. **Guardrails & automatic rollback**  
   Monitor secondary metrics; roll back if they breach thresholds.

5. **Analysis pipeline**  
   - Compute primary metric by variant  
   - Run the appropriate test (two-proportion z-test, t-test, or CUPED-adjusted)  
   - Check SRM and other validity threats  
   - Report confidence intervals, not only p-values

### What must be true for trustworthy results

- Random (or properly randomized) assignment
- Consistent assignment per unit
- Pre-specified metric and analysis plan
- Adequate power
- No unaccounted interference
- SRM check passes
- Practical significance is considered

## Common Pitfalls

- Peeking and stopping early (inflates false-positive rate)
- Changing the metric after seeing results
- Ignoring interference in ranking or recommendation systems
- Instrumentation bugs that cause SRM or missing data
- Focusing only on statistical significance and ignoring effect size
- Running underpowered tests

## Relation to Other Notes

- Statistical foundations: [inferential_statistics.md](inferential_statistics.md)
- Two-proportion z-test implementation: [practical_interview_solutions.md](practical_interview_solutions.md)
- Bias and sampling: [inferential_statistics.md](inferential_statistics.md), [codebasics_key_takeaways.md](codebasics_key_takeaways.md)

---

**Last updated**: November 2026
