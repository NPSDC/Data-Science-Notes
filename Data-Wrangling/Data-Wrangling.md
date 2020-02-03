Operations on **dplyr** Package in R that work on data frame and return the same.</br>
Notes based on Chapter 6,7 from [Class notes of Intro to Data Science course](https://www.hcbravo.org/IntroDataSci/bookdown-notes)

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
```
**filter** - This selects entities by filtering based on the attribute properties. A set of conditions defined on the attributes which are then applied to each row
```{r}
arrest_tab %>% filter(age >= 18 & age < = 25)
```
**sample_n**, **sample_frac** - Former selects n number of random entities from the data frame, latter selects a certain fraction of samples
```{r}
arrest_tab %>% sample_n(10)
arrest_tab %>% sample_frac(0.2)
```
#### Other Operations
**arrange** - For sorting entities based on the value of an attribute
```{r}
arrest_tab %>% arrange(age) ##Ascending order
arrest_tab %>% arrange(desc(age)) ##Descending order
```

**mutate** - It creates new attributes based on the value of existing attributes
```{r}
arrest_tab %>% mutate(age_months = age*12) %>% select(arrest, age_months)
```
Note you can also define your own custom functions and pass attributes to them as the parameters along with other attributes
```{r}
mult12 <- function(x) x*12
multNum <- function(x, a) x*a ## Multiplies by a number
arrest_tab %>% mutate(age_months = mult12(age)) %>% select(arrest, age_months)
arrest_tab %>% mutate(age_months = multNum(age, 12)) %>% select(arrest, age_months)
```
**summarize** - Collapses a data frame into single row by applying some aggregating function on attribute/s over the entities
```{r}
arrest_tab %>% summarize(min_age = min(age), mean_age = mean(age), max_age = max(age))
```
Operations allowed include min, max, mean, median, sd, n, n_distinct, any, all

**group_by**  - Groups different entitities with same value across one or more attributes together, thus creating groups/categories.
```{r}
df <- arrest_tab %>% group_by(district)
class(df) ## Notice the class of the df now
```
Now if summarisation is performed, it would be applied on the group of entities rather the entire set of entities
```{r}
arrest_tab %>%
group_by(district) %>%
summarize(min_age=min(age), max_age=max(age), mean_age=mean(age))
```
**pull** - All the above operations return a tibble/data.frame as the final output. However if you want to pull a specific attribute as a vector use pull
```{r}
age_vec <- arrest_tab %>% pull(age)
class(age_vec)
```
