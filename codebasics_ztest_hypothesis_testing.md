# Codebasics Chapter 10 — Z-Test Hypothesis Testing Exercise (Solution)

## Problem Statement

You are a data scientist evaluating cost-saving measures. Dataset: **operational_costs_data.csv**

Columns:
- `department_id`
- `cost_reduction_pct`: Percentage reduction in operational costs

**Given population parameters:**
- Population mean (target before measures): 7%
- Population standard deviation: 3%

**Goal:** Determine whether the cost-saving measures reduced operational costs beyond the company's target of 8%.

---

## Solution

### Import libraries and data

```python
import pandas as pd
import numpy as np
from scipy import stats

df = pd.read_csv("operational_costs_data.csv")
print(df.shape)
df.head()
```

### Define Hypotheses

- **Null Hypothesis (H₀):** The reduction in average monthly operational costs is less than or equal to 8%.  
  \( H_0: \mu \leq 8 \)
- **Alternative Hypothesis (Hₐ):** The reduction in average monthly operational costs is greater than 8%.  
  \( H_a: \mu > 8 \)

(This is a **one-tailed** test.)

### Calculate Test Statistics

```python
sample_mean = df.cost_reduction_pct.mean()
sample_size = df.shape[0]
population_mean = 7
population_std_dev = 3

standard_error = population_std_dev / np.sqrt(sample_size)
z_score = (sample_mean - population_mean) / standard_error

print("Sample mean:", round(sample_mean, 2))
print("Sample size:", sample_size)
print("Standard error:", round(standard_error, 4))
print("Z-score:", round(z_score, 2))
```

### Decision (using critical value or p-value)

```python
# Critical z-value for one-tailed test at α = 0.05
alpha = 0.05
z_critical = stats.norm.ppf(1 - alpha)
print("Critical z-value (α=0.05):", round(z_critical, 2))

# p-value
p_value = 1 - stats.norm.cdf(z_score)
print("p-value:", round(p_value, 4))

if z_score > z_critical:
    print("Reject H₀: Cost reduction is significantly greater than 8%.")
else:
    print("Fail to reject H₀.")
```

---

## Related Chapter 10 Assets

- One-tailed Z-test (housing inflation example)
- Two-tailed Z-test
- A/B testing Z-test (drug effectiveness / control vs test group)
- p-value calculations

**Key concepts:**
- One-tailed vs two-tailed tests
- Z-test statistic: \( z = \frac{\bar{x} - \mu_0}{\sigma / \sqrt{n}} \)
- Critical value and rejection region
- p-value interpretation

*Source: Codebasics chapter 10 exercise*
