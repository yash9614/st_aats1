# Practical Interview Questions — Solutions

Working implementations using only NumPy and the standard library (no SciPy / statsmodels).

## 1. Online Mean and Variance (Welford)

```python
import numpy as np

def running_stats(values):
    """
    Single-pass mean and sample variance using Welford's method.
    Accurate for large values that are close together.
    :type values: List[float]
    :rtype: List[float]   # [mean, sample_variance]
    """
    n = 0
    mean = 0.0
    M2 = 0.0  # sum of squared deviations from the current mean

    for x in values:
        n += 1
        delta = x - mean
        mean += delta / n
        delta2 = x - mean
        M2 += delta * delta2

    if n < 2:
        return [mean, 0.0]
    sample_variance = M2 / (n - 1)
    return [mean, sample_variance]
```

## 2. Sample vs Population Variance

```python
import numpy as np

def variance_and_std(values, sample):
    """
    :type values: List[float]
    :type sample: bool
    :rtype: List[float]   # [variance, std]
    """
    arr = np.asarray(values, dtype=float)
    n = len(arr)
    mean = arr.mean()
    # sum of squared deviations
    ss = np.sum((arr - mean) ** 2)
    divisor = (n - 1) if sample else n
    variance = ss / divisor
    std = np.sqrt(variance)
    return [variance, std]
```

## 3. Two-Proportion z-Test

```python
import math
import numpy as np

def two_proportion_z_test(x1, n1, x2, n2):
    """
    Two-sided two-proportion z-test using the pooled proportion.
    :rtype: List[float]   # [z, p_value]
    """
    p1 = x1 / n1
    p2 = x2 / n2
    p_pool = (x1 + x2) / (n1 + n2)

    se = math.sqrt(p_pool * (1 - p_pool) * (1 / n1 + 1 / n2))
    z = (p2 - p1) / se   # positive when B converts better

    # two-sided p-value via error function
    # P(|Z| > |z|) = erfc(|z| / sqrt(2))
    p_value = math.erfc(abs(z) / math.sqrt(2))
    return [z, p_value]
```

## 4. Outliers by Median Absolute Deviation (Modified Z-Score)

```python
import numpy as np

def mad_outliers(values, threshold=3.5):
    """
    Return indices of outliers using the modified z-score.
    M = 0.6745 * (x - median) / MAD
    :rtype: List[int]
    """
    arr = np.asarray(values, dtype=float)
    med = np.median(arr)
    abs_dev = np.abs(arr - med)
    mad = np.median(abs_dev)

    # modified z-scores
    M = 0.6745 * (arr - med) / mad
    outlier_indices = np.where(np.abs(M) > threshold)[0]
    return sorted(outlier_indices.tolist())
```

## 5. Variance Inflation Factor (VIF)

```python
import numpy as np

def vif(X):
    """
    Compute VIF for each predictor.
    VIF_j = 1 / (1 - R^2_j) where R^2_j comes from regressing
    column j on all other columns (with intercept).
    :type X: List[List[float]] or np.ndarray
    :rtype: List[float]
    """
    X = np.asarray(X, dtype=float)
    n, k = X.shape
    vifs = []

    for j in range(k):
        y = X[:, j]
        # predictors: intercept + all other columns
        others = np.delete(X, j, axis=1)
        A = np.column_stack([np.ones(n), others])

        # least squares: beta = (A^T A)^{-1} A^T y
        beta, _, _, _ = np.linalg.lstsq(A, y, rcond=None)
        y_hat = A @ beta

        # centered total sum of squares and residual sum of squares
        y_mean = y.mean()
        ss_tot = np.sum((y - y_mean) ** 2)
        ss_res = np.sum((y - y_hat) ** 2)
        r2 = 1 - ss_res / ss_tot if ss_tot > 0 else 0.0

        # VIF
        vif_j = 1.0 / (1.0 - r2) if r2 < 1.0 else np.inf
        vifs.append(vif_j)

    return vifs
```

---

All solutions match the expected test-case behavior described in [practical_interview_questions.md](practical_interview_questions.md).
