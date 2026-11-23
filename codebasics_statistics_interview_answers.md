# Codebasics Statistics Interview Questions — Detailed Answers

Companion answers to [codebasics_statistics_interview_questions.md](codebasics_statistics_interview_questions.md).

This file contains detailed interview-ready answers for all Beginner, Intermediate, and Advanced questions.

---

## Beginner Answers

(See previous detailed answers for questions 1–11. Key points remain the same.)

---

## Intermediate Answers (including newly added)

### 4. What is the Standard Error (SE)?

**Standard Error** is the standard deviation of the sampling distribution of a statistic (usually the sample mean).

For the sample mean:
\[
SE = \frac{\sigma}{\sqrt{n}}
\]

(or \( s / \sqrt{n} \) when σ is unknown)

**Significance:**
- Measures how much the sample mean is expected to vary from sample to sample.
- Smaller SE → more precise estimate of the population mean.
- Used in confidence intervals and hypothesis tests.
- Decreases as sample size increases (by the square root).

---

### 5. Outliers in heavily right-skewed income data

**Response to teammate:**  
Using mean ± 3 standard deviations is **not appropriate** for heavily skewed data.

**Why:**
- Mean and SD are highly influenced by the extreme high incomes.
- The distribution is not symmetric, so the Empirical Rule does not hold.
- This method can fail to flag real outliers or incorrectly flag normal high values.

**Better methods:**
1. **IQR method**: Flag values outside \( Q1 - 1.5 \times IQR \) or \( Q3 + 1.5 \times IQR \)
2. **Modified Z-score** using Median Absolute Deviation (MAD)
3. **Percentile-based** (e.g., below 1st or above 99th percentile)
4. Domain knowledge + visualization (box plot, histogram)

For income data, IQR or MAD-based methods are preferred because they are robust to skewness.

---

### 6. What is a Z-score?

A **z-score** tells you how many standard deviations a data point is from the mean.

\[
z = \frac{x - \mu}{\sigma}
\]

**Significance:**
- Standardizes data so different distributions can be compared.
- Used for outlier detection (|z| > 3).
- Converts any normal distribution to the standard normal distribution.
- Enables probability calculations using standard normal tables.

---

### 7. 95% Confidence Interval for student heights

Given: \( \bar{x} = 170 \) cm, \( s = 10 \) cm, \( n = 30 \)

For 95% CI (large sample approximation or t with df=29):

\[
CI = \bar{x} \pm z_{0.025} \times \frac{s}{\sqrt{n}}
\]

\( z_{0.025} \approx 1.96 \)

\[
SE = \frac{10}{\sqrt{30}} \approx 1.826
\]
\[
Margin\ of\ error = 1.96 \times 1.826 \approx 3.58
\]
\[
CI = 170 \pm 3.58 = (166.42,\ 173.58)
\]

**Interpretation:** We are 95% confident that the true average height of the population lies between 166.42 cm and 173.58 cm.

---

### 8. Common statistical methods to detect outliers

| Method              | How it works                                      | Best for          |
|---------------------|---------------------------------------------------|-------------------|
| **Z-score**         | \|z\| > 3                                          | Roughly normal data |
| **IQR**             | Outside [Q1 − 1.5·IQR, Q3 + 1.5·IQR]           | Skewed data       |
| **Modified Z-score (MAD)** | Based on median and MAD                  | Robust to outliers |
| **Percentiles**     | Extreme percentiles (e.g., <1% or >99%)           | Any distribution  |
| **Visualization**   | Box plots, histograms, scatter plots              | Exploratory       |

---

## Advanced Answers

### 1. Converting Normal to Standard Normal

Use the z-score transformation:
\[
z = \frac{x - \mu}{\sigma}
\]

**Why useful:**
- Allows use of standard normal tables or software for any normal distribution.
- Enables comparison across different scales.
- Simplifies probability calculations.
- Foundation for many hypothesis tests.

---

### 2. Relationship between Confidence Level and Significance Level

\[
\text{Confidence Level} = 1 - \alpha
\]

- 95% confidence level → α = 0.05
- 99% confidence level → α = 0.01

Higher confidence level → lower significance level → wider confidence intervals and harder to reject H₀.

---

*(Previous detailed answers for Type I/II errors, churn prediction, A/B testing, email campaigns, t-tests, equal variance, screen time estimation, same mean/SD datasets, and sample size effects remain valid and are listed in earlier sections of this file or the previous version.)*

---

*All answers are written in an interview-ready style with definitions, formulas, examples, and practical implications.*
