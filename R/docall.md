# The do.call function

R has an incredibly interesting function called `do.call`. Here is where `lapply` and `do.call` are different:

&nbsp;&nbsp;&nbsp;`lapply` returns a list the same length of X which contains the result of from applying the passed function

&nbsp;&nbsp;&nbsp;`do.call` on the other hand, constructs and executes a function call from a function and a list of arguments.

Why is this useful you might ask?


### Say for example we start with a list containing a bunch of data.frames 

```
data <- lapply(sapply(as.character(unique(diamonds$cut))
               , function(x) paste("cut == '",x,"'", sep=""))
               , function(x) diamonds %>%
                 filter_(.dots = x) %>%
                 select(cut, clarity, price))  

names(data) <- as.character(unique(diamonds$cut))

head(data$Fair, 5)
Source: local data frame [5 x 3]

     cut clarity price
  (fctr)  (fctr) (int)
1   Fair     VS2   337
2   Fair     SI2  2757
3   Fair     SI2  2759
4   Fair     VS2  2762
5   Fair     VS2  2762

```

### A natural desire may be to merge these things back together to get to the data.frame we started with
```
## Ugly way of doing it

#initialize an empty df
df <- data.frame(character(0)
                 ,character(0)
                 ,character(0))

#loop through the list of dataframes and append them
for (i in 1:length(data)) {
  df <- rbind(df, data[[i]])
}

#print the final concatenated dataframe
head(df, 5)

    cut clarity price
  (fctr)  (fctr) (int)
1  Ideal     SI2   326
2  Ideal     VS1   340
3  Ideal     SI2   344
4  Ideal     SI2   348
5  Ideal     SI2   403
```

### Do.Call way of doing it!

```
df1 <- do.call(rbind, data)

head(df1, 5)

Source: local data frame [5 x 3]

     cut clarity price
  (fctr)  (fctr) (int)
1  Ideal     SI2   326
2  Ideal     VS1   340
3  Ideal     SI2   344
4  Ideal     SI2   348
5  Ideal     SI2   403

```

### So what is going on?
`do.call` operates as if the actual the actual call was 

`rbind(data[[1]], data[[2]], data[[3]], data[[4]], data[[5]])`
