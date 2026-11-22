# Practical Statistics Interview Questions

Coding-style questions focused on numerically stable implementations and common applied techniques. Implement using NumPy and the standard library only (no SciPy / statsmodels).

## 1. Online Mean and Variance (Welford)

**Problem**: Compute the mean and sample variance (divide by n−1) of a stream of values in a single pass, without storing the values. Must remain accurate when values are very large and close together (e.g., timestamps near 10⁹).

**Constraints**: 2 ≤ len(values) ≤ 10⁷. Return [mean, sample_variance].

**Hint**: Track count, running mean, and running sum of squared deviations from the mean (Welford’s method). The classic “n × mean² − sum of squares” formula loses precision for large close values.

**Test cases**:
- [1, 2, 3, 4] → [2.5, 1.666667]
- [1000000004, 1000000007, 1000000013, 1000000016] → [1000000010, 30.0]
- [100000000.5, 100000001.5, 100000002.5] → [100000001.5, 1.0]

## 2. Sample vs Population Variance

**Problem**: Compute variance and standard deviation. If `sample=True`, divide by n−1; if `False`, divide by n. Return [variance, std].

**Constraints**: len ≥ 1 (and ≥ 2 when sample=True). Implement yourself.

**Hint**: The only difference is the divisor.

**Test cases**:
- [2,4,4,4,5,5,7,9], sample=True → [4.571429, 2.13809]
- Same values, sample=False → [4.0, 2.0]
- [1,3], sample=True → [2.0, 1.414214]

## 3. Two-Proportion z-Test

**Problem**: Given x₁ successes out of n₁ and x₂ out of n₂, compute the z-statistic using the pooled proportion under H₀ and the two-sided p-value. Return [z, p_value]. z is positive when group B converts better.

**Constraints**: Use pooled proportion for the standard error. Use `math.erf` / `math.erfc` for the normal CDF. No SciPy.

**Hint**: Pooled rate = (x₁+x₂)/(n₁+n₂). SE is driven by the pooled rate; the difference of rates drives the statistic.

**Test cases**:
- x1=200, n1=1000, x2=240, n2=1000 → [2.159168, 0.030837]
- x1=50, n1=500, x2=50, n2=500 → [0.0, 1.0]
- x1=1000, n1=10000, x2=900, n2=10000 → [-2.411565, 0.015884]

## 4. Outliers by Median Absolute Deviation (Modified Z-Score)

**Problem**: Flag outliers with the modified z-score. For each value compute  
M = 0.6745 × (x − median) / MAD,  
where MAD is the median of absolute deviations from the median. Return indices where |M| > threshold (usually 3.5), in ascending order.

**Constraints**: MAD > 0. `np.median` is allowed.

**Hint**: First compute the median of the data, then the median of the absolute deviations from that median.

**Test cases**:
- [10,11,12,13,14,30], threshold=3.5 → [5]
- [10,11,12,13,14,20], threshold=3.5 → []
- [1..9,17,40], threshold=3.5 → [10]

## 5. Variance Inflation Factor (VIF)

**Problem**: For each predictor j, regress it on all other predictors (with intercept), obtain R²ⱼ, and set VIFⱼ = 1 / (1 − R²ⱼ). Return the VIFs in column order.

**Constraints**: X is n × k with n > k, 2 ≤ k ≤ 100. R² uses centered total sum of squares. Implement with NumPy only.

**Hint**: Loop over columns. For each column treat it as the target and the remaining columns (plus a column of ones) as predictors.

**Test cases**:
- Two correlated predictors → [3.083333, 3.083333]
- Centered nearly unrelated predictors → [1.0, 1.0]
- Three predictors that move together → high VIFs (e.g. ~32, ~33, ~100)

---

These questions complement the conceptual interview questions in [statistics_interview_questions.md](statistics_interview_questions.md). For theoretical background see the descriptive and inferential notes.
