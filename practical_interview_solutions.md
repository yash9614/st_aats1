# Practical Interview Questions — Solutions

Working implementations using only NumPy and the standard library (no SciPy / statsmodels) unless noted. Each solution is self-contained and matches the expected test-case behavior.

## 1. Online Mean and Variance (Welford)

Numerically stable single-pass algorithm. Avoids catastrophic cancellation when values are large and close together.

```python
import numpy as np

def running_stats(values):
    """
    Online mean and sample variance (Bessel's correction) via Welford's method.
    :rtype: List[float]  # [mean, sample_variance]
    """
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
    return [mean, M2 / (n - 1)]
```

## 2. Sample vs Population Variance

```python
import numpy as np

def variance_and_std(values, sample):
    """
    Variance and standard deviation.
    sample=True  → divide by n-1 (unbiased sample variance)
    sample=False → divide by n   (population variance)
    :rtype: List[float]  # [variance, std]
    """
    arr = np.asarray(values, dtype=float)
    n = len(arr)
    mean = arr.mean()
    ss = np.sum((arr - mean) ** 2)
    divisor = (n - 1) if sample else n
    variance = ss / divisor
    return [variance, np.sqrt(variance)]
```

## 3. Two-Proportion z-Test

Uses the pooled proportion under H₀ for the standard error. Two-sided p-value via `math.erfc`.

```python
import math

def two_proportion_z_test(x1, n1, x2, n2):
    """
    Two-sided z-test for the difference of two proportions.
    z is positive when group B converts better.
    :rtype: List[float]  # [z, p_value]
    """
    p1 = x1 / n1
    p2 = x2 / n2
    p_pool = (x1 + x2) / (n1 + n2)
    se = math.sqrt(p_pool * (1 - p_pool) * (1 / n1 + 1 / n2))
    z = (p2 - p1) / se
    p_value = math.erfc(abs(z) / math.sqrt(2))
    return [z, p_value]
```

## 4. Outliers by Median Absolute Deviation (Modified Z-Score)

More robust than the classical z-score because it uses the median and MAD instead of the mean and standard deviation.

```python
import numpy as np

def mad_outliers(values, threshold=3.5):
    """
    Modified z-score outliers: |0.6745 * (x - median) / MAD| > threshold.
    Returns indices in ascending order.
    """
    arr = np.asarray(values, dtype=float)
    med = np.median(arr)
    mad = np.median(np.abs(arr - med))
    if mad == 0:
        return []  # all values identical
    M = 0.6745 * (arr - med) / mad
    return sorted(np.where(np.abs(M) > threshold)[0].tolist())
```

## 5. Variance Inflation Factor (VIF)

```python
import numpy as np

def vif(X):
    """
    VIF for each column. VIF_j = 1 / (1 - R²_j) where R²_j comes from regressing
    column j on all other columns (with intercept).
    """
    X = np.asarray(X, dtype=float)
    n, k = X.shape
    vifs = []

    for j in range(k):
        y = X[:, j]
        others = np.delete(X, j, axis=1)
        A = np.column_stack([np.ones(n), others])
        beta, _, _, _ = np.linalg.lstsq(A, y, rcond=None)
        y_hat = A @ beta
        ss_tot = np.sum((y - y.mean()) ** 2)
        ss_res = np.sum((y - y_hat) ** 2)
        r2 = 1 - ss_res / ss_tot if ss_tot > 0 else 0.0
        vifs.append(1.0 / (1.0 - r2) if r2 < 1.0 else np.inf)

    return vifs
```

## 6. Weighted Least Squares

Rescale each row by √w so ordinary least squares on the rescaled data minimizes the weighted sum of squares.

```python
import numpy as np

def weighted_least_squares(x, y, w):
    """
    Fit y = a + b*x by weighted least squares.
    :rtype: List[float]  # [intercept, slope]
    """
    x, y, w = (np.asarray(v, dtype=float) for v in (x, y, w))
    sqrt_w = np.sqrt(w)
    A = np.column_stack([np.ones(len(x)), x])
    beta, _, _, _ = np.linalg.lstsq(A * sqrt_w[:, None], y * sqrt_w, rcond=None)
    return beta.tolist()
```

## 7. Ridge Regression in Closed Form

Intercept is not penalized. Centering lets us solve for the slopes alone, then recover the intercept.

```python
import numpy as np

def ridge_regression(X, y, lam):
    """
    Ridge regression with unpenalized intercept.
    :rtype: List[float]  # [intercept, b1, ..., bk]
    """
    X = np.asarray(X, dtype=float)
    y = np.asarray(y, dtype=float)
    x_mean = X.mean(axis=0)
    y_mean = y.mean()
    Xc, yc = X - x_mean, y - y_mean
    k = X.shape[1]
    beta = np.linalg.solve(Xc.T @ Xc + lam * np.eye(k), Xc.T @ yc)
    intercept = y_mean - x_mean @ beta
    return [float(intercept)] + beta.tolist()
```

## 8. OLS Coefficients and Standard Errors

```python
import numpy as np

def ols_with_se(X, y):
    """
    OLS with intercept. Residual variance = RSS / (n - p).
    :rtype: List[List[float]]  # [coefficients, standard_errors]
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

Delta-method standard error for the ratio of two proportions.

```python
import math
from statistics import NormalDist

def relative_lift_ci(x1, n1, x2, n2, alpha=0.05):
    """
    Relative lift = p2/p1 - 1 with delta-method confidence interval.
    :rtype: List[float]  # [lift, lower, upper]
    """
    p1, p2 = x1 / n1, x2 / n2
    v1 = p1 * (1 - p1) / n1
    v2 = p2 * (1 - p2) / n2
    ratio = p2 / p1
    se = ratio * math.sqrt(v1 / p1**2 + v2 / p2**2)
    z = NormalDist().inv_cdf(1 - alpha / 2)
    lift = ratio - 1
    return [lift, lift - z * se, lift + z * se]
```

## 10. Deterministic Experiment Bucketing

Stable, experiment-specific assignment. Different salts produce independent assignments. Do not use Python’s built-in `hash()` (randomized per process).

```python
import hashlib

def assign_buckets(user_ids, salt, n_buckets):
    """
    Deterministic bucket assignment via MD5 of "{salt}:{user_id}".
    :rtype: List[int]
    """
    buckets = []
    for uid in user_ids:
        key = f"{salt}:{uid}".encode("utf-8")
        digest = hashlib.md5(key).hexdigest()
        buckets.append(int(digest, 16) % n_buckets)
    return buckets
```

## 11. Bayes' Rule for a Rare-Event Detector

Even a highly sensitive detector can produce mostly false alarms when the event is rare.

```python
def alarm_posterior(prior, sensitivity, false_positive_rate):
    """
    P(event | alarm) = [sensitivity * prior] / [sensitivity * prior + fpr * (1 - prior)]
    :rtype: float
    """
    true_alarms = sensitivity * prior
    false_alarms = false_positive_rate * (1 - prior)
    return true_alarms / (true_alarms + false_alarms)
```

## 12. Expected Value of a Dice Game

Optimal policy: with rolls remaining, keep a face only if it exceeds the expected value of continuing. Solved by backward induction.

```python
def dice_game_value(n_rolls, sides=6):
    """
    Optimal expected value of a dice game with up to n_rolls.
    :rtype: float
    """
    faces = range(1, sides + 1)
    value = sum(faces) / sides          # one roll left
    for _ in range(n_rolls - 1):
        continue_value = value
        value = sum(max(f, continue_value) for f in faces) / sides
    return value
```

## 13. Regression Discontinuity Estimate

Local linear regression on each side of the cutoff. Using (x − cutoff) as the predictor makes each intercept the fitted value at the cutoff.

```python
import numpy as np

def rdd_estimate(x, y, cutoff, bandwidth):
    """
    Local linear RDD estimate of the jump at the cutoff.
    :rtype: float  # right value - left value at the cutoff
    """
    x = np.asarray(x, dtype=float)
    y = np.asarray(y, dtype=float)
    near = np.abs(x - cutoff) <= bandwidth
    left = near & (x < cutoff)
    right = near & (x >= cutoff)
    # Intercepts are the fitted values at the cutoff
    _, a_l = np.polyfit(x[left] - cutoff, y[left], 1)
    _, a_r = np.polyfit(x[right] - cutoff, y[right], 1)
    return float(a_r - a_l)
```

## 14. Exact Binomial Test

Two-sided exact binomial test using the minimum-likelihood definition. Outcomes whose probability is within a relative tolerance of 1e-7 of the observed probability are treated as equally likely. The p-value is capped at 1.

```python
import math

def binomial_test(k, n, p):
    """
    Exact two-sided binomial test (minimum-likelihood definition).
    :rtype: float
    """
    pmf = [
        math.comb(n, i) * p**i * (1 - p) ** (n - i)
        for i in range(n + 1)
    ]
    observed = pmf[k]
    p_value = sum(q for q in pmf if q <= observed * (1 + 1e-7))
    return min(1.0, p_value)
```

## 15. Comparing Two Poisson Rates

Rate ratio of two Poisson processes. The log rate ratio is approximately normal with standard error √(1/events_A + 1/events_B).

```python
import math

def poisson_rate_test(events_a, exposure_a, events_b, exposure_b):
    """
    Compare two Poisson rates. Returns [rate_ratio, z, p_value].
    rate_ratio = (events_b / exposure_b) / (events_a / exposure_a)
    z is the log rate ratio divided by its SE.
    :rtype: List[float]
    """
    rate_a = events_a / exposure_a
    rate_b = events_b / exposure_b
    rate_ratio = rate_b / rate_a
    log_ratio = math.log(rate_ratio)
    se = math.sqrt(1 / events_a + 1 / events_b)
    z = log_ratio / se
    p_value = math.erfc(abs(z) / math.sqrt(2))
    return [rate_ratio, z, p_value]
```

## 16. Build a Recommendation System (System Design Outline)

```text
High-level design

1. Objective & metrics
   - Primary: engagement (CTR, watch time, conversion, retention)
   - Secondary: diversity, novelty, fairness, freshness, latency

2. Candidate generation (retrieval)
   - Collaborative filtering (user–user or item–item)
   - Content-based (embeddings of items and users)
   - Popularity / trending as a baseline or fallback
   - Two-tower models + approximate nearest neighbors for scale

3. Ranking
   - Pointwise, pairwise, or listwise models
   - Features: user history, item features, context, real-time signals
   - Offline training with online serving

4. Cold start & exploration
   - Content-based or popularity for new users/items
   - Exploration: epsilon-greedy, Thompson sampling, contextual bandits

5. Evaluation
   - Offline: NDCG, MAP, recall@k, calibration
   - Online: A/B tests on primary metrics plus guardrails (latency, diversity)

6. Infrastructure
   - Feature store, low-latency model serving
   - Logging for training data and offline evaluation
   - Experimentation platform

Key trade-offs
- Freshness vs latency
- Exploration vs exploitation
- Accuracy vs diversity / fairness
- Model complexity vs serving cost
```

## 17. Performers with MapReduce (System Design Outline)

```text
Goal: Join customers and sales, then report the top 10 performers (e.g., by total sales).

Assumptions
- customers: customer_id, name, region, …
- sales: customer_id, amount, date, …
- Performer = customer with the highest total sales amount

MapReduce plan

1. Map (sales file)
   - Emit (customer_id, amount) for every sale

2. Map (customers file)
   - Emit (customer_id, ("CUSTOMER", name, region, …)) so the join key is the same

3. Shuffle / sort by customer_id

4. Reduce (per customer_id)
   - Separate the customer record from the list of sales amounts
   - Sum the amounts
   - Emit (total_sales, customer_info)   # secondary sort key later, or just collect

5. Top-10 (second job or in-memory if small)
   - Option A (simple): collect all (total, customer) pairs in the reducer output and sort globally (feasible if the number of customers fits in memory after aggregation)
   - Option B (scalable): second MapReduce job that uses a composite key or a top-N pattern (each reducer keeps a local heap of size 10, then a final merge produces the global top 10)

Output
- Top 10 customers by total sales, with name / region and the total amount

Notes
- Handle customers with no sales (total = 0) if required
- Handle sales with missing customer records (skip or log)
- For very large data, the top-N pattern avoids a full global sort
```

---

All solutions match the expected test-case behavior in [practical_interview_questions.md](practical_interview_questions.md). See also [ab_testing.md](ab_testing.md) for experiment-design context and [inferential_statistics.md](inferential_statistics.md) for Bayes and hypothesis-testing foundations.
