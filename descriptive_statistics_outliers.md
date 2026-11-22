# Descriptive Statistics, Normal Distribution & Outlier Detection

Notes distilled from chapter materials covering measures of central tendency/dispersion, normal distribution properties, Z-scores, and practical outlier detection.

## Key Measures

| Measure | Definition | Use |
|---------|------------|-----|
| Mean | Arithmetic average | Central tendency (sensitive to outliers) |
| Median | Middle value | Robust central tendency |
| Mode | Most frequent value | Categorical / multimodal data |
| Range | Max − Min | Simple spread |
| Variance / Std Dev | Average squared deviation | Spread of data |
| Percentiles / Quartiles | Values at given percentages | Distribution shape, IQR |

**Interquartile Range (IQR)** = Q3 − Q1. Common outlier rule: points outside [Q1 − 1.5×IQR, Q3 + 1.5×IQR].

## Normal Distribution Rules of Thumb

For approximately normal data:

- ~68% of data lies within ±1 standard deviation of the mean
- ~95% within ±2 standard deviations
- ~99.7% within ±3 standard deviations

These percentages are useful for quick sanity checks on real datasets (e.g., height data).

## Z-Score

$$ z = \frac{x - \mu}{\sigma} $$

- Tells how many standard deviations a point is from the mean.
- Standard practice for outlier detection: flag or remove points with $|z| > 3$.
- Equivalent to the ±3σ rule under normality.

## Practical Outlier Detection Workflow

1. Inspect summary statistics (min, max, mean, std).
2. Visualize (histogram + KDE).
3. Apply Z-score or IQR method.
4. Remove or cap outliers and re-check distribution.
5. Document the threshold used (commonly ±3 Z-score).

## Example Takeaways from Materials

- **Heights analysis**: Extreme values (e.g., 3.2 ft or 9.4 ft) are clear data errors. After ±3σ removal, the distribution becomes reasonable.
- **Telecom churn**: Compute mean/median/mode of monthly charges, percentiles of total charges, and quartile differences between churned vs non-churned customers.
- **Climate stability**: Compare standard deviations of temperature across cities; lower variability is preferred for agricultural planning.
- **Sports league**: Analyze age and player rating distributions, report ±1/2/3σ ranges, and overlay intervals on histograms.

## Pandas / Visualization Support

The materials also cover:
- GroupBy (split-apply-combine)
- Concat and merge operations
- Basic matplotlib / seaborn histograms and scatter plots

These are foundational for any data analysis pipeline that feeds into NLP or ML models.

## Relation to NLP / ML

- Outlier handling improves embedding quality and model stability.
- Understanding distributions helps interpret confidence intervals and evaluation metrics.
- Descriptive stats are the first step before any classification or regression task.
