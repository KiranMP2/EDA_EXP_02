# Exp - 2 Netflix Shows & Movies

## Aim

To analyze Netflix dataset and compare movies vs TV shows, top producing countries, and release year trends.

## Procedure / Algorithm

1)Load dataset (netflix_titles.csv).

2)Count movies vs TV shows.

3)Group by country → top contributors.

4)Create pivot table (release year vs type).

5)Visualize with bar & line charts.

## Program

### Load dataset directly from GitHub

```python 
import pandas as pd
import numpy as np

url="https://raw.githubusercontent.com/allenkong221/netflix-titles-dataset/main/netflix_titles.csv"
df=pd.read_csv(url)
print("KIRAN MP")
print("212224230123")

print("Shape:",df.shape)

print("Columns:",df.columns,"\n")

print("Types:",df['type'].value_counts(),"\n")
```

### Clean 'date_added' and extract year/month

```python
df['date_added']=df['date_added'].astype(str).str.strip()
df['date_added']=pd.to_datetime(df['date_added'],errors='coerce')
df['year_added']=df['date_added'].dt.year.astype('Int64')
df['month_added']=df['date_added'].dt.month_name()
print("KIRAN MP")
print("212224230123")

df.head()
```
###  Movies vs TV Shows
```python
count_by_type = df.groupby('type')['title'].count()
print("KIRAN MP")
print("212224230123")
print("Count by Type:\n", count_by_type, "\n")
```
###  Country vs Type Pivot Table
```python
pivot_country_type = df.pivot_table(
index='country',
columns='type',
values='title',
aggfunc='count',
fill_value=0
)
pivot_country_type['Total'] = pivot_country_type.sum(axis=1)
max_country = pivot_country_type['Total'].idxmax() 
max_count = pivot_country_type['Total'].max()
print("KIRAN MP")
print("212224230123")
print("Pivot Table (Country vs Type):\n", pivot_country_type.head(), "\n")
print(f"Largest Overall: {max_country} with {max_count} titles\n")
```
### Top 5 Directors
```python
top_directors = df['director'].value_counts().head(5)
print("KIRAN MP")
print("212224230123")
print("Top 5 Directors:\n", top_directors, "\n")
```

### Yearly Trend of Additions (Movies vs TV Shows)
```python
trend=df.groupby(['year_added','type']).size().unstack(fill_value=0)
print("KIRAN MP")
print("212224230123")
print("Yearly Trend by Type\n")
print(trend.head())
```

### Expand Genres
``` python
df_genre = (df[['show_id','listed_in']]
.dropna()
.assign(listed_in=df['listed_in'].str.split(', '))
.explode('listed_in'))
df_expanded = df.merge(df_genre, on='show_id', how='left')
print("KIRAN MP")
print("212224230123")
print("Columns after merge:\n", df_expanded.columns)
print("\nExpanded Genre Sample:\n",
df_expanded[['title','listed_in_y']].head())

top_genres = df_expanded['listed_in_y'].value_counts().head(5)
print("\nTop 5 Genres:\n", top_genres, "\n")
```
## Ouptut

### Load dataset directly from GitHub
<img width="958" height="889" alt="image" src="https://github.com/user-attachments/assets/a122c3f1-91cc-4c34-88f6-cc6ead343192" />


### Clean 'date_added' and extract year/month
<img width="950" height="588" alt="image" src="https://github.com/user-attachments/assets/6f9eea4c-76ae-48c7-b876-e54f998e7404" />


###  Movies vs TV Shows
<img width="946" height="191" alt="image" src="https://github.com/user-attachments/assets/94b9ea46-711f-4e2c-ba15-acb8dc44f007" />


###  Country vs Type Pivot Table

<img width="948" height="396" alt="image" src="https://github.com/user-attachments/assets/434a804e-4c7e-4e00-b3d0-5ca552a58013" />


### Top 5 Directors

<img width="914" height="220" alt="image" src="https://github.com/user-attachments/assets/8f4d5cf5-754f-4714-a545-2a9ca0fe7918" />


### Yearly Trend of Additions (Movies vs TV Shows)
<img width="938" height="270" alt="image" src="https://github.com/user-attachments/assets/e2e18d89-026f-4eac-aa52-d16d60b110a6" />


### Expand Genres
<img width="947" height="544" alt="image" src="https://github.com/user-attachments/assets/39276e68-20c5-44cb-85f4-8b2a1624b77d" />



## Result 
Helps Netflix in content planning & investments.
