# Descriptive Statistics & Outlier Detection

## Measures of Central Tendency

| Measure | Definition | When preferred |
|---------|------------|----------------|
| Mean | Arithmetic average | Symmetric data, no extreme outliers |
| Median | Middle value | Skewed data or outliers present |
| Mode | Most frequent value | Categorical or multimodal data |

**Interview angle (Facebook)**: In a right-skewed distribution (e.g., age in some populations), mean > median.

## Measures of Spread

- **Range**: max − min (sensitive to outliers).
- **Variance** (sample): Σ(xᵢ − x̄)² / (n − 1).
- **Standard deviation**: √variance.
- **IQR**: Q3 − Q1.

## Normal Distribution & Empirical Rule

Approximately:
- 68% of data within 1 σ of the mean
- 95% within 2 σ
- 99.7% within 3 σ

## Outlier Detection

### Z-score method
Flag points where |z| > 3 (assumes roughly normal data).

### IQR method
Flag points outside [Q1 − 1.5·IQR, Q3 + 1.5·IQR].

### Modified z-score (Median Absolute Deviation)
More robust to outliers in the data itself:

$$ M = 0.6745 \cdot \frac{x - \text{median}}{\text{MAD}} $$

Flag |M| > 3.5 (common threshold).

**StrataScratch / interview reference**: Microsoft — “How do you detect if a new observation is an outlier?”

Implementation of MAD outliers: [practical_interview_solutions.md](practical_interview_solutions.md).

## Numerically Stable Online Statistics

For streaming data or very large values that are close together, use Welford’s method for mean and sample variance (single pass, no storage of all values).

See [practical_interview_solutions.md](practical_interview_solutions.md).
