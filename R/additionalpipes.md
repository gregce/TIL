# Additional `magrittr` pipes

Magrittr has transformed the way I write R code. The piping paradigm `%>%` introduced by the `magrittr` package and popularized by `dplyr` has been of great use in simplifying complex preprocessing tasks. 

In this TIL, I will expose the other less commonly used pipe operators:
```
%T>%
%$%
%<>%
```


### The T operator allows you to "skip a step"

For example, say I want to plot some data and return the summarization all in one step. The `%T>%` operator allows for this....

```
mtcars %>%
  group_by(cyl) %>%
  ## This pipes the DF into plot but also ungroup
  summarise(avg_hp = mean(hp)) %T>% 
  plot() %>% 
  ungroup()
```

### The exposition operator allows you to expose variable names to functions that do not have a data input

Say for example, I want to modify the above example and show the covariance of avg_hp and avg_mpg. Unfortunately, var() does not have a data input... enter `%$%`

```
mtcars %>%
  group_by(cyl) %>%
  ##next statement introuces the %$% syntax
  summarise(avg_hp = mean(hp), avg_mpg = mean(mpg)) %$%
  var(avg_hp,avg_mpg)

[1] -356.9504


## One change and this fails

mtcars %>%
  group_by(cyl) %>%
  summarise(avg_hp = mean(hp), avg_mpg = mean(mpg)) %>%
  var(avg_hp,avg_mpg)

Error in var(., avg_hp, avg_mpg) : object 'avg_mpg' not found

```

### Finally, the compund pipe operator `%<>%` allows for easy assignment

```

##this 

mtcars %<>%
  group_by(cyl) %>%
  summarise(avg_hp = mean(hp), avg_mpg = mean(mpg))

## is the same as this

mtcars <- mtcars %>%
  group_by(cyl) %>%
  summarise(avg_hp = mean(hp), avg_mpg = mean(mpg))

```
