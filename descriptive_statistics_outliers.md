# Descriptive Statistics & Outlier Detection

## Measures of Central Tendency

| Measure | Definition | When preferred |
|---------|------------|----------------|
| Mean | Arithmetic average (sum of values / count) | Symmetric data, no extreme outliers |
| Median | Middle value when ordered | Skewed data or outliers present |
| Mode | Most frequent value | Categorical or multimodal data |

**Interview angle (Facebook)**: In a right-skewed distribution (e.g., age in some populations), mean > median.

## Measures of Spread

- **Range**: max − min (sensitive to outliers).
- **Variance** (sample): Σ(xᵢ − x̄)² / (n − 1).
- **Standard deviation**: √variance. Measures how far data is spread from the mean; lower = closer to average, higher = more spread out.
- **IQR**: Q3 − Q1.

## Distributions

**Distribution** refers to the arrangement or spread of different values in a dataset.

### Types of Distributions

- **Discrete distribution**: Outcomes occur in specific steps or groups (e.g., counts, number of defects).
- **Continuous distribution**: Values can occur anywhere within a range (e.g., height, weight, temperature).

### Skewness

- **Right-skewed (positive skew)**: Most data on the left with a few high values extending to the right.  
  **Mean > Median**.
- **Left-skewed (negative skew)**: Most data on the right with a few low values extending to the left.  
  **Median > Mean**.
- **Zero-skewed / Symmetric**: Data evenly spread around the mean, forming a symmetrical shape.  
  In a normal distribution: **Mean = Median = Mode**.

### Normal Distribution

Features most values clustered in the middle, forming a **bell-shaped curve**.

**Key characteristics**:
- Symmetric around the mean
- Unimodal (single peak)
- Mean = Median = Mode
- Defined by mean (μ) and standard deviation (σ)
- Asymptotic tails

**Empirical Rule (68-95-99.7 Rule)**:  
In a normal distribution:
- ~68% of data falls within one standard deviation from the mean
- ~95% within two standard deviations
- ~99.7% within three standard deviations

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
