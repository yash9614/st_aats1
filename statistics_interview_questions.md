# Statistics Interview Questions

Organized from Codebasics math & stats materials. Use with the concept notes and takeaways for preparation.

## Beginner

1. Imagine you're conducting a survey to understand people's opinion about a new product, but you only collect responses from people in a shopping mall. What type of bias might this introduce and why?
   - *Hint: Sample / selection bias — mall-goers are not representative of the full population.*

2. What does the Law of Large Numbers state in statistics, and why is it important?
   - *Hint: Sample average converges to population mean as n grows; underpins why larger samples are more reliable.*

3. What is the difference between a parameter and a statistic?
   - *Hint: Parameter = population quantity; statistic = sample quantity used to estimate it.*

4. What is the difference between a normal distribution and a standard normal distribution? Why do we convert data to a standard normal distribution?
   - *Hint: Standard normal has μ=0, σ=1; conversion (z-score) allows use of standard tables and comparison across variables.*

5. What is the Standard Normal Distribution, and how is data typically distributed within ±1, ±2, and ±3 standard deviations from the mean?
   - *Hint: ~68%, ~95%, ~99.7%.*

6. What is a hypothesis in statistics? Explain the difference between a null hypothesis and an alternative hypothesis with a real-life example.
   - *Hint: H₀ = no effect; H₁ = effect exists. Example: drug vs placebo.*

7. What is a One-Tailed and Two-Tailed Test in Statistics? Give examples for each.
   - *Hint: One-tailed tests direction (e.g., improvement); two-tailed tests any difference.*

8. What is Alpha (α) in Hypothesis Testing?
   - *Hint: Significance level — probability of Type I error (false positive).*

9. In what situation would the median be a more suitable measure compared to the mean?
   - *Hint: Skewed data or presence of outliers.*

10. What are the characteristics of a bell-curve distribution?
    - *Hint: Symmetric, unimodal, mean = median = mode, 68/95/99.7 rule.*

11. What are Degrees of Freedom in Statistics?
    - *Hint: Number of independent pieces of information; often n-1 for sample variance or t-tests.*

## Intermediate

1. You survey 20 people about their daily screen time and get an average of 5.4 hours. Your colleague surveys 2,000 people from the same population and gets 5.0 hours. Which concept explains why the larger survey's average is likely closer to the true population average?
   - *Hint: Law of Large Numbers / Central Limit Theorem.*

2. What is the Central Limit Theorem (CLT)? Why is the CLT important in statistics?
   - *Hint: Sampling distribution of the mean approaches normality; enables inference even for non-normal populations.*

3. What happens to the mean, variance, and standard deviation when comparing a population distribution with the sampling distribution of the sample mean?
   - *Hint: Mean stays the same; variance becomes σ²/n; standard deviation becomes σ/√n (standard error).*

4. You are testing a new blood pressure medication. Describe how Type I and Type II errors would apply in this context, and discuss the trade-offs involved in setting the significance level (α). How would changing α affect the probability of Type II error (β), and how would you balance the risk in a high-stakes environment like healthcare?
   - *Hint: Type I = false positive (approve ineffective drug); Type II = false negative (reject effective drug). Lower α reduces Type I but increases Type II.*

5. You are analyzing customer churn data for a subscription service. The dataset is highly imbalanced, with only 8% of customers churning. You're tasked with building a model to predict churn. What statistical challenges do you anticipate, and how would you address them?
   - *Hint: Accuracy is misleading; use precision/recall/F1, class weights, resampling, or threshold tuning.*

6. An e-commerce company wants to evaluate two different designs for its checkout page. One version uses a single-step process, while the other features a multi-step design with trust badges and a progress bar. The business wants to know which design leads to a higher purchase completion rate. How would you design an experiment to help make a data-driven decision, and what factors would you consider during analysis?
   - *Hint: A/B test with random assignment, sufficient sample size, primary metric = completion rate, check for sample ratio mismatch, consider practical significance.*

7. A marketing team runs three different promotional email campaigns (Campaign A, B, and C) to boost customer purchases. After the campaign, they record whether each recipient made a purchase (Yes/No). How would you determine if the type of email campaign has a significant impact on purchase behaviour?
   - *Hint: Chi-squared test of independence; watch for multiple comparisons and unbalanced groups.*

8. Why is the t-test not used for a two-sample test of proportions?
   - *Hint: Proportions follow a binomial/normal approximation; use z-test for proportions or chi-squared.*

9. What are the different types of t-tests, and when should each be used?
   - *Hint: One-sample, independent two-sample (equal or unequal variance), paired.*

10. How can you determine if two samples have equal variance?
    - *Hint: Levene's test, F-test, or visual comparison of standard deviations.*

11. You are tasked with estimating the average daily screen time of teenagers across the country. How would you approach this problem using statistical methods?
    - *Hint: Define population, choose sampling design (stratified if needed), compute sample size, construct confidence interval.*

12. You are given two datasets with the same mean and standard deviation. What additional descriptive measures would you use to understand the data distribution better, and why?
    - *Hint: Skewness, kurtosis, median, IQR, histograms, or box plots.*

13. How does sample size affect the reliability of descriptive statistics like standard deviation and variance?
    - *Hint: Larger n reduces sampling variability of the estimates; sample variance uses n-1 to remain unbiased.*

---

Cross-reference detailed explanations with:
- [codebasics_key_takeaways.md](codebasics_key_takeaways.md)
- [descriptive_statistics_outliers.md](descriptive_statistics_outliers.md)
- [inferential_statistics.md](inferential_statistics.md)
