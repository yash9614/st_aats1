# Codebasics Chapter 3 — Pandas Exercise Solutions

Clean reference of exercise solutions from Codebasics Pandas materials (chapter 3 assets).

These support data cleaning and analysis workflows commonly used before statistical analysis.

---

## Dataframe Basics

### DataFrame Basics (Exercise: Solution)

Peter Pandey arrived in Bangalore with the aim of finding a suitable house. Dataset columns: area_type, availability, location, size, society, total_sqft, bath, balcony, price.

```python
import pandas as pd
df = pd.read_csv('bengaluru_house_prices.csv')
print(df.shape)
df.head()
```

### Unique categories

```python
df['area_type'].unique()
df['size'].unique()
```

### Filter 2 BHK Super built-up Area

```python
filtered = df[(df['size'] == '2 BHK') & (df['area_type'] == 'Super built-up  Area')]
print(len(filtered))
```

### Add price_category column

```python
df['price_category'] = df.apply(lambda x: "Affordable" if x['price'] < 80 else "High Cost", axis=1)
df.head()
```

### Rows above mean price

```python
df[df['price'] > df['price'].mean()]
```

---

## Read / Write CSV & Excel

```python
import pandas as pd
df = pd.read_csv("movies_data.csv")
df.head()
```

### Add year_classify column

```python
df['year_classify'] = df.apply(lambda x: 'Before 2000' if x['release_year'] < 2000 else 'From 2000', axis=1)
```

### Save selected columns

```python
df.to_csv('final_movie_data.csv', columns=['movie_id', 'title', 'budget', 'revenue', 'year_classify'], index=False)
```

---

## Handling Missing Data (fillna)

```python
import pandas as pd
df = pd.read_csv('fruits_data.csv')
print(df.shape)
print(df.columns)
df
```

### Fill all nulls with -1

```python
new_df = df.fillna('-1')
```

### Column-specific filling

```python
new_df = df.fillna({
    'apple(1kg)': df['apple(1kg)'].mean(),
    'banana(1 dozen)': df['banana(1 dozen)'].mean(),
    'grapes(1kg)': df['grapes(1kg)'].median(),
    'mango(1kg)': df['mango(1kg)'].median(),
    'Water Melons(1)': 'Not Available'
})
```

---

## Handling Missing Data (replace)

Typical patterns covered in the solution notebooks:
- Replace specific values or ranges
- Use dictionary-based replacement
- Handle special missing markers (e.g. -999, 'N/A')

---

## Group By

```python
import pandas as pd
df = pd.read_csv('movies_data.csv')
g = df.groupby('industry')

# Iterate groups
for key, group_df in g:
    print("Group by Key:", key)
    print(group_df)
```

Common operations in solutions:
- `groupby().mean()`, `groupby().size()`, `groupby().agg()`
- Filtering groups and transforming

---

## Concat & Merge

```python
import pandas as pd

df_movies = pd.read_csv('movies.csv')
df_financials = pd.read_csv('financials.csv')
df_languages = pd.read_csv('languages.csv')
df_new_movies = pd.read_csv('new_movies.csv')

# Concat
df_movies = pd.concat([df_movies, df_new_movies], ignore_index=True)

# Inner join with languages
df_movies = pd.merge(df_movies, df_languages, on='language_id', how='inner')

# Left join with financials
df_movies = pd.merge(df_movies, df_financials, on='movie_id', how='left')

# Save selected columns
df_movies.to_csv('final_complete_data.csv',
                 columns=['movie_id', 'title', 'lang_name', 'budget', 'revenue', 'currency'],
                 index=False)
```

---

*Source: Codebasics chapter 3 assets (exercise solution notebooks).*
*These patterns are foundational for cleaning data before statistical analysis.*
