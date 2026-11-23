# Codebasics Chapter 4 — Climate Stability Analysis (Solution)

Exercise solution for climate stability analysis using pandas and statistical concepts (standard deviation).

---

## Comparing Weather Temperature Variability for Agricultural Investment Decisions

**Context:** An agricultural investment firm is deciding on a location for a new farming project. Consistent and predictable weather conditions are vital for successful agriculture. The firm wants to evaluate and compare two potential cities based on their temperature stability.

The key factor is the **variability in average daily temperatures**, as it directly impacts crop growth and agricultural planning.

**Dataset:** `climate_stability_comparison.xlsx`

Columns:
- `month`
- `Avg Temp City A (°C)`
- `Avg Temp City B (°C)`

### Task Objective

- Calculate the standard deviation for average temperatures in both cities.
- Determine which city has higher temperature variability.
- Decide on the city with more stable (lower variability) temperatures for agricultural investment.

---

## Solution

### 1. Import libraries and data

```python
import pandas as pd

df = pd.read_excel("climate_stability_comparison.xlsx")
print(df.shape)
df.head(12)
```

### 2. Calculate standard deviations

```python
# City A standard deviation
cityA_std_dev = round(df['Avg Temp City A (°C)'].std(), 2)
print("Standard Deviation of Avg Temp in City A:", cityA_std_dev)

# City B standard deviation
cityB_std_dev = round(df['Avg Temp City B (°C)'].std(), 2)
print("Standard Deviation of Avg Temp in City B:", cityB_std_dev)
```

### 3. Comparison and decision

```python
if cityA_std_dev < cityB_std_dev:
    print("Invest in City A due to more stable temperature conditions.")
else:
    print("Invest in City B due to more stable temperature conditions.")
```

### 4. Observation and Decision

- City A demonstrated a notably lower standard deviation in its average daily temperatures compared to City B. This indicates that City A experiences less fluctuation in temperature throughout the year.
- The temperature range in City A was found to be more consistent and narrow, fluctuating moderately between 14°C and 19°C.
- Conversely, City B displayed higher variability with temperatures ranging more broadly from 12°C to 25°C.
- **Recommendation:** Choose City A for the agricultural investment due to more stable temperature conditions.

---

**Key concept applied:** Standard deviation as a measure of variability / stability. Lower standard deviation = more stable conditions.
