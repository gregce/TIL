# Approximating group concat in Hive

Unfortunately Hive doesn't have a `group_concat` function like MySQL. It does, however; have `collect_set` and `collect_list` functions which can be used with another wrapper functinon `concat_ws` to return a string representation similar to `group_concat`. 

Use Case:
You want to collapse the values from a number of rows into a single concatenated value/field and determine its length

### Starting point w/ a list without the same number of columns

```
str(fakeobj)

List of 2
 $ :List of 8
  ..$ name   : chr "Nash"
  ..$ num    : chr "1347523241"
  ..$ add    : chr "819 Et, Avenue"
  ..$ city   : chr "Comblain-la-Tour"
  ..$ country: chr "Libya"
  ..$ zip    : chr "9349"
  ..$ rand   : chr "-0.143485200785"
  ..$ pin    : chr "16942250999"
 $ :List of 7
  ..$ name: chr "Noble"
  ..$ num : chr "1370069110"
  ..$ add : chr "5275 Amet Ave"
  ..$ city: chr "Zaragoza"
  ..$ zip : chr "3876"
  ..$ rand: chr "0.00801882167272"
  ..$ pin : chr "25719278199"
```

### The below fails 

```
data.frame(do.call(rbind.data.frame, fakeobj))
Error in (function (..., deparse.level = 1, make.row.names = TRUE)  : 
  numbers of columns of arguments do not match
```

### Instead, use data.table's rbindlist with the fill option!

```
library(data.table)

rbindlist(fakeobj, fill=TRUE)
    name        num            add             city country  zip             rand         pin
1:  Nash 1347523241 819 Et, Avenue Comblain-la-Tour   Libya 9349  -0.143485200785 16942250999
2: Noble 1370069110  5275 Amet Ave         Zaragoza      NA 3876 0.00801882167272 25719278199
```


