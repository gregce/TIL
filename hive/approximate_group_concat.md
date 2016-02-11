# Approximating group concat in Hive

Unfortunately Hive doesn't have a `group_concat` function like MySQL. It does, however; have `collect_set` and `collect_list` functions which can be used with another wrapper functinon `concat_ws` to return a string representation similar to `group_concat`. 

Use Case:
You want to collapse the values from a number of rows into a single concatenated value/field and determine its length

### Start w/ a query and it's output to get the hang of collect_list

```
SELECT
FROM (
    SELECT country 
        ,collect_list(NAME) AS name_list 
    FROM fakedata
    GROUP BY country 
    ) AS SQ
WHERE size(name_list) > 1 

country                 name_list
Bahrain                 ["Erasmus","Robert"]
Cape Verde              ["Herman","Graham"]
Cocos (Keeling) Islands ["Graiden","Justin"]
```

### The below fails because length() expects a string parameter

```
SELECT length(name_list) as len
FROM (
    SELECT country
        ,collect_list(NAME) AS name_list
    FROM fakedata
    GROUP BY country
    ) AS SQ
WHERE size(name_list) > 1
```

### In the absense of an explict cast function, concat\_ws is a handy stand in that can take an array (your name_list value)

```
SELECT length(concat_ws('', name_list)) as len
FROM (
    SELECT country
        ,collect_list(NAME) AS name_list
    FROM fakedata
    GROUP BY country
    ) AS SQ
WHERE size(name_list) > 1

len
13
12
13
16
```


