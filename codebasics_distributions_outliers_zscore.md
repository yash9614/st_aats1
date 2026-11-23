# Codebasics Chapter 6 — Distributions, Outliers & Z-Score Solutions

Practical solutions from Codebasics materials covering normal distribution, outlier detection using normal distribution, z-score, and standard normal distribution.

---

## Normal Distribution Analysis (Heights)

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.read_csv("heights.csv")
mean = round(df.height.mean(), 2)
std = round(df.height.std(), 2)
print(mean, std)

sns.histplot(df.height, kde=True)
plt.axvline(mean, color='k', linestyle='dashed', linewidth=1)
plt.axvline(mean + std, color='r', linestyle='dashed', linewidth=1)
plt.axvline(mean - std, color='r', linestyle='dashed', linewidth=1)
plt.axvline(mean + 2*std, color='g', linestyle='dashed', linewidth=1)
plt.axvline(mean - 2*std, color='g', linestyle='dashed', linewidth=1)
plt.axvline(mean + 3*std, color='b', linestyle='dashed', linewidth=1)
plt.axvline(mean - 3*std, color='b', linestyle='dashed', linewidth=1)
```

**Empirical Rule verification:**
- ~65.9% of data within ±1 standard deviation
- ~97% within ±2 standard deviations
- ~99.9% within ±3 standard deviations

---

## Outlier Detection Using Normal Distribution

```python
df = pd.read_csv("heights_with_outliers.csv")
df.describe()

mean = df.height.mean()
std = df.height.std()
print(mean, std)

# Identify potential outliers (beyond ±3σ)
outliers = df[(df.height < mean - 3*std) | (df.height > mean + 3*std)]
print(outliers)
```

**Observation:** Minimum height 3.2 ft and maximum 9.4 ft are clear outliers (data errors).

---

## Z-Score

**Z-score** measures how many standard deviations a data point is from the mean.

```python
# Manual z-score
df['z_score'] = (df.height - df.height.mean()) / df.height.std()

# Using scipy
from scipy.stats import zscore
df['z_score_scipy'] = zscore(df.height)

# Flag outliers where |z| > 3
outliers = df[df['z_score'].abs() > 3]
```

**Uses:**
- Comparing values across different datasets
- Outlier detection (|z| > 3)

---

## Standard Normal Distribution (SND)

The standard normal distribution has:
- Mean = 0
- Standard deviation = 1

```python
# Convert to standard normal (z-scores)
df['z'] = (df.height - df.height.mean()) / df.height.std()

# Now the distribution of z has mean ≈ 0 and std ≈ 1
print(df['z'].mean(), df['z'].std())
```

**Uses of SND / Z-scores:**
- Comparing datasets on the same scale
- Calculating probabilities
- Z-tests for comparing means

---

**Key takeaways:**
- Normal distribution → Empirical Rule (68-95-99.7)
- Outliers often fall beyond ±3σ
- Z-score = (x − μ) / σ
- Standard normal = z-scores of a normal distribution

*Source: Codebasics chapter 6 assets*
