# Practical Statistics Interview Questions

Coding-style questions focused on numerically stable implementations and common applied techniques. Implement using NumPy and the standard library only (no SciPy / statsmodels).

**Working solutions**: [practical_interview_solutions.md](practical_interview_solutions.md)

## 1. Online Mean and Variance (Welford)

**Problem**: Compute the mean and sample variance (divide by n−1) of a stream of values in a single pass, without storing the values. Must remain accurate when values are very large and close together.

**Constraints**: 2 ≤ len(values) ≤ 10⁷. Return [mean, sample_variance].

**Hint**: Track count, running mean, and running sum of squared deviations from the mean (Welford’s method).

## 2. Sample vs Population Variance

**Problem**: Compute variance and standard deviation. If `sample=True`, divide by n−1; if `False`, divide by n. Return [variance, std].

## 3. Two-Proportion z-Test

**Problem**: Given x₁ successes out of n₁ and x₂ out of n₂, compute the z-statistic using the pooled proportion under H₀ and the two-sided p-value. Return [z, p_value]. z is positive when group B converts better.

## 4. Outliers by Median Absolute Deviation (Modified Z-Score)

**Problem**: Flag outliers with the modified z-score M = 0.6745 × (x − median) / MAD. Return indices where |M| > threshold (usually 3.5), in ascending order.

## 5. Variance Inflation Factor (VIF)

**Problem**: For each predictor j, regress it on all other predictors (with intercept), obtain R²ⱼ, and set VIFⱼ = 1 / (1 − R²ⱼ). Return the VIFs in column order.

## 6. Weighted Least Squares

**Problem**: Fit a straight line y = a + b·x by weighted least squares. Minimize Σ wᵢ(yᵢ − a − b·xᵢ)². One way: multiply each row of the design matrix and of y by √wᵢ and solve ordinary least squares. Return [a, b].

**Constraints**: 2 ≤ n ≤ 10⁶; weights are positive.

**Hint**: Rescale each row by √w so that ordinary least squares on the rescaled data minimizes the weighted sum of squares.

**Test cases**:
- Equal weights → ordinary least squares
- Higher weight on one point → line leans toward that point
- Weights as inverse variances

## 7. Ridge Regression in Closed Form

**Problem**: Fit ridge regression with an intercept that is not penalized. Center X and y, solve β = (XcᵀXc + λI)⁻¹ Xcᵀyc for the slopes, then recover the intercept as mean(y) − mean(X)·β. Return the coefficients, intercept first.

**Constraints**: n ≥ 2, λ ≥ 0. The intercept is not penalized.

**Hint**: Centering lets you solve for the slopes alone; the intercept is recovered afterward so it is not shrunk.

**Test cases**:
- λ = 0 recovers ordinary least squares
- Large baseline: only the slope shrinks, not the intercept
- Two correlated predictors

## 8. OLS Coefficients and Standard Errors

**Problem**: Fit ordinary least squares with an intercept and return the coefficients and their standard errors. Add a column of ones to X, solve the normal equations, estimate residual variance as RSS / (n − p), and take SE = √diag(σ² (XᵀX)⁻¹). Return [coefficients, standard_errors], intercept first.

**Constraints**: n > p; X has full column rank. Do not use `lstsq` residuals for the variance.

**Hint**: Compute (XᵀX)⁻¹ once and use it for both the coefficients and the standard errors.

## 9. Confidence Interval for Relative Lift

**Problem**: Report an A/B test result as a relative lift with a confidence interval. Given x₁ of n₁ conversions in control and x₂ of n₂ in treatment, return [lift, lower, upper], where lift = p₂/p₁ − 1. Use the delta method for the standard error of the ratio:

SE = (p₂/p₁) · √(v₁/p₁² + v₂/p₂²) with vᵢ = pᵢ(1 − pᵢ)/nᵢ

and a two-sided normal interval.

**Constraints**: 0 < x₁ < n₁ and 0 < x₂ < n₂. Use `statistics.NormalDist().inv_cdf` for the critical value.

**Hint**: Both rates contribute uncertainty to the ratio. Start with each rate and its variance.

---

These questions complement the conceptual interview questions in [statistics_interview_questions.md](statistics_interview_questions.md) and the A/B testing guide in [ab_testing.md](ab_testing.md).
