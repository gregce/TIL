# Approximating select count(*) in postgres

Its a known issue that it can be extremely slow to count rows from big tables in postgres. This is mainly due to MVCC[https://devcenter.heroku.com/articles/postgresql-concurrency] _aka Multi Version Concurrency Control_ which guarantees that reads don't block writes and vice versa.

### This is bad
select count(*) requires postgres do an entire table scan of the query you just issued...

```
## myschema.mytable > 50M rows

SELECT count(*) AS exact_count FROM myschema.mytable;
```

### This is good
Depending on how currently your pg_stats table is - which you can refresh by running ANALYZE <table name>, you'll get a really fast result back!

```
## myschema.mytable > 50M rows

SELECT reltuples::bigint AS estimate FROM pg_class where relname='mytable';
```
