# Random sampling in Hive

It's often necessary to take a random sample of "big data" for one reason or another. Accordingly, there are a couple of easy ways to do this in HIVE but some are more performant than others. 

Use Case:
You want to grab a performant random

### The easiest way (not truly random)
Hive makes no guarantees that selecting data will be returned in a specified order... So you can do this but be aware that it's not truly random as the order will likely be the same as the data exists on disk.
```
select * from fakedata limit 100;
```

### The easiest random way
This will give random data but depending on the size of your table the performance can be very, very slow due to the nature of the way hive operates: in order to actually impose ordering, all of the data is first forced into a single reducer and then that reducer sorts the *entire* dataset. Yuck!
```
select * from fakedata order by rand() limit 100;
```

### Possibly the best way
This optimization leverages a number of hive language constructs including:
Sort By - which sorts rows prior to feeding to the reducer
Distribute by - which uses the rand function to ensure that all the rows go to the same reducer
```
select * from fakedata
distribute by rand()
sort by rand()
limit 10000;
```

