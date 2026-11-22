# Practical Python Examples

Concise, runnable patterns for common statistics tasks using `numpy`, `scipy`, and `pandas`. These complement the conceptual notes.

## Descriptive Statistics & Outliers

```python
import numpy as np
import pandas as pd
from scipy import stats

# Summary stats
data = pd.Series([1, 2, 2, 3, 4, 5, 100])  # 100 is an outlier
print(data.describe())

# Z-score outlier removal
z = np.abs(stats.zscore(data))
clean = data[z < 3]

# IQR method
Q1, Q3 = data.quantile(0.25), data.quantile(0.75)
IQR = Q3 - Q1
clean_iqr = data[(data >= Q1 - 1.5*IQR) & (data <= Q3 + 1.5*IQR)]
```

## Confidence Interval

```python
from scipy import stats
import numpy as np

sample = np.random.normal(50, 10, 30)
n = len(sample)
mean = sample.mean()
se = stats.sem(sample)
ci = stats.t.interval(0.95, df=n-1, loc=mean, scale=se)
print(f"95% CI: {ci}")
```

## One-Sample T-Test

```python
# H0: mean = 72
t_stat, p_value = stats.ttest_1samp(exam_scores, 72)
# For one-tailed (greater): p_one = p_value / 2 if t_stat > 0 else 1 - p_value/2
```

## Two-Sample Z / T-Test (A/B)

```python
# Two independent samples
t_stat, p_value = stats.ttest_ind(design_a, design_b, equal_var=False)  # Welch's
# Or for large samples / known variance, use manual Z formula
```

## Chi-Squared Tests

```python
# Goodness of fit
observed = [25, 30, 20, 25]
expected = [25, 25, 25, 25]
chi2, p = stats.chisquare(observed, expected)

# Independence (contingency table)
from scipy.stats import chi2_contingency
table = np.array([[30, 10], [20, 40]])  # rows: age groups, cols: phone types
chi2, p, dof, expected = chi2_contingency(table)
```

## Central Limit Theorem Demonstration

```python
# Sampling distribution of the mean from a skewed population
population = np.random.exponential(scale=50, size=10000)
sample_means = [np.random.choice(population, 30).mean() for _ in range(1000)]
# sample_means will be approximately normal
```

These patterns map directly to the examples discussed in the conceptual notes (heights, telecom, A/B tests, phone sales, exam scores, etc.).
