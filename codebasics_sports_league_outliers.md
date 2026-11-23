# Codebasics Chapter 6 Exercise 1 — Sports League Outliers Detection (Solution)

## Problem Statement

You are a data scientist working for a sports analytics company. The dataset **sports_league_data.csv** includes attributes for players in the league:

- `player_id`: Unique identifier
- `age`: Age of the player
- `position`: Position (Forward, Midfielder, Defender, Goalkeeper)
- `team`: Team the player belongs to
- `games_played`: Total games played in the season
- `player_rating`: Overall performance rating for the season

---

## Solution

### Import libraries and data

```python
import pandas as pd
from matplotlib import pyplot as plt
import seaborn as sns

df = pd.read_csv("sports_league_data.csv")
print(df.shape)
df.head()
```

### Task 2: Age Analysis

```python
mean_age = int(df['age'].mean())
std_age = int(df['age'].std())
print("Mean age:", mean_age)
print("Std age:", std_age)

# Ranges within 1, 2, 3 standard deviations
print("Age within ±1σ:", round(mean_age - std_age, 2), "to", round(mean_age + std_age, 2))
print("Age within ±2σ:", round(mean_age - 2*std_age, 2), "to", round(mean_age + 2*std_age, 2))
print("Age within ±3σ:", round(mean_age - 3*std_age, 2), "to", round(mean_age + 3*std_age, 2))
```

### Task 3: Player Rating Analysis

```python
mean_rating = df['player_rating'].mean()
std_rating = df['player_rating'].std()
print("Mean rating:", round(mean_rating, 2))
print("Std rating:", round(std_rating, 2))

print("Rating within ±1σ:", round(mean_rating - std_rating, 2), "to", round(mean_rating + std_rating, 2))
print("Rating within ±2σ:", round(mean_rating - 2*std_rating, 2), "to", round(mean_rating + 2*std_rating, 2))
print("Rating within ±3σ:", round(mean_rating - 3*std_rating, 2), "to", round(mean_rating + 3*std_rating, 2))
```

### Task 4: Outlier Detection (using ±3σ rule)

```python
# Age outliers
age_outliers = df[(df['age'] < mean_age - 3*std_age) | (df['age'] > mean_age + 3*std_age)]
print("Age outliers:")
print(age_outliers)

# Player rating outliers
rating_outliers = df[(df['player_rating'] < mean_rating - 3*std_rating) | (df['player_rating'] > mean_rating + 3*std_rating)]
print("\nRating outliers:")
print(rating_outliers)
```

### Visualization (optional)

```python
sns.histplot(df['age'], kde=True)
plt.axvline(mean_age, color='k', linestyle='dashed')
plt.axvline(mean_age + 3*std_age, color='r', linestyle='dashed')
plt.axvline(mean_age - 3*std_age, color='r', linestyle='dashed')
plt.title("Age Distribution with ±3σ bounds")
plt.show()

sns.histplot(df['player_rating'], kde=True)
plt.axvline(mean_rating, color='k', linestyle='dashed')
plt.axvline(mean_rating + 3*std_rating, color='r', linestyle='dashed')
plt.axvline(mean_rating - 3*std_rating, color='r', linestyle='dashed')
plt.title("Player Rating Distribution with ±3σ bounds")
plt.show()
```

---

**Key concept:** Outlier detection using the normal distribution / Empirical Rule (±3 standard deviations from the mean).

*Source: Codebasics chapter 6 exercise 1*
