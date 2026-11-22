# Practical Python Examples

Runnable patterns that implement the concepts in the notes. Requires `numpy`, `scipy`, and `pandas`.

## Descriptive Statistics and Outlier Removal

```python
import numpy as np
import pandas as pd
from scipy import stats

data = pd.Series([1, 2, 2, 3, 4, 5, 100])  # 100 is an outlier
print(data.describe())

# Z-score method
z = np.abs(stats.zscore(data))
clean_z = data[z < 3]

# IQR method
Q1, Q3 = data.quantile(0.25), data.quantile(0.75)
IQR = Q3 - Q1
clean_iqr = data[(data >= Q1 - 1.5 * IQR) & (data <= Q3 + 1.5 * IQR)]
```

## Confidence Interval for the Mean

```python
sample = np.random.normal(50, 10, 30)
n = len(sample)
mean = sample.mean()
se = stats.sem(sample)
ci = stats.t.interval(0.95, df=n-1, loc=mean, scale=se)
print(f"95% CI: {ci}")
```

## One-Sample T-Test

```python
# H0: population mean = 72
t_stat, p_value = stats.ttest_1samp(exam_scores, 72)
```

## Two-Sample Test (A/B)

```python
# Welch's t-test (does not assume equal variance)
t_stat, p_value = stats.ttest_ind(design_a, design_b, equal_var=False)
```

## Two-Proportion Z-Test (conversion rates)

```python
import math

def two_proportion_z_test(x1, n1, x2, n2):
    p1, p2 = x1 / n1, x2 / n2
    p_pool = (x1 + x2) / (n1 + n2)
    se = math.sqrt(p_pool * (1 - p_pool) * (1/n1 + 1/n2))
    z = (p2 - p1) / se
    p_value = math.erfc(abs(z) / math.sqrt(2))
    return z, p_value

# Example: 20% vs 24% on 1,000 users each
print(two_proportion_z_test(200, 1000, 240, 1000))
```

## Chi-Squared Tests

```python
# Goodness of fit
observed = [25, 30, 20, 25]
expected = [25, 25, 25, 25]
chi2, p = stats.chisquare(observed, expected)

# Test of independence
from scipy.stats import chi2_contingency
table = np.array([[30, 10], [20, 40]])
chi2, p, dof, expected = chi2_contingency(table)
```

## Sample Ratio Mismatch (SRM) Check

```python
from scipy.stats import chisquare

# Observed traffic: 4800 control, 5200 treatment; expected 50/50 on 10,000
observed = [4800, 5200]
expected = [5000, 5000]
chi2, p = chisquare(observed, expected)
# If p is small, SRM is present → investigate assignment bug
```

## Central Limit Theorem Illustration

```python
population = np.random.exponential(scale=50, size=10000)  # skewed
sample_means = [np.random.choice(population, 30).mean() for _ in range(1000)]
# The distribution of sample_means is approximately normal
```

These snippets correspond to the heights, telecom, A/B, phone-sales, exam-score, and electricity-bill examples discussed in the conceptual notes. See also [ab_testing.md](ab_testing.md) for full experiment-design guidance.
