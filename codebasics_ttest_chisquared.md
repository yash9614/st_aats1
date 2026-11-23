# Codebasics Chapters 11-12 — T-Test & Chi-Squared Solutions

Practical solutions covering hypothesis testing with one-sample t-test and chi-squared tests.

---

## 1. One-Sample T-Test (Exam Scores)

**Scenario:** A school introduced a new teaching method that claims to improve average exam scores. Historical average = 72. Pilot test on 20 students.

**Hypotheses:**
- **H₀:** New teaching method does not increase the average exam score (\( \mu \leq 72 \))
- **H₁:** New teaching method increases the average exam score (\( \mu > 72 \))

```python
import pandas as pd
from scipy import stats

df = pd.read_csv("exam_scores.csv")
population_mean = 72

# One-sample t-test (right-tailed)
t_stat, p_value = stats.ttest_1samp(df.score, population_mean, alternative="greater")
print("t-statistic:", round(t_stat, 3))
print("p-value:", round(p_value, 4))
```

**Decision:**
- If t-statistic > critical value **or** p-value < α (0.05) → reject H₀
- Conclusion: New teaching method improves grades

---

## 2. Chi-Squared Test of Goodness of Fit

**Purpose:** Check if observed frequencies match expected frequencies.

```python
import numpy as np
import scipy.stats as stats

expected = np.array([40, 60, 30, 70])
actual = np.array([45, 55, 35, 65])

chi_square_stat, p_value = stats.chisquare(actual, expected)
print("Chi-square statistic:", round(chi_square_stat, 3))
print("p-value:", round(p_value, 4))
```

**Decision:** If p-value ≥ 0.05 → fail to reject H₀ (observed matches expected).

---

## 3. Chi-Squared Test of Independence

**Scenario:** Mobile phone store — does phone preference (iPhone vs Samsung) depend on age group?

**Hypotheses:**
- **H₀:** No association between phone preference and age group
- **H₁:** There is an association between phone preference and age group

```python
import numpy as np
from scipy.stats import chi2_contingency

# Contingency table
# Rows: age groups (<30, ≥30)
# Columns: iPhone, Samsung
observed = np.array([
    [50, 30],   # Under 30
    [20, 50]    # 30 & Over
])

chi2, p_value, dof, expected = chi2_contingency(observed)
print("Chi-square statistic:", round(chi2, 3))
print("p-value:", round(p_value, 4))
print("Degrees of freedom:", dof)
```

**Decision:** If p-value < 0.05 → reject H₀ (variables are dependent).

---

## Related Chapter 11 Content

Chapter 11 includes a bank campaign analysis case study (`phase_2_atliqo_bank.ipynb`) involving transaction data before/after a campaign, useful for applying hypothesis testing in a business context.

**Key concepts covered:**
- One-sample t-test (small samples or unknown σ)
- Chi-squared goodness of fit
- Chi-squared test of independence
- p-value and critical value decision rules

*Source: Codebasics chapters 11–12 assets*
