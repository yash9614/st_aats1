# Practical Interview Questions — Solutions

Working implementations using only NumPy and the standard library (no SciPy / statsmodels).

## 1. Online Mean and Variance (Welford)

```python
import numpy as np

def running_stats(values):
    n = 0
    mean = 0.0
    M2 = 0.0

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
    arr = np.asarray(values, dtype=float)
    n = len(arr)
    mean = arr.mean()
    ss = np.sum((arr - mean) ** 2)
    divisor = (n - 1) if sample else n
    variance = ss / divisor
    std = np.sqrt(variance)
    return [variance, std]
```

## 3. Two-Proportion z-Test

```python
import math

def two_proportion_z_test(x1, n1, x2, n2):
    p1 = x1 / n1
    p2 = x2 / n2
    p_pool = (x1 + x2) / (n1 + n2)
    se = math.sqrt(p_pool * (1 - p_pool) * (1 / n1 + 1 / n2))
    z = (p2 - p1) / se
    p_value = math.erfc(abs(z) / math.sqrt(2))
    return [z, p_value]
```

## 4. Outliers by Median Absolute Deviation (Modified Z-Score)

```python
import numpy as np

def mad_outliers(values, threshold=3.5):
    arr = np.asarray(values, dtype=float)
    med = np.median(arr)
    abs_dev = np.abs(arr - med)
    mad = np.median(abs_dev)
    M = 0.6745 * (arr - med) / mad
    outlier_indices = np.where(np.abs(M) > threshold)[0]
    return sorted(outlier_indices.tolist())
```

## 5. Variance Inflation Factor (VIF)

```python
import numpy as np

def vif(X):
    X = np.asarray(X, dtype=float)
    n, k = X.shape
    vifs = []

    for j in range(k):
        y = X[:, j]
        others = np.delete(X, j, axis=1)
        A = np.column_stack([np.ones(n), others])
        beta, _, _, _ = np.linalg.lstsq(A, y, rcond=None)
        y_hat = A @ beta
        y_mean = y.mean()
        ss_tot = np.sum((y - y_mean) ** 2)
        ss_res = np.sum((y - y_hat) ** 2)
        r2 = 1 - ss_res / ss_tot if ss_tot > 0 else 0.0
        vif_j = 1.0 / (1.0 - r2) if r2 < 1.0 else np.inf
        vifs.append(vif_j)

    return vifs
```

## 6. Weighted Least Squares

```python
import numpy as np

def weighted_least_squares(x, y, w):
    """
    Fit y = a + b*x by weighted least squares.
    Rescale rows by sqrt(w) and solve ordinary least squares.
    :rtype: List[float]   # [intercept, slope]
    """
    x, y, w = (np.asarray(v, dtype=float) for v in (x, y, w))
    sqrt_w = np.sqrt(w)
    # Design matrix with intercept
    A = np.column_stack([np.ones(len(x)), x])
    # Rescale rows
    A_w = A * sqrt_w[:, None]
    y_w = y * sqrt_w
    # Ordinary least squares on rescaled data
    beta, _, _, _ = np.linalg.lstsq(A_w, y_w, rcond=None)
    return beta.tolist()
```

## 7. Ridge Regression in Closed Form

```python
import numpy as np

def ridge_regression(X, y, lam):
    """
    Ridge regression with unpenalized intercept.
    Center data, solve for slopes, recover intercept.
    :rtype: List[float]   # [intercept, b1, ..., bk]
    """
    X = np.asarray(X, dtype=float)
    y = np.asarray(y, dtype=float)
    x_mean = X.mean(axis=0)
    y_mean = y.mean()
    Xc = X - x_mean
    yc = y - y_mean
    k = X.shape[1]
    # Penalized normal equations on centered data
    beta = np.linalg.solve(Xc.T @ Xc + lam * np.eye(k), Xc.T @ yc)
    intercept = y_mean - x_mean @ beta
    return [float(intercept)] + beta.tolist()
```

## 8. OLS Coefficients and Standard Errors

```python
import numpy as np

def ols_with_se(X, y):
    """
    OLS with intercept. Return coefficients and standard errors.
    Residual variance = RSS / (n - p).
    :rtype: List[List[float]]   # [coefficients, standard_errors]
    """
    X = np.column_stack([np.ones(len(y)), np.asarray(X, dtype=float)])
    y = np.asarray(y, dtype=float)
    n, p = X.shape
    XtX_inv = np.linalg.inv(X.T @ X)
    beta = XtX_inv @ X.T @ y
    rss = np.sum((y - X @ beta) ** 2)
    sigma2 = rss / (n - p)
    se = np.sqrt(np.diag(sigma2 * XtX_inv))
    return [beta.tolist(), se.tolist()]
```

## 9. Confidence Interval for Relative Lift

```python
import math
from statistics import NormalDist

def relative_lift_ci(x1, n1, x2, n2, alpha=0.05):
    """
    Relative lift with delta-method confidence interval.
    lift = p2/p1 - 1
    :rtype: List[float]   # [lift, lower, upper]
    """
    p1 = x1 / n1
    p2 = x2 / n2
    v1 = p1 * (1 - p1) / n1
    v2 = p2 * (1 - p2) / n2
    ratio = p2 / p1
    se = ratio * math.sqrt(v1 / p1**2 + v2 / p2**2)
    z = NormalDist().inv_cdf(1 - alpha / 2)
    lift = ratio - 1
    return [lift, lift - z * se, lift + z * se]
```

---

All solutions match the expected test-case behavior described in [practical_interview_questions.md](practical_interview_questions.md). Relative lift CI is especially relevant to A/B testing analysis; see [ab_testing.md](ab_testing.md).
