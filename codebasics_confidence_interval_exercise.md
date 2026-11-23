# Codebasics Chapter 9 — Confidence Interval Exercise (Solution)

## Problem Statement

You are a data scientist at a retail consulting firm. Dataset: **retail_store_sales_data.csv**

Columns:
- `date`
- `day_of_week`
- `sales_amount (usd)`: Daily sales amount

---

## Solution

### Import libraries and data

```python
import pandas as pd
from matplotlib import pyplot as plt
import seaborn as sns
import scipy.stats as st
import numpy as np

df = pd.read_csv("retail_store_sales_data.csv")
print(df.shape)
df.head()
```

### Histogram of sales

```python
sns.histplot(df['sales_amount (usd)'], kde=True)
```

### Population standard deviation

```python
std_dev_population = round(df['sales_amount (usd)'].std())
print("Standard Deviation:", std_dev_population)
```

### Create sample and calculate sample mean

```python
SAMPLE_SIZE = 100
sample = df.sample(SAMPLE_SIZE, random_state=100)
mean_sample = sample['sales_amount (usd)'].mean()
print("Sample mean:", mean_sample)
```

### Confidence Intervals

**Formula:**
\[
\text{Margin of Error} = z_{\alpha/2} \times \frac{\sigma}{\sqrt{n}}
\]
\[
\text{CI} = \bar{x} \pm \text{Margin of Error}
\]

```python
def confidence_interval(confidence_level, mean_sample, std_dev, n):
    # Two-tailed z-score
    alpha = 1 - confidence_level
    z = st.norm.ppf(1 - alpha/2)
    margin_of_error = z * (std_dev / np.sqrt(n))
    lower = mean_sample - margin_of_error
    upper = mean_sample + margin_of_error
    return lower, upper, z

# 60% CI
lower, upper, z = confidence_interval(0.60, mean_sample, std_dev_population, SAMPLE_SIZE)
print(f"60% CI: [{lower:.2f}, {upper:.2f}]  (z={z:.3f})")

# 82% CI
lower, upper, z = confidence_interval(0.82, mean_sample, std_dev_population, SAMPLE_SIZE)
print(f"82% CI: [{lower:.2f}, {upper:.2f}]  (z={z:.3f})")

# 98% CI
lower, upper, z = confidence_interval(0.98, mean_sample, std_dev_population, SAMPLE_SIZE)
print(f"98% CI: [{lower:.2f}, {upper:.2f}]  (z={z:.3f})")
```

---

## Related Assets in Chapter 9

- **Central Limit Theorem** demonstration using solar panel bill survey data
- Additional confidence interval examples (e.g., car miles)

**Key concepts:**
- Sample mean as estimator of population mean
- Margin of error and confidence intervals
- Z-score from standard normal distribution for different confidence levels
- Larger confidence level → wider interval

*Source: Codebasics chapter 9 exercise*
