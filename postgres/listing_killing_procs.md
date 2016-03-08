# Listing running transactions AND killing them

Sometimes you might issue an un-optimizng query and forget about it. Never fear, there is a really easy way to figure what is running (and subequently kill those processes)

### Conduct investigation

```
select * from pg_stat_activity;

45864   nyc_taxi_data   25408   10  postgres    FALSE   2016-03-08 20:53:40.856744+00
45864   nyc_taxi_data   25333   32189   midsuser    FALSE   2016-03-08 21:01:40.000021+00
```

### Kill that errant process

```
  SELECT pg_cancel_backend(25408); 
```

