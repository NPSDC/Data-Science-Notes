Operations on **dplyr** Package in R that work on data frame and return the same

#### Subsetting Attributes/Features
**select** - Selects the specific attributes from a data.frame
Example
```{r}
arrest_tab %>% select(arrestDate) OR select(arrest_tab, arrestDate) ## First argument is the name of the data frame
arrest_tab %>% select(1:5)
arrest_tab %>% select(c(1,2,5))
select(arrest_tab, starts_with("a"))
```

#### Subsetting Entities/Samples
**slice** - The above operation selects the entity based on the position row position
```{r}
arrest_tab %>% slice(1:5) 
arrest_tab %>% slice(-c(1,3,5)) ##Everything row excluding the first, third and fifth
```{r}
