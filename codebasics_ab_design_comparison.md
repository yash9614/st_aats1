# Codebasics Chapter 10 Exercise 3 — A/B Website Design Comparison (Solution)

## Problem Statement

An e-commerce company is evaluating two website designs:
- **Design A** (current): `current_design.csv`
- **Design B** (new): `new_design.csv`

Columns in both: `user_id`, `time_spent_minutes`

**Objective:** Determine whether Design B results in a higher average time spent on the website compared to Design A.

---

## Solution

### Hypotheses

- **H₀:** Design B does not lead to higher average time spent  
  \( \mu_B \leq \mu_A \)
- **H₁:** Design B leads to higher average time spent  
  \( \mu_B > \mu_A \)

(One-tailed / right-tailed test)

### Load data and compute statistics

```python
import pandas as pd
import numpy as np
from scipy import stats as st

df_a = pd.read_csv("current_design.csv")
df_b = pd.read_csv("new_design.csv")

mean_a = df_a.time_spent_minutes.mean()
std_a = df_a.time_spent_minutes.std()
n_a = len(df_a)

mean_b = df_b.time_spent_minutes.mean()
std_b = df_b.time_spent_minutes.std()
n_b = len(df_b)

print(f"Design A: mean={mean_a:.2f}, std={std_a:.2f}, n={n_a}")
print(f"Design B: mean={mean_b:.2f}, std={std_b:.2f}, n={n_b}")
```

### Z-score for two-sample test

```python
# Standard error of the difference
se = np.sqrt((std_a**2 / n_a) + (std_b**2 / n_b))
z_score = (mean_b - mean_a) / se
print("Z-score:", round(z_score, 3))
```

### Decision at α = 0.05 (right-tailed)

```python
alpha = 0.05
z_critical = st.norm.ppf(1 - alpha)
p_value = 1 - st.norm.cdf(z_score)

print("Critical z (α=0.05):", round(z_critical, 3))
print("p-value:", round(p_value, 4))

if z_score > z_critical:
    print("Reject H₀: Design B has significantly higher average time spent.")
else:
    print("Fail to reject H₀.")
```

---

**Key concepts:** Two-sample Z-test, A/B testing, one-tailed hypothesis, critical value comparison.

*Source: Codebasics chapter 10 exercise 3*
