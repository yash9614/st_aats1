# Practical Statistics Interview Questions

Coding-style questions focused on numerically stable implementations and common applied techniques. Implement using NumPy and the standard library only (no SciPy / statsmodels) unless noted.

**Working solutions**: [practical_interview_solutions.md](practical_interview_solutions.md)

## 1. Online Mean and Variance (Welford)

**Problem**: Compute the mean and sample variance (divide by n−1) of a stream of values in a single pass, without storing the values. Must remain accurate when values are very large and close together.

**Constraints**: 2 ≤ len(values) ≤ 10⁷. Return [mean, sample_variance].

## 2. Sample vs Population Variance

**Problem**: Compute variance and standard deviation. If `sample=True`, divide by n−1; if `False`, divide by n. Return [variance, std].

## 3. Two-Proportion z-Test

**Problem**: Given x₁ successes out of n₁ and x₂ out of n₂, compute the z-statistic using the pooled proportion under H₀ and the two-sided p-value. Return [z, p_value]. z is positive when group B converts better.

## 4. Outliers by Median Absolute Deviation (Modified Z-Score)

**Problem**: Flag outliers with the modified z-score M = 0.6745 × (x − median) / MAD. Return indices where |M| > threshold (usually 3.5), in ascending order.

## 5. Variance Inflation Factor (VIF)

**Problem**: For each predictor j, regress it on all other predictors (with intercept), obtain R²ⱼ, and set VIFⱼ = 1 / (1 − R²ⱼ). Return the VIFs in column order.

## 6. Weighted Least Squares

**Problem**: Fit y = a + b·x by weighted least squares. Minimize Σ wᵢ(yᵢ − a − b·xᵢ)² by rescaling rows with √w and solving ordinary least squares. Return [a, b].

## 7. Ridge Regression in Closed Form

**Problem**: Fit ridge regression with an intercept that is not penalized. Center X and y, solve for the slopes, then recover the intercept. Return coefficients with intercept first.

## 8. OLS Coefficients and Standard Errors

**Problem**: Fit OLS with an intercept and return coefficients and standard errors. Residual variance = RSS / (n − p). Return [coefficients, standard_errors].

## 9. Confidence Interval for Relative Lift

**Problem**: Return [lift, lower, upper] where lift = p₂/p₁ − 1. Use the delta method for the SE of the ratio and a two-sided normal interval.

## 10. Deterministic Experiment Bucketing

**Problem**: Assign users to experiment buckets deterministically so a user always lands in the same bucket and different experiments are independent. For each user ID, hash the string f"{salt}:{user_id}" with MD5, read the hex digest as an integer, and take it modulo n_buckets. Return the bucket for each user in order.

**Constraints**: 1 ≤ len(user_ids) ≤ 10⁶, 2 ≤ n_buckets ≤ 10⁴. Use hashlib.md5. Do not use Python’s built-in hash().

## 11. Bayes' Rule for a Rare-Event Detector

**Problem**: A detector flags a rare event. Given the prior probability of the event, the detector's sensitivity P(alarm | event) and its false positive rate P(alarm | no event), return P(event | alarm) using Bayes' rule.

**Constraints**: 0 < prior < 1, 0 < sensitivity ≤ 1, 0 ≤ false_positive_rate < 1.

## 12. Expected Value of a Dice Game

**Problem**: You can roll a fair die with `sides` faces up to `n_rolls` times. After each roll you either stop and collect the face value, or roll again — but you must keep the last roll. Playing optimally, what is your expected payoff? Use dynamic programming.

**Constraints**: 1 ≤ n_rolls ≤ 1000, 2 ≤ sides ≤ 100. Faces are 1 … sides, equally likely.

## 13. Regression Discontinuity Estimate

**Problem**: Estimate the effect of a policy that applies above a cutoff. Using only observations within `bandwidth` of the cutoff, fit a separate straight line on each side (x < cutoff and x ≥ cutoff), evaluate both at the cutoff, and return the jump: right value − left value.

**Constraints**: At least two distinct x values on each side within the bandwidth. Use np.polyfit of degree 1 on each side.

## 14. Exact Binomial Test

**Problem**: Run an exact two-sided binomial test. Given `k` successes in `n` trials and a null success probability `p`, return the p-value. Use the "minimum likelihood" definition: sum the probabilities of every outcome that is no more likely than the observed one. Treat outcomes whose probability is within a relative tolerance of `1e-7` of the observed probability as equally likely.

**Constraints**: 1 ≤ n ≤ 1000, 0 ≤ k ≤ n, 0 < p < 1. Use `math.comb`. Cap the p-value at 1. No SciPy.

## 15. Comparing Two Poisson Rates

**Problem**: Compare how often something happens in two fleets (e.g., disengagements per 10,000 miles). Each fleet has a count of events over some exposure. Estimate the rate ratio (B / A) and test whether it differs from 1 using the log rate ratio, whose standard error is √(1/events_A + 1/events_B). Return [rate_ratio, z, p_value] with a two-sided p-value.

**Constraints**: Event counts are positive integers; exposures are positive. Use the normal approximation on the log rate ratio and `math.erfc` for the two-sided p-value.

## 16. Build a Recommendation System (System Design)

**Problem**: Walk through how you would build a recommendation system.

## 17. Performers with MapReduce (System Design)

**Problem**: How would you join two data files (customers, sales) and report the top 10 performers with MapReduce?

---

These questions complement the conceptual interview questions in [statistics_interview_questions.md](statistics_interview_questions.md) and the A/B testing guide in [ab_testing.md](ab_testing.md).
