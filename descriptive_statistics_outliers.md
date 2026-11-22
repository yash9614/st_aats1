# Descriptive Statistics, Normal Distribution & Outlier Detection

Notes distilled from chapter materials and Codebasics takeaways.

## Descriptive vs Inferential (Quick Distinction)

- **Descriptive**: Summarize and describe data (mean, median, spread, shape).
- **Inferential**: Draw conclusions about a population from a sample (covered in the companion note).

## Key Measures

| Measure | Definition | Strengths / Weaknesses |
|---------|------------|------------------------|
| Mean | Arithmetic average | Sensitive to outliers |
| Median | Middle value when ordered | Robust to outliers |
| Mode | Most frequent value | Useful for categorical / multimodal data |
| Range | Max − Min | Simple; highly sensitive to outliers |
| Variance / Std Dev | Average squared deviation | Standard measure of spread |
| Percentiles / Quartiles | Values at given percentages | Describe distribution shape |

**IQR** = Q3 − Q1. Common outlier rule: points outside [Q1 − 1.5×IQR, Q3 + 1.5×IQR].

## Normal Distribution Rules of Thumb

For approximately normal data:

- ~68% of data lies within ±1 standard deviation of the mean
- ~95% within ±2 standard deviations
- ~99.7% within ±3 standard deviations

## Z-Score

$$ z = \frac{x - \mu}{\sigma} $$

- Number of standard deviations from the mean.
- Standard outlier flag: $|z| > 3$.
- Equivalent to the ±3σ rule under normality.

## Practical Outlier Detection Workflow

1. Inspect summary statistics (min, max, mean, std).
2. Visualize (histogram + KDE).
3. Apply Z-score ($|z| > 3$) or IQR method.
4. Remove or cap outliers and re-check distribution.
5. Document the threshold used.

## Example Takeaways from Materials

- **Heights**: Extreme values (e.g. 3.2 ft or 9.4 ft) are data errors. After ±3σ removal the distribution becomes reasonable.
- **Telecom churn**: Mean/median/mode of monthly charges, percentiles of total charges, quartile differences between churned vs non-churned.
- **Climate stability**: Compare standard deviations of temperature across cities; lower variability preferred for planning.
- **Sports league**: Age and rating distributions with ±1/2/3σ ranges overlaid on histograms.
- **Work hours**: Mean, std, and Z-score outlier removal on daily hours.

## Supporting Tools

- Pandas GroupBy, concat, merge
- Matplotlib / seaborn histograms and scatter plots

## Relation to NLP / ML

- Outlier handling improves embedding quality and model stability.
- Understanding distributions helps interpret confidence intervals and evaluation metrics.
