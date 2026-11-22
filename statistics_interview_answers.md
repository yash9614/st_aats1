# Statistics Interview Answers (Concise)

Short, accurate answers corresponding to the questions in [statistics_interview_questions.md](statistics_interview_questions.md). Use for review; expand with the concept notes when needed.

## Beginner

1. **Mall survey bias**  
   Sample / selection bias. Mall visitors are not representative of the general population (e.g., age, income, interests differ).

2. **Law of Large Numbers**  
   As sample size grows, the sample mean converges to the true population mean. Larger samples give more reliable estimates.

3. **Parameter vs Statistic**  
   Parameter = numerical summary of the entire population. Statistic = numerical summary calculated from a sample (used to estimate the parameter).

4. **Normal vs Standard Normal**  
   Standard normal is a special case with mean 0 and standard deviation 1. Converting via z-scores allows use of standard tables and comparison across different scales.

5. **Standard Normal percentages**  
   Approximately 68% within ±1σ, 95% within ±2σ, 99.7% within ±3σ.

6. **Hypothesis**  
   A statement about a population parameter.  
   H₀ = no effect / no difference (status quo).  
   H₁ = effect or difference exists.  
   Example: H₀ — new drug has no effect on recovery time; H₁ — new drug reduces recovery time.

7. **One-tailed vs Two-tailed**  
   One-tailed tests a specific direction (e.g., mean > 10).  
   Two-tailed tests any difference (mean ≠ 10).

8. **Alpha (α)**  
   Significance level — the probability of rejecting H₀ when it is true (Type I error rate). Commonly 0.05.

9. **Median vs Mean**  
   Median is preferred when data are skewed or contain outliers, because it is robust to extreme values.

10. **Bell-curve characteristics**  
    Symmetric, unimodal, mean = median = mode, follows the 68/95/99.7 rule.

11. **Degrees of Freedom**  
    Number of independent pieces of information available to estimate a parameter. For sample variance or a one-sample t-test it is usually n − 1.

## Intermediate

1. **20 vs 2,000 survey**  
   Law of Large Numbers (and CLT). Larger sample means are closer to the true population mean.

2. **Central Limit Theorem**  
   The sampling distribution of the sample mean approaches a normal distribution as sample size increases, regardless of the population shape (provided variance is finite). Enables normal-based inference for large samples.

3. **Population vs Sampling Distribution of the Mean**  
   Mean remains μ. Variance becomes σ²/n. Standard deviation becomes σ/√n (the standard error).

4. **Blood-pressure medication errors**  
   Type I: conclude the drug works when it does not (approve ineffective drug).  
   Type II: conclude the drug does not work when it does (reject effective drug).  
   Lowering α reduces Type I risk but increases Type II risk (β). In healthcare, balance depends on the cost of each error; sometimes a lower α is preferred, sometimes power is prioritized.

5. **Imbalanced churn (8%)**  
   Accuracy is misleading. Use precision, recall, F1, ROC-AUC; apply class weights, resampling (SMOTE), or threshold tuning; consider cost-sensitive evaluation.

6. **Checkout A/B test**  
   Randomly assign users to single-step vs multi-step design. Primary metric = purchase completion rate. Ensure adequate sample size, check for sample ratio mismatch, and evaluate both statistical and practical significance.

7. **Three email campaigns**  
   Chi-squared test of independence on the campaign × purchase contingency table. Watch for multiple comparisons (if doing pairwise follow-ups) and unbalanced group sizes.

8. **Why not t-test for proportions**  
   Proportions are bounded [0,1] and follow a binomial distribution; the normal approximation or chi-squared / z-test for proportions is appropriate.

9. **Types of t-tests**  
   - One-sample: compare sample mean to a known value.  
   - Independent two-sample: compare means of two groups (equal or unequal variance / Welch).  
   - Paired: compare two related measurements on the same subjects.

10. **Equal variance check**  
    Levene’s test, F-test, or visual comparison of standard deviations / box plots.

11. **National teen screen-time estimate**  
    Define the population, choose a sampling design (simple random or stratified), determine required sample size, collect data, and construct a confidence interval for the mean.

12. **Same mean and SD, different distributions**  
    Examine skewness, kurtosis, median, IQR, and visualize with histograms or box plots.

13. **Sample size and reliability of SD/variance**  
    Larger samples reduce the sampling variability of the estimates. Sample variance uses n−1 to remain unbiased.

---

For fuller explanations see the concept notes and [codebasics_key_takeaways.md](codebasics_key_takeaways.md).
