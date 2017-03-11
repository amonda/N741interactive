# N741: Homework 5
Melinda K. Higgins, PhD.  
February 27, 2017  

# Homework 5 - DUE March 15, 2017

For this homework, we'll work with the "Wong" dataset built in to the `car` package. The "Wong" data frame has 331 row and 7 columns. The observations are longitudinal data on recovery of IQ after comas of varying duration for 200 subjects. The data are from Wong, Monette, and Weiner (2001) and are for 200 patients who sustained traumatic brain injuries resulting in comas of varying duration. After awakening from their comas, patients were periodically administered a standard IQ test, but the average number of measurements per patient is small (331/200 = 1.7). *To get more info type `??Wong`.*

The 7 variables in the dataset are:

* `id`
    + patient ID number.
* `days`
    + number of days post coma at which IQs were measured.
* `duration`
    + duration of the coma in days.
* `sex`
    + a factor with levels Female and Male.
* `age`
    + in years at the time of injury.
* `piq`
    + performance (i.e., mathematical) IQ.
* `viq`
    + verbal IQ.

## Load dataset in from `car` package


```r
library(car)
data(Wong)

library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following object is masked from 'package:car':
## 
##     recode
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
# add an age group variable
Wong$agegrp <- case_when(
  (Wong$age > 0 & Wong$age <= 10) ~ 1,
  (Wong$age > 10 & Wong$age <= 20) ~ 2,
  (Wong$age > 20 & Wong$age <= 30) ~ 3,
  (Wong$age > 30 & Wong$age <= 40) ~ 4,
  (Wong$age > 40 & Wong$age <= 50) ~ 5,
  (Wong$age > 50 & Wong$age <= 60) ~ 6,
  (Wong$age > 60 & Wong$age <= 70) ~ 7,
  (Wong$age > 70 & Wong$age <= 100) ~ 8)

# convert to factor, add code levels and labels
Wong$agegrp <- factor(Wong$agegrp,
                  levels = c(1,2,3,4,5,6,7,8),
                  labels = c("Ages 1-10",
                             "Ages 11-10",
                             "Ages 21-10",
                             "Ages 31-10",
                             "Ages 41-10",
                             "Ages 51-10",
                             "Ages 61-70",
                             "Ages 71-100"))
```

Using this dataset, and today's demos complete the following tasks:

1. Make a table of non-parametric statistics (median and IQR) for the number of days and duration grouped by `sex`. You'll be using `summarise()` from the `dplyr` package. For a given variable `x` you'll use `median(x, na.rm=TRUE)`, `quantile(x, 0.25, na.rm=TRUE)`, and `quantile(x, 0.75, na.rm=TRUE)`. Give the table a title using the `caption=` option and update the column names with something nice using the `col.names=` option in the `knitr::kable()` command. 




2.  Make a table of parametric statistics (mean and SD) for the performance outcomes `piq` and `viq` grouped by `sex`. Like the table above, you'll be using `summarise()` from the `dplyr` package. Now you'll use `mean(x, na.rm=TRUE)` and `sd(x, na.rm=TRUE)`. Give the table a title using the `caption=` option and update the column names with something nice using the `col.names=` option in the `knitr::kable()` command. 

3. Make a table containing the frequencies and relative percentages for `agegrp`. Use the example we did in class to help guide you.

4. Make a regression model (Model 1) for the performance IQ (`piq`) using `age` and `sex`. Put the regression model results into a table.

5. Make a second regression model (Model 2) for performance IQ (`piq`) using `age` and `sex` plus `days` and `duration`. Put the regression model results into a table.

6. Finally, make a table showing the results from the `anova()` command comparing Model 1 and Model 2 you made above using the example we did in class as a guide. 

7. STUDENT CHOICE - pick either a `htmlwidget` from [http://gallery.htmlwidgets.org/](http://gallery.htmlwidgets.org/) or do a "flexdashboard" using the templates at [http://rmarkdown.rstudio.com/flexdashboard/](http://rmarkdown.rstudio.com/flexdashboard/) as a guide.

### References

Wong, P. P., Monette, G., and Weiner, N. I. (2001) Mathematical models of cognitive recovery. Brain Injury, 15, 519–530.

Fox, J. (2016) Applied Regression Analysis and Generalized Linear Models, Third Edition. Sage.
