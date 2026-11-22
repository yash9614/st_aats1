# Statistics Materials Index

## Core Notes (this repository)

| File | Description |
|------|-------------|
| [formulas_cheatsheet.md](formulas_cheatsheet.md) | Formulas for descriptive stats, distributions, CIs, and tests |
| [descriptive_statistics_outliers.md](descriptive_statistics_outliers.md) | Center, spread, normal distribution, outlier detection (Z-score, IQR, MAD) |
| [inferential_statistics.md](inferential_statistics.md) | CLT, CIs, hypothesis testing, p-values, multicollinearity, A/B testing, bias |
| [ab_testing.md](ab_testing.md) | Dedicated A/B testing guide (design, production model versions, network effects, CUPED, SRM) |
| [concepts_notes.md](concepts_notes.md) | Short notes on deterministic bucketing, Bayes rare events, dice-game EV, RDD, exact binomial test, Poisson rates, recommendation systems, MapReduce |
| [practical_python_examples.md](practical_python_examples.md) | Runnable numpy patterns including SRM check |
| [codebasics_key_takeaways.md](codebasics_key_takeaways.md) | Official Codebasics key takeaways |
| [statistics_interview_questions.md](statistics_interview_questions.md) | High-priority conceptual questions (CLT, p-value, multicollinearity, A/B, outliers) |
| [statistics_interview_answers.md](statistics_interview_answers.md) | Concise answers to the conceptual questions |
| [practical_interview_questions.md](practical_interview_questions.md) | Coding-style questions |
| [practical_interview_solutions.md](practical_interview_solutions.md) | Working Python solutions with notes and edge-case handling |

## Topics Covered (aligned with common StrataScratch / FAANG questions)

### Descriptive
- Mean, median, mode (when to prefer each)
- Variance, standard deviation, IQR
- Normal distribution & empirical rule
- Outlier detection: Z-score, IQR, modified z-score (MAD)
- Numerically stable online mean & variance (Welford)

### Inferential & Probability
- Central Limit Theorem
- Confidence intervals & margin of error (sample-size scaling)
- Hypothesis testing workflow
- p-values (definition and effect of sample size)
- Type I / Type II errors and power
- One-sample and two-sample Z-tests, t-tests
- Exact binomial test (minimum-likelihood definition)
- Comparing two Poisson rates (log rate ratio)
- Chi-squared tests
- Multicollinearity detection (correlation matrix, VIF)
- A/B testing (design, analysis, network effects, CUPED, SRM, deterministic bucketing)
- Relative lift confidence intervals (delta method)
- Bayes’ rule for rare-event detectors
- Expected value of sequential decision problems (dice game)
- Regression discontinuity designs
- Sampling bias types

### Modeling / Systems
- Ordinary least squares with standard errors
- Weighted least squares
- Ridge regression (unpenalized intercept)
- Variance Inflation Factor
- Recommendation system design (candidate generation, ranking, evaluation)
- MapReduce join + top-N performers

## External Sources

- StrataScratch statistics & probability articles and questions
- Codebasics Math & Stats takeaway PDFs
- Practical coding-style statistics interview questions

## Related Repository

Practical NLP notes and solved notebooks: [yash9614/grnd_a](https://github.com/yash9614/grnd_a)

---

**Last updated**: November 2026
