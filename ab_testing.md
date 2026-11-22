# A/B Testing

## What is A/B Testing?

A/B testing (also called split testing or controlled experimentation) is a method of comparing two or more versions of a product, feature, or model by randomly assigning users to different variants and measuring the effect on a key metric.

- **A** = control (current version)
- **B** = treatment (new version)
- Goal: decide whether the observed difference is statistically significant and practically meaningful.

## Core Statistical Foundation

Most A/B tests reduce to a **two-sample hypothesis test** (or a two-proportion z-test when the metric is a rate).

### For continuous metrics (e.g., time on page, revenue)

$$ Z = \frac{\bar{x}_B - \bar{x}_A}{\sqrt{\frac{s_A^2}{n_A} + \frac{s_B^2}{n_B}}} $$

### For proportions (e.g., conversion rate)

Use the **pooled proportion** under $H_0$:

$$ p_{pool} = \frac{x_A + x_B}{n_A + n_B} $$

$$ SE = \sqrt{p_{pool}(1-p_{pool})\left(\frac{1}{n_A}+\frac{1}{n_B}\right)} $$

$$ z = \frac{p_B - p_A}{SE} $$

Two-sided p-value is obtained from the standard normal distribution.

See the working implementation in [practical_interview_solutions.md](practical_interview_solutions.md).

## Designing a Trustworthy Experiment

For results to be trustworthy, the following must hold:

### 1. Randomization
- Units (users, sessions, requests) are randomly assigned to control or treatment.
- Prevents systematic differences between groups.

### 2. Sufficient Sample Size / Power
- Pre-compute required sample size given:
  - Minimum detectable effect (MDE)
  - Desired power (usually 80%)
  - Significance level α (usually 0.05)
- Underpowered tests produce inconclusive or misleading results.

### 3. Clear Primary Metric
- Define the metric in advance (conversion rate, revenue per user, latency, etc.).
- Avoid changing the metric after seeing results (HARKing).

### 4. No Peeking / Sequential Testing Discipline
- Do not stop early just because the result looks significant (unless using proper sequential or Bayesian methods).
- Peeking inflates the false-positive rate.

### 5. Sample Ratio Mismatch (SRM) Check
- Verify that the observed traffic split matches the intended split.
- A significant mismatch indicates a bug in assignment or instrumentation.

### 6. Interference / Network Effects
- For model versions or features that can affect other users (ranking, recommendations, shared resources), simple user-level randomization may be invalid.
- Consider cluster randomization or other designs when interference is present.

### 7. Practical Significance
- Statistical significance alone is not enough.
- Evaluate whether the effect size is large enough to justify the cost of shipping.

## A/B Testing Model Versions in Production

When comparing different model versions (or feature sets) in production:

### System Design Requirements

1. **Deterministic assignment**
   - Hash user/session ID to a bucket so the same user consistently sees the same model version.
   - Enables proper analysis and avoids contamination.

2. **Traffic routing layer**
   - A service that routes requests to Model A or Model B according to the assignment.
   - Must be low-latency and reliable.

3. **Logging and instrumentation**
   - Log assignment, request features, model outputs, and the downstream metric (click, conversion, etc.).
   - Joinable by user/session ID.

4. **Guardrails**
   - Monitor latency, error rate, and other secondary metrics.
   - Automatic rollback if guardrail metrics degrade.

5. **Analysis pipeline**
   - Compute the primary metric by variant.
   - Run the appropriate statistical test (two-proportion z-test, t-test, or CUPED-adjusted estimator).
   - Check for SRM and other validity threats.

### What Must Be True for Trustworthy Results

| Requirement | Why it matters |
|-------------|----------------|
| Random (or properly randomized) assignment | Removes selection bias |
| Consistent assignment per unit | Prevents contamination |
| Pre-specified metric and analysis plan | Avoids p-hacking |
| Adequate power / sample size | Controls Type II error |
| No interference (or proper design for it) | Validates the independence assumption |
| SRM check passes | Detects assignment bugs |
| Practical significance considered | Ensures the win is worth shipping |

## Common Pitfalls

- **Peeking** and stopping early
- **Multiple testing** without correction when running many experiments or variants
- **Novelty / primacy effects** (users react differently to a new experience simply because it is new)
- **Instrumentation bugs** that cause SRM or missing data
- **Ignoring variance reduction** techniques (CUPED, stratification) that could improve power

## Relation to Other Notes

- Statistical foundations: [inferential_statistics.md](inferential_statistics.md)
- Two-proportion z-test implementation: [practical_interview_solutions.md](practical_interview_solutions.md)
- Bias and sampling issues: [inferential_statistics.md](inferential_statistics.md) and [codebasics_key_takeaways.md](codebasics_key_takeaways.md)

---

**Last updated**: November 2026
