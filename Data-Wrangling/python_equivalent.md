Panda operations that are equivalent to pandas. </br>

#### Loading Data

```python
import pandas as pd
arrest_tab = pd.read_csv('../data/BPD_Arrests.csv')
arrest_tab.head()
```
#### Subsetting attributes
```python
arrest_tab[['age','sex','district']].head() ##Note the use of double brackets
# selection by attribute index
arrest_tab.iloc[:,[0,2,3]].head() ##iloc for chosing index by number
```

#### Subsetting entities
```python
arrest_tab.iloc[:5,] 
arrest_tab.iloc[1:len(arrest_tab):2,].head()
arrest_tab.query('age >= 18 & age <= 25').head() ## Note query used instead of filter and defined within quotes
arrest_tab.sample(n=10)
arrest_tab.sample(frac=.1).head()
```
**Subsetting index with column names**
```python
arrest_tab.loc[0:3, ["age", "sex"]]
```
#### Pipeline
**Example**
```python
analysis_tab = (arrest_tab.query('age >= 18 & age <= 25')
    .loc[:,['sex','district','arrestDate']] ## Could have simply referenced the columns like [[]], but the chain wont work
    .rename(columns={'arrestDate': 'arrest_date'}) 
    .sample(frac=.5)) 
analysis_tab.head()
```
**Sort**
```python
arrest_tab.sort_values(['age']).head()
arrest_tab.sort_values(['age'], ascending=False).head() 
```
**Mutate**
```python
(arrest_tab.assign(age_months = 12 * arrest_tab.age)
    .loc[:10,['age','age_months']])
```
**Summarize**
```python
arrest_tab.agg({'age': ['min', 'mean', 'max'], 'arrest':["min"]})
```
**Group By**
```python
arrest_tab.groupby('district').agg({'age': ['min','mean','max']})
(arrest_tab.query('age >= 21') ##This bracket allows us to make use of next line
    .groupby(['district','sex'])
    .agg({'age': 'mean'}))
```
