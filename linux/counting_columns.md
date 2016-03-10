# Counting CSV columns using bash

A very simplistic method (does not handle all edge cases) of getting the general idea of how many rows exists in a CSV can be done with a single line of bash.

### Contents of a file

```
$ cat mytxt.txt

1,2,3,4,5
a,b,c,d,e
a,b,c,d,e
```

###  Get the top row

```
$ head -1 mytxt.txt
1,2,3,4,5

```

###  Leverage SED to remove everything except columns

```
$ head -1 mytxt.txt | sed 's/[^,]//g'
,,,,
```

###  Pipe it into wc -c 

```
$ head -1 myfile.csv | sed 's/[^,]//g' | wc -c
5
```
