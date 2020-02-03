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

#### Pipeline
**Sort**
```python
arrest_tab.sort_values(['age']).head()
arrest_tab.sort_values(['age'], ascending=False).head() 
```
