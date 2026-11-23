# Codebasics Statistics Interview Questions — Detailed Answers

Companion answers to [codebasics_statistics_interview_questions.md](codebasics_statistics_interview_questions.md).

Collected and organized from Codebasics math & stats materials.

---

## Beginner

### 1. Shopping mall survey bias

**Type of bias:** **Selection bias** (specifically **convenience sampling bias** or **coverage bias**).

**Why it occurs:**
- You are only surveying people who happen to be in a shopping mall.
- This sample is **not representative** of the broader population.
- People who visit shopping malls tend to differ systematically from those who don’t (age, income, location, lifestyle, free time, etc.).
- Online shoppers, people who work odd hours, rural populations, or those who avoid malls are under-represented or completely missing.

**Impact:**  
Opinions about the new product will be skewed toward the preferences of mall-going customers. The results cannot be reliably generalized to the entire target market.

**Better approaches:**  
Random sampling, stratified sampling, or combining multiple channels (online + offline + different locations).

---

### 2. Law of Large Numbers (LLN)

**Statement:**  
As the sample size \( n \) increases, the sample average (or sample proportion) converges to the true population average (or true probability).

In mathematical terms:  
\[
\lim_{n \to \infty} \bar{X}_n = \mu
\]  
(with probability 1, under certain conditions).

**Why it is important:**
- It is the foundation of why larger samples give more reliable estimates.
- It justifies using sample statistics to estimate population parameters.
- It underpins confidence intervals, hypothesis testing, and A/B testing.
- It explains why a survey of 2,000 people is more trustworthy than a survey of 20 people (even if both are randomly sampled).

**Intuition:**  
Short-term fluctuations average out as more observations are collected.

---

### 3. Parameter vs Statistic

| Aspect              | Parameter                          | Statistic                          |
|---------------------|------------------------------------|------------------------------------|
| **What it is**      | Fixed numerical characteristic of the **population** | Numerical characteristic calculated from a **sample** |
| **Example**         | Population mean \( \mu \), population proportion \( p \), population variance \( \sigma^2 \) | Sample mean \( \bar{x} \), sample proportion \( \hat{p} \), sample variance \( s^2 \) |
| **Known or unknown?** | Usually unknown (we want to estimate it) | Always known once we have the sample |
| **Notation**        | Greek letters (usually)            | Latin letters / hats               |

**Key point:**  
We use **statistics** (from samples) to estimate **parameters** (of the population). The goal of most statistical inference is to make statements about parameters based on statistics.

---

### 4. Normal Distribution vs Standard Normal Distribution

**Normal Distribution**  
A bell-shaped, symmetric continuous distribution defined by two parameters:
- Mean \( \mu \)
- Standard deviation \( \sigma \)

Any normal distribution can be written as \( X \sim \mathcal{N}(\mu, \sigma^2) \).

**Standard Normal Distribution**  
A special case of the normal distribution where:
- Mean \( \mu = 0 \)
- Standard deviation \( \sigma = 1 \)

It is denoted as \( Z \sim \mathcal{N}(0, 1) \).

**Why we convert data to standard normal (z-score / standardization):**

\[
z = \frac{x - \mu}{\sigma}
\]

**Reasons:**
1. **Comparability** — Scores from different distributions (different means and SDs) can be compared on the same scale.
2. **Probability calculations** — Standard normal tables (or software) give probabilities for any normal distribution after conversion.
3. **Outlier detection** — A value with \( |z| > 3 \) is often considered an extreme outlier.
4. **Many statistical methods** assume or work more cleanly with standardized data.
5. **Interpretation** — A z-score directly tells you how many standard deviations a point is from the mean.

---

### 5. Standard Normal Distribution and the Empirical Rule

The **Standard Normal Distribution** is the normal distribution with \( \mu = 0 \) and \( \sigma = 1 \).

**Empirical Rule (68-95-99.7 Rule)** for any normal distribution (including the standard normal):

| Range from mean | Percentage of data |
|-----------------|--------------------|
| \( \pm 1\sigma \) | ≈ **68%** |
| \( \pm 2\sigma \) | ≈ **95%** |
| \( \pm 3\sigma \) | ≈ **99.7%** |

**For the standard normal specifically:**
- Between \( -1 \) and \( +1 \) → ~68% of the data
- Between \( -2 \) and \( +2 \) → ~95% of the data
- Between \( -3 \) and \( +3 \) → ~99.7% of the data

This rule is extremely useful for quickly assessing how unusual a data point is without calculating exact probabilities.

---

### 6. What is a hypothesis? Null vs Alternative Hypothesis

**Hypothesis**  
A hypothesis is a clear, testable statement or claim about a population parameter (e.g., mean, proportion, difference between groups).

**Null Hypothesis (\( H_0 \))**  
The default assumption that there is **no effect**, no difference, or no relationship. It is the statement we try to disprove with data.

**Alternative Hypothesis (\( H_1 \) or \( H_a \))**  
The claim we want to support. It states that there **is** an effect, a difference, or a relationship.

**Real-life example:**  
A company claims that a new training program increases average employee productivity.

- \( H_0 \): The training has no effect → \( \mu_{\text{after}} = \mu_{\text{before}} \) (or difference = 0)
- \( H_1 \): The training increases productivity → \( \mu_{\text{after}} > \mu_{\text{before}} \)

We collect data, run a statistical test, and decide whether the evidence is strong enough to reject \( H_0 \) in favor of \( H_1 \).

---

### 7. One-Tailed vs Two-Tailed Test

| Type          | Direction of interest                  | Critical region          | When to use |
|---------------|----------------------------------------|--------------------------|-------------|
| **One-tailed** | Only one direction (greater than or less than) | Only one tail of the distribution | You care about a change in a specific direction |
| **Two-tailed** | Either direction (different from)      | Both tails               | You care about any difference, regardless of direction |

**Examples:**

- **One-tailed:**  
  Testing whether a new drug **reduces** blood pressure more than the old drug.  
  \( H_1 \): \( \mu_{\text{new}} < \mu_{\text{old}} \)  
  You only reject if the new drug is significantly lower.

- **Two-tailed:**  
  Testing whether a new website design changes the conversion rate (could go up or down).  
  \( H_1 \): conversion rate is **not equal** to the old rate.  
  You reject if the rate is significantly higher **or** significantly lower.

**Note:** One-tailed tests have more power for the direction you care about, but you must decide the direction **before** looking at the data.

---

### 8. What is Alpha (α) in Hypothesis Testing?

**Alpha (\( \alpha \))** is the **significance level** — the probability of making a **Type I error**.

- Type I error = rejecting the null hypothesis when it is actually true (false positive).
- \( \alpha \) is the maximum risk you are willing to take of wrongly rejecting \( H_0 \).

**Common values:**  
\( \alpha = 0.05 \) (5%) or \( \alpha = 0.01 \) (1%).

**Interpretation:**  
If you set \( \alpha = 0.05 \), you are saying:  
“I am willing to accept a 5% chance of concluding there is an effect when there really isn’t one.”

**Decision rule:**  
- If p-value \( \leq \alpha \) → reject \( H_0 \) (statistically significant)
- If p-value \( > \alpha \) → fail to reject \( H_0 \)

Lower \( \alpha \) makes it harder to reject \( H_0 \) (more conservative).

---

### 9. When is the median more suitable than the mean?

The **median** is preferred over the mean when the data is:

1. **Skewed** (long tail on one side)
2. **Contains outliers** or extreme values
3. **Ordinal** (ranked categories)

**Why:**  
The mean is pulled toward extreme values, while the median is robust and stays in the middle of the ordered data.

**Classic examples:**
- **Income / house prices** — a few very high values make the mean much higher than what a “typical” person earns/pays. Median is a better measure of central tendency.
- **Response time of a website** — a few very slow requests inflate the mean; median better represents typical user experience.
- **Exam scores** with a couple of extremely low scores due to absences.

**Rule of thumb:**  
If the mean and median are very different, the distribution is skewed and the median is usually the more representative measure.

---

### 10. Characteristics of a Bell-Curve (Normal) Distribution

A bell-curve (normal) distribution has these key characteristics:

1. **Symmetric** around the mean — left and right sides are mirror images.
2. **Unimodal** — single peak at the center.
3. **Mean = Median = Mode** — all three measures of central tendency are equal.
4. **Asymptotic tails** — the curve approaches the x-axis but never touches it.
5. **Defined by two parameters** — mean (\( \mu \)) and standard deviation (\( \sigma \)).
6. **Empirical Rule applies:**
   - ~68% of data within \( \pm 1\sigma \)
   - ~95% within \( \pm 2\sigma \)
   - ~99.7% within \( \pm 3\sigma \)
7. **Total area under the curve = 1** (it is a probability density function).

**Why it matters:**  
Many real-world phenomena (heights, measurement errors, test scores, etc.) approximately follow a normal distribution, which allows us to use powerful statistical methods and the standard normal table.

---

### 11. What are Degrees of Freedom in Statistics?

**Degrees of Freedom (df)** is the number of independent values or pieces of information that are free to vary when estimating a parameter.

**Intuition:**  
Once you know the mean of a sample, not all data points are independent. If you fix the mean, the last value is determined by the others.

**Examples:**
- Sample variance:  
  \[
  s^2 = \frac{\sum (x_i - \bar{x})^2}{n-1}
  \]  
  We divide by \( n-1 \) (not \( n \)) because one degree of freedom is used to estimate the mean. Using \( n \) would bias the variance estimate downward.

- t-test:  
  For a one-sample t-test, \( df = n - 1 \).  
  For a two-sample t-test (equal variance), \( df = n_1 + n_2 - 2 \).

- Chi-square test:  
  For a contingency table, \( df = (rows - 1) \times (columns - 1) \).

**Why it matters:**  
Many critical values (t-distribution, chi-square, F-distribution) depend on degrees of freedom. As \( df \) increases, these distributions approach the normal distribution.

---

## Intermediate

### 1. Screen time survey (20 vs 2,000 people)

**Concept:** **Law of Large Numbers (LLN)**

The larger sample (n = 2,000) produces a sample mean that is closer to the true population mean because, as sample size increases, the sample average converges to the population average.

The smaller sample (n = 20) has higher sampling variability, so its mean (5.4) can easily be farther from the true value. The larger sample’s mean (5.0) is more reliable.

This is exactly what the Law of Large Numbers guarantees.

---

### 2. Central Limit Theorem (CLT)

**Statement of the CLT:**  
If you take repeated random samples of size \( n \) from any population with mean \( \mu \) and finite variance \( \sigma^2 \), then the distribution of the sample means \( \bar{X} \) approaches a normal distribution as \( n \) becomes large:

\[
\bar{X} \sim \mathcal{N}\left( \mu, \frac{\sigma^2}{n} \right)
\]

(approximately, for large \( n \))

**Why the CLT is important:**
1. It allows us to use normal-based methods (confidence intervals, t-tests, z-tests) even when the original data is **not** normally distributed.
2. It is the foundation of most statistical inference.
3. It explains why the standard error decreases as \( \sqrt{n} \) increases.
4. It justifies the use of the normal approximation in A/B testing, quality control, and survey analysis.

**Rule of thumb:** \( n \geq 30 \) is often considered “large enough” for the CLT to kick in (though highly skewed distributions may need larger \( n \)).

---

### 3. Population vs Sampling Distribution of the Sample Mean

| Quantity              | Population Distribution | Sampling Distribution of \( \bar{X} \) |
|-----------------------|-------------------------|----------------------------------------|
| **Mean**              | \( \mu \)               | \( \mu \) (same)                       |
| **Variance**          | \( \sigma^2 \)          | \( \frac{\sigma^2}{n} \) (smaller)     |
| **Standard Deviation**| \( \sigma \)            | \( \frac{\sigma}{\sqrt{n}} \) (standard error) |

**Key points:**
- The mean stays the same (unbiased estimator).
- The variance and standard deviation shrink as sample size \( n \) increases.
- For large \( n \), the sampling distribution becomes approximately normal (by the CLT), regardless of the shape of the original population.

This is why larger samples give more precise estimates of the population mean.

---

### 4. Type I & Type II Errors in Blood Pressure Medication Trial

**Setup:**  
Testing a new blood pressure medication.

- \( H_0 \): The new drug has no effect (or is not better than the existing treatment).
- \( H_1 \): The new drug lowers blood pressure.

**Type I Error (α):**  
Concluding the drug works when it actually doesn’t.  
→ Approving an ineffective (or harmful) drug.  
This is controlled by the significance level \( \alpha \) you choose (commonly 0.05 or 0.01).

**Type II Error (β):**  
Concluding the drug doesn’t work when it actually does.  
→ Missing a genuinely effective treatment.  
Power = \( 1 - \beta \) (probability of correctly detecting a real effect).

**Trade-offs with α:**
- Lower \( \alpha \) (e.g., 0.01 instead of 0.05) → reduces Type I error but **increases** Type II error (harder to reject \( H_0 \), lower power).
- Higher \( \alpha \) → easier to claim the drug works, but higher risk of false positive.

**In a high-stakes healthcare setting:**  
You usually want a **low Type I error** (strict α, e.g., 0.01 or even lower) because approving a useless or harmful drug can harm patients and waste resources.  
To keep Type II error low as well, you increase sample size (which increases power without raising α).  
You may also pre-specify clinically meaningful effect sizes and use interim analyses or adaptive designs carefully.

**Balance strategy:**  
- Set a conservative α (protect against false positives).  
- Power the study adequately (large enough sample) so you don’t miss a real benefit.  
- Consider the cost of each error type (patient harm vs missed opportunity).

---

### 5. Highly Imbalanced Churn Prediction (only 8% churn)

**Statistical challenges:**
1. **Class imbalance** — The model can achieve high accuracy simply by predicting “no churn” for everyone.
2. **Bias toward the majority class** — Most algorithms optimize overall error and under-perform on the rare class.
3. **Misleading evaluation metrics** — Accuracy, precision, and even AUC can look good while the model fails to catch actual churners.
4. **Unstable estimates** — With few positive cases, parameter estimates and feature importance can be noisy.
5. **Different costs of errors** — Missing a churner (false negative) is usually more costly than incorrectly flagging a non-churner (false positive).

**How to address them:**

| Area              | Approach |
|-------------------|----------|
| **Evaluation**    | Use **Precision, Recall, F1-score, PR-AUC** (not just accuracy or ROC-AUC). Focus on Recall of the churn class. Report confusion matrix. |
| **Error types**   | Explicitly discuss business cost of Type I (false positive) vs Type II (false negative). Optimize for the more expensive error. |
| **Data-level**    | Oversample minority (SMOTE, ADASYN) or undersample majority. Use class weights. |
| **Algorithm-level** | Use models that handle imbalance well (e.g., gradient boosting with scale_pos_weight, balanced random forest). Consider threshold tuning. |
| **Validation**    | Stratified k-fold cross-validation to preserve class ratio. |
| **Other**         | Collect more churn examples if possible. Use anomaly-detection style approaches if imbalance is extreme. |

**Interview tip:** Emphasize that accuracy is almost useless here and that you would align the metric and threshold with the business cost of missing a churner.

---

### 6. A/B Test for Checkout Page Designs

**Goal:** Determine which design (single-step vs multi-step with trust badges + progress bar) has a higher purchase completion rate.

**Experiment design:**

1. **Randomized Controlled Experiment (A/B test)**
   - Randomly assign users to Control (current single-step) or Treatment (multi-step design).
   - Ensure assignment is persistent (same user always sees the same version — use cookie/user ID hashing).

2. **Primary metric**
   - Purchase completion rate (binary: completed purchase / reached checkout).

3. **Sample size**
   - Calculate required sample size based on baseline conversion rate, minimum detectable effect (MDE), desired power (usually 80%), and α (usually 0.05).

4. **Duration**
   - Run long enough to cover weekly seasonality and reach the calculated sample size. Avoid stopping early just because results look good.

5. **Analysis factors to consider**
   - Statistical significance (two-proportion z-test or chi-square).
   - Practical significance (is the lift big enough to justify the design change?).
   - Guardrail metrics (page load time, bounce rate, support tickets, revenue per user).
   - Segmentation (new vs returning users, device type, traffic source).
   - Check for Sample Ratio Mismatch (SRM).
   - Novelty effect or learning effect if the multi-step design is unfamiliar.

6. **Decision rule**
   - Declare a winner only if statistically significant **and** the effect size meets the business threshold.

---

### 7. Three Email Campaigns and Purchase Behavior

**Question:** Does the type of email campaign (A, B, or C) significantly affect purchase rate (Yes/No)?

**Approach:**

1. **Data structure**  
   Categorical independent variable (campaign: A/B/C) and binary dependent variable (purchased: Yes/No).  
   This forms a 3×2 contingency table.

2. **Statistical test**  
   **Chi-square test of independence**.  
   It tests whether the proportion of purchases differs across the three campaigns.

3. **Assumptions**
   - Observations are independent.
   - Expected cell counts ≥ 5 (if not, use Fisher’s exact test or combine categories).
   - Random sampling.

4. **Handling challenges**
   - **Multiple comparisons:** If the overall chi-square is significant, do pairwise comparisons (A vs B, A vs C, B vs C) and apply a correction (Bonferroni or Tukey-style) to control family-wise error rate.
   - **Unbalanced groups:** Chi-square handles unequal sample sizes, but very small groups reduce power. Report effect sizes (Cramér’s V or differences in proportions with confidence intervals).
   - **Practical significance:** Even if statistically significant, check whether the lift is large enough to matter for the business.

5. **Alternative / complementary**  
   Logistic regression with campaign as a categorical predictor (and optionally other covariates) to get odds ratios and control for confounders.

---

### 8. Why is the t-test not used for a two-sample test of proportions?

The **t-test** is designed for **continuous** outcomes (means).  
Proportions are **binary / binomial** outcomes (success/failure counts).

**Reasons the t-test is inappropriate:**
1. The sampling distribution of a proportion is binomial (or approximately normal only under certain conditions), not t-distributed.
2. Variance of a proportion is \( p(1-p)/n \), which depends on the proportion itself. The t-test assumes a different variance structure.
3. Using a t-test on binary data violates the underlying assumptions and can give incorrect p-values and confidence intervals.

**Correct test:**  
**Two-proportion z-test** (or chi-square test of independence for a 2×2 table).  
These use the proper standard error for proportions.

---

### 9. Different Types of t-tests and When to Use Each

| Type of t-test              | When to use | Hypotheses example | Degrees of freedom |
|-----------------------------|-------------|--------------------|--------------------|
| **One-sample t-test**       | Compare a sample mean to a known/hypothesized population mean | \( H_0: \mu = \mu_0 \) | \( n - 1 \) |
| **Two-sample t-test (independent)** | Compare means of two independent groups | \( H_0: \mu_1 = \mu_2 \) | \( n_1 + n_2 - 2 \) (equal variance) or Welch’s approximation |
| **Paired t-test**           | Compare means of two related measurements (before-after, matched pairs) | \( H_0: \mu_d = 0 \) | \( n - 1 \) (number of pairs) |
| **Welch’s t-test**          | Two independent groups when variances are unequal (more robust) | Same as two-sample | Adjusted (not integer) |

**Quick decision guide:**
- One group vs a fixed value → one-sample t-test
- Two separate groups → independent two-sample t-test (prefer Welch’s unless you have strong reason to assume equal variances)
- Same subjects measured twice → paired t-test

**Assumptions common to t-tests:**  
Approximately normal data (or large n by CLT), independent observations, and (for classical two-sample) equal variances.

---

### 10. How can you determine if two samples have equal variance?

You can check for equal variance (homoscedasticity) in several ways:

**1. Formal statistical tests**
- **F-test** — Compares the ratio of the two sample variances. Sensitive to non-normality.
- **Levene’s test** — More robust; uses absolute deviations from the median (or mean). Preferred in practice.
- **Bartlett’s test** — Also checks equality of variances but assumes normality.

**2. Visual methods**
- Side-by-side box plots
- Residual plots (if in a regression context)
- Histogram or density plots of both groups

**3. Rule of thumb**
- If the larger standard deviation is less than twice the smaller one, many analysts treat the variances as roughly equal (especially with large samples).

**Practical recommendation:**  
Use **Levene’s test**. If it is significant (p ≤ 0.05), assume unequal variances and use **Welch’s t-test** instead of the classical two-sample t-test. Welch’s test does not require the equal-variance assumption and is generally safer.

---

### 11. Estimating average daily screen time of teenagers across the country

**Goal:** Estimate the population mean screen time of all teenagers in the country.

**Recommended statistical approach:**

1. **Define the population clearly**  
   All teenagers (e.g., ages 13–19) in the country.

2. **Sampling design**
   - Prefer **probability sampling** (simple random, stratified, or multi-stage cluster sampling).
   - Stratify by age group, region, urban/rural, or socioeconomic status to improve representativeness and precision.
   - Avoid convenience samples (e.g., only malls or only online surveys).

3. **Sample size calculation**
   - Use the formula for estimating a mean:
     \[
     n = \left( \frac{z_{\alpha/2} \cdot \sigma}{E} \right)^2
     \]
   - Decide acceptable margin of error \( E \), confidence level, and an estimate of \( \sigma \) (from a pilot study or prior research).

4. **Data collection**
   - Use validated instruments (diary, app tracking, or carefully worded survey questions).
   - Account for non-response and potential reporting bias.

5. **Estimation**
   - Calculate the sample mean \( \bar{x} \) and standard error.
   - Construct a confidence interval for the true mean \( \mu \).
   - If the sampling design is complex (stratified/cluster), use the appropriate design-based variance estimator or survey weights.

6. **Reporting**
   - Point estimate + confidence interval + description of sampling method and any limitations.

**Key principle:** Random (or probability) sampling + adequate sample size → reliable estimate via the Law of Large Numbers and Central Limit Theorem.

---

### 12. Two datasets with the same mean and standard deviation — what else to look at?

Mean and standard deviation only capture center and spread. They do **not** describe the shape of the distribution. Two datasets can have identical mean and SD yet look completely different.

**Additional descriptive measures to examine:**

| Measure              | What it tells you                          | Why it helps |
|----------------------|--------------------------------------------|--------------|
| **Median**           | Middle value                               | Detects skewness (if mean ≠ median) |
| **Skewness**         | Asymmetry of the distribution              | Positive = right tail, negative = left tail |
| **Kurtosis**         | Heaviness of the tails / peakedness        | High kurtosis = more outliers |
| **Minimum & Maximum**| Range and extreme values                   | Shows outliers and full span |
| **IQR (Q3 – Q1)**    | Spread of the middle 50%                   | Robust measure of variability |
| **Percentiles**      | e.g., 5th, 25th, 75th, 95th                | Better picture of the distribution |
| **Histogram / Box plot / Density plot** | Visual shape                    | Instantly reveals multimodality, skew, outliers |

**Example:**  
One dataset could be perfectly normal; the other could be bimodal or heavily skewed — yet both can share the same mean and standard deviation.

**Interview takeaway:** Always look at the full distribution (visuals + shape statistics), not just mean and SD.

---

### 13. How does sample size affect the reliability of descriptive statistics like standard deviation and variance?

**Larger sample size → more reliable estimates.**

**Specific effects:**

1. **Standard deviation and variance**
   - With small \( n \), the sample SD/variance can fluctuate a lot and is often biased (especially variance, which is why we use \( n-1 \)).
   - As \( n \) increases, the sample variance converges to the true population variance (Law of Large Numbers).
   - The sampling variability of the sample variance decreases.

2. **Stability**
   - Small samples are highly sensitive to individual outliers. One extreme value can dramatically inflate the SD.
   - Large samples dilute the effect of any single observation.

3. **Confidence in the estimate**
   - You can construct confidence intervals for the variance itself (using the chi-square distribution). These intervals become narrower as \( n \) grows.
   - With very small \( n \) (e.g., < 10–15), descriptive statistics like SD should be interpreted with caution.

4. **Practical implication**
   - A standard deviation calculated from 10 observations is much less trustworthy than one calculated from 1,000 observations, even if the numerical values look similar.
   - This is why pilot studies with tiny samples give only rough ideas of variability.

**Summary:**  
Sample size directly improves the precision and stability of estimates of spread (SD and variance), just as it does for the mean.

---

*All answers are interview-ready with definitions, intuition, examples, and practical implications.*
