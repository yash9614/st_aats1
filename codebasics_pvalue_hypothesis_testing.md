# Codebasics Chapter 10 Exercise 2 — P-Value Hypothesis Testing (Solution)

## Problem Statement

A company implemented a new marketing campaign and wants to assess if it significantly increased the product's average monthly sales by more than 15%.

Dataset: **monthly_sales_data.csv**
- `product_id`
- `sales_increase_pct`

**Given population parameters:**
- Population mean (before campaign): 12%
- Population standard deviation: 5%

**Goal:** Determine whether the campaign increased average monthly sales by more than 15%.

---

## Solution

### Import and load data

```python
import pandas as pd
import numpy as np
from scipy import stats

df = pd.read_csv("monthly_sales_data.csv")
print(df.shape)
df.head()
```

### Hypotheses

- **H₀:** The increase in average monthly sales ≤ 15%  
  \( H_0: \mu \leq 15 \)
- **H₁:** The increase in average monthly sales > 15%  
  \( H_1: \mu > 15 \)

(One-tailed test)

### Calculate test statistic

```python
sample_mean = df.sales_increase_pct.mean()
sample_size = len(df)
population_mean = 12
population_std_dev = 5

standard_error = population_std_dev / np.sqrt(sample_size)
z_score = (sample_mean - population_mean) / standard_error

print("Sample mean:", round(sample_mean, 2))
print("Z-score:", round(z_score, 2))
```

### p-value and decision

```python
alpha = 0.05
p_value = 1 - stats.norm.cdf(z_score)   # one-tailed
print("p-value:", round(p_value, 4))

if p_value < alpha:
    print("Reject H₀: Campaign significantly increased sales beyond 15%.")
else:
    print("Fail to reject H₀.")
```

---

**Key concepts:** p-value, one-tailed Z-test, significance level (α).

*Source: Codebasics chapter 10 exercise 2*
