# Codebasics Chapter 6 Exercise 2 — Employees Work Hours Analysis (Solution)

## Problem Statement

You are a data scientist at a management consulting firm specializing in workplace efficiency and employee productivity. Dataset: **employees_work_hours_data.csv**

Columns:
- `employee_id`: Unique identifier
- `department`: Department (Sales, IT, HR, etc.)
- `remote_working`: Yes/No
- `hours_worked_per_day`: Average hours worked per day

---

## Solution

### Import libraries and data

```python
import pandas as pd
from matplotlib import pyplot as plt
import seaborn as sns

df = pd.read_csv("employees_work_hours_data.csv")
print(df.shape)
df.head()
```

### Task 2: Statistical Measures of Work Hours

```python
mean = round(df.hours_worked_per_day.mean(), 1)
std = round(df.hours_worked_per_day.std(), 1)

print("Mean:", mean)
print("Std:", std)
```

### Task 3: Calculating Z-Scores for Outlier Detection

```python
df['z_score'] = (df.hours_worked_per_day - mean) / std
df.head()
```

### Task 4: Removing Outliers Based on Z-Scores

```python
# Identify outliers (|z| > 3)
outliers = df[(df.z_score < -3) | (df.z_score > 3)]
print("Number of outliers:", outliers.shape[0])
outliers

# Remove outliers
df_no_outliers = df[(df.z_score > -3) & (df.z_score < 3)]
print("Shape after removal:", df_no_outliers.shape)
df_no_outliers.head()
```

**Note:** It is standard practice in industry to use ±3 Z-score (i.e., ±3 standard deviations) as the criterion for outlier removal.

### Task 5: Standard Normal Distribution Post-Outlier Removal

After removing outliers, the z-scores of the remaining data approximate a standard normal distribution (mean ≈ 0, std ≈ 1).

```python
# Recalculate z-scores on cleaned data if needed
clean_mean = df_no_outliers.hours_worked_per_day.mean()
clean_std = df_no_outliers.hours_worked_per_day.std()
df_no_outliers['z_clean'] = (df_no_outliers.hours_worked_per_day - clean_mean) / clean_std

print(df_no_outliers['z_clean'].mean(), df_no_outliers['z_clean'].std())

sns.histplot(df_no_outliers['z_clean'], kde=True)
plt.title("Standard Normal Distribution after Outlier Removal")
plt.show()
```

---

**Key concepts applied:**
- Mean and standard deviation
- Z-score calculation: \( z = \frac{x - \mu}{\sigma} \)
- Outlier detection and removal using |z| > 3
- Standard normal distribution after cleaning

*Source: Codebasics chapter 6 exercise 2*
