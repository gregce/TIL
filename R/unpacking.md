# Break down anything into its individual components!
 
It's often easier or necessary to manipulate vectors when you have a list, matrix or dataframe. 

`Unlist()` is a very helpful function to unpack lists into vectors, but did you know that the `c()` function with the `recursive=TRUE` argument works on just about anything?

Use Case:
You want to unpack objects in R!

### Unpack a matrix!

```
> matrix(c(2,3,4,5,3,5), nrow = 2, ncol = 3)
     [,1] [,2] [,3]
[1,]    2    4    3
[2,]    3    5    5

my.matrix <- matrix(c(2,3,4,5,3,5), nrow = 2, ncol = 3)

> c(my.matrix, recursive=TRUE)
[1] 2 3 4 5 3 5
```

### Unpack a column or an entire dataframe

```
> library(data.table)
> my.dataframe <- data.table(x=c("b","b","b","a","a"),v=rnorm(5))
> my.dataframe
   x          v
1: b -1.2660600
2: b  2.4019710
3: b -1.0933418
4: a  1.3680858
5: a -0.8716245

> c(my.dataframe, recursive = TRUE)
                  x1                   x2                   x3                   x4 
                 "b"                  "b"                  "b"                  "a" 
                  x5                   v1                   v2                   v3 
                 "a"  "-1.26606004766633"   "2.40197103332027"   "-1.0933417757497" 
                  v4                   v5 
  "1.36808582683175" "-0.871624476980082" 

> c(my.dataframe$x, recursive = TRUE)
[1] "b" "b" "b" "a" "a"


```

# Sweet!
