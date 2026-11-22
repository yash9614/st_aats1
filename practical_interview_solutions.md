# Practical Interview Questions — Solutions

Working implementations using only NumPy and the standard library (no SciPy / statsmodels) unless noted.

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
    x, y, w = (np.asarray(v, dtype=float) for v in (x, y, w))
    sqrt_w = np.sqrt(w)
    A = np.column_stack([np.ones(len(x)), x])
    A_w = A * sqrt_w[:, None]
    y_w = y * sqrt_w
    beta, _, _, _ = np.linalg.lstsq(A_w, y_w, rcond=None)
    return beta.tolist()
```

## 7. Ridge Regression in Closed Form

```python
import numpy as np

def ridge_regression(X, y, lam):
    X = np.asarray(X, dtype=float)
    y = np.asarray(y, dtype=float)
    x_mean = X.mean(axis=0)
    y_mean = y.mean()
    Xc = X - x_mean
    yc = y - y_mean
    k = X.shape[1]
    beta = np.linalg.solve(Xc.T @ Xc + lam * np.eye(k), Xc.T @ yc)
    intercept = y_mean - x_mean @ beta
    return [float(intercept)] + beta.tolist()
```

## 8. OLS Coefficients and Standard Errors

```python
import numpy as np

def ols_with_se(X, y):
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

## 10. Deterministic Experiment Bucketing

```python
import hashlib

def assign_buckets(user_ids, salt, n_buckets):
    """
    Deterministic bucket assignment via MD5 hash of "{salt}:{user_id}".
    :rtype: List[int]
    """
    buckets = []
    for uid in user_ids:
        key = f"{salt}:{uid}"
        digest = hashlib.md5(key.encode("utf-8")).hexdigest()
        buckets.append(int(digest, 16) % n_buckets)
    return buckets
```

## 11. Bayes' Rule for a Rare-Event Detector

```python
def alarm_posterior(prior, sensitivity, false_positive_rate):
    """
    P(event | alarm) via Bayes' rule.
    :rtype: float
    """
    true_alarms = sensitivity * prior
    false_alarms = false_positive_rate * (1 - prior)
    return true_alarms / (true_alarms + false_alarms)
```

## 12. Expected Value of a Dice Game

```python
def dice_game_value(n_rolls, sides=6):
    """
    Optimal expected value of a dice game with up to n_rolls.
    Dynamic programming: keep a face only if it beats the value of continuing.
    :rtype: float
    """
    faces = range(1, sides + 1)
    # Value with one roll left
    value = sum(faces) / sides
    for _ in range(n_rolls - 1):
        continue_value = value
        value = sum(max(f, continue_value) for f in faces) / sides
    return value
```

## 13. Regression Discontinuity Estimate

```python
import numpy as np

def rdd_estimate(x, y, cutoff, bandwidth):
    """
    Local linear regression discontinuity estimate of the jump at the cutoff.
    :rtype: float   # right value - left value at the cutoff
    """
    x = np.asarray(x, dtype=float)
    y = np.asarray(y, dtype=float)
    near = np.abs(x - cutoff) <= bandwidth
    left = near & (x < cutoff)
    right = near & (x >= cutoff)
    # Fit degree-1 polynomials using (x - cutoff) so intercepts are values at cutoff
    b_l, a_l = np.polyfit(x[left] - cutoff, y[left], 1)
    b_r, a_r = np.polyfit(x[right] - cutoff, y[right], 1)
    return float(a_r - a_l)
```

## 14. Build a Recommendation System (System Design Outline)

```text
High-level design:
1. Objective & metrics
   - Primary: engagement (CTR, watch time, conversion)
   - Secondary: diversity, novelty, fairness, latency

2. Candidate generation (retrieval)
   - Collaborative filtering (user-user or item-item)
   - Content-based (embeddings of items/users)
   - Popularity / trending as a baseline or fallback
   - Two-tower models or approximate nearest neighbors for scale

3. Ranking
   - Pointwise, pairwise, or listwise models
   - Features: user history, item features, context, interaction signals
   - Offline training + online serving

4. Cold start & exploration
   - Content-based or popularity for new users/items
   - Exploration strategies (epsilon-greedy, Thompson sampling, bandits)

5. Evaluation
   - Offline: NDCG, MAP, recall@k
   - Online: A/B tests on engagement and guardrail metrics

6. Infrastructure
   - Feature store, model serving with low latency
   - Logging for training data
   - Experimentation platform for A/B tests

Key trade-offs: freshness vs latency, exploration vs exploitation, accuracy vs diversity.
```

---

All solutions match the expected test-case behavior described in [practical_interview_questions.md](practical_interview_questions.md). See also [ab_testing.md](ab_testing.md) for experiment design context and [inferential_statistics.md](inferential_statistics.md) for Bayes and hypothesis-testing foundations.
