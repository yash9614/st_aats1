# Descriptive Statistics, Normal Distribution & Outlier Detection

## Descriptive vs Inferential

- **Descriptive statistics** summarize and describe data (center, spread, shape).
- **Inferential statistics** draw conclusions about a population from a sample (see companion note).

## Key Measures

| Measure | Definition | When to Prefer |
|---------|------------|----------------|
| Mean | Arithmetic average | Symmetric data, no extreme outliers |
| Median | Middle value when ordered | Skewed data or presence of outliers |
| Mode | Most frequent value | Categorical data or multimodal distributions |
| Range | Max − Min | Quick sense of total spread |
| Variance / Std Dev | Average squared deviation | Standard measure of variability |
| Percentiles / Quartiles | Position in ordered data | Describing distribution shape |

**IQR** = Q3 − Q1. Robust outlier rule: flag points outside [Q1 − 1.5×IQR, Q3 + 1.5×IQR].

## Normal Distribution

For approximately normal data:

- ~68% of observations lie within ±1 standard deviation of the mean
- ~95% within ±2 standard deviations
- ~99.7% within ±3 standard deviations

These percentages provide quick sanity checks (e.g., on height or rating data).

## Z-Score

$$ z = \frac{x - \mu}{\sigma} $$

- Measures how many standard deviations a point is from the mean.
- Common outlier threshold: $|z| > 3$ (equivalent to the ±3σ rule under normality).

## Practical Outlier Detection Workflow

1. Compute summary statistics (min, max, mean, std, quartiles).
2. Visualize with histogram + KDE.
3. Apply Z-score ($|z| > 3$) or IQR method.
4. Remove or cap flagged points and re-check the distribution.
5. Document the rule and threshold used.

## Worked Examples from Materials

- **Heights**: Values such as 3.2 ft or 9.4 ft are clear data errors. Removing points beyond ±3σ yields a sensible distribution.
- **Telecom churn**: Compare mean, median, and mode of monthly charges; examine percentiles of total charges and quartile gaps between churned and non-churned customers.
- **Climate stability**: Lower standard deviation of temperature is preferred for agricultural planning.
- **Sports league**: Report ±1/2/3σ ranges for age and player rating and overlay them on histograms.
- **Work hours**: Calculate mean and standard deviation, then remove outliers via Z-score before further analysis.

## Supporting Operations

Pandas GroupBy, concat, and merge, plus matplotlib/seaborn histograms and scatter plots, are the usual tools for these analyses.

## Relation to Downstream Work

Clean descriptive analysis and outlier handling improve the quality of features that later feed models or embedding pipelines.
