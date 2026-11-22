# Statistics Formulas Cheatsheet

Quick reference for commonly used formulas. All notation follows standard conventions.

## Descriptive Statistics

| Quantity | Formula |
|----------|---------|
| Mean | $\bar{x} = \frac{1}{n}\sum_{i=1}^{n} x_i$ |
| Sample Variance | $s^2 = \frac{1}{n-1}\sum_{i=1}^{n} (x_i - \bar{x})^2$ |
| Sample Std Dev | $s = \sqrt{s^2}$ |
| Z-Score | $z = \frac{x - \mu}{\sigma}$ |
| IQR | $IQR = Q_3 - Q_1$ |
| Coefficient of Variation | $CV = \frac{s}{\bar{x}}$ |

## Probability & Distributions

| Distribution | PMF / PDF | Mean | Variance |
|--------------|-----------|------|----------|
| Bernoulli($p$) | $P(X=1)=p$ | $p$ | $p(1-p)$ |
| Normal($\mu,\sigma^2$) | $\frac{1}{\sigma\sqrt{2\pi}}e^{-\frac{(x-\mu)^2}{2\sigma^2}}$ | $\mu$ | $\sigma^2$ |
| Standard Normal | $\phi(z) = \frac{1}{\sqrt{2\pi}}e^{-z^2/2}$ | 0 | 1 |

## Inferential Statistics

| Quantity | Formula |
|----------|---------|
| Standard Error of Mean | $SE = \frac{\sigma}{\sqrt{n}}$ (or $s/\sqrt{n}$) |
| Confidence Interval (mean, known $\sigma$) | $\bar{x} \pm z_{\alpha/2}\frac{\sigma}{\sqrt{n}}$ |
| Confidence Interval (mean, unknown $\sigma$) | $\bar{x} \pm t_{\alpha/2, n-1}\frac{s}{\sqrt{n}}$ |
| One-sample Z-test | $Z = \frac{\bar{x} - \mu_0}{\sigma/\sqrt{n}}$ |
| One-sample t-test | $t = \frac{\bar{x} - \mu_0}{s/\sqrt{n}}$ |
| Two-sample Z-test (means) | $Z = \frac{\bar{x}_1 - \bar{x}_2}{\sqrt{\sigma_1^2/n_1 + \sigma_2^2/n_2}}$ |
| Chi-squared Goodness of Fit | $\chi^2 = \sum \frac{(O_i - E_i)^2}{E_i}$ |
| Chi-squared Independence | Same formula on contingency table |

## Decision Rules (Hypothesis Testing)

- **Critical value**: Reject $H_0$ if test statistic falls in rejection region.
- **p-value**: Reject $H_0$ if $p < \alpha$.
- Both methods are equivalent.

## Rules of Thumb

- Normal data: ~68% within $\pm 1\sigma$, ~95% within $\pm 2\sigma$, ~99.7% within $\pm 3\sigma$.
- Outlier flag: $|z| > 3$ or outside $[Q_1 - 1.5\,IQR,\ Q_3 + 1.5\,IQR]$.
