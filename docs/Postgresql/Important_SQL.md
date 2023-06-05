```sql
SELECT table_schema ,
       TABLE_NAME ,
       COLUMN_NAME ,
       data_type ||coalesce(' ' || text(character_maximum_length), '') ||coalesce(' ' || text(numeric_precision), '') ||coalesce(',' || text(numeric_scale), '') AS data_type
FROM information_schema.columns
WHERE COLUMN_NAME IN
    (SELECT COLUMN_NAME
     FROM
       (SELECT COLUMN_NAME ,
               data_type ,
               character_maximum_length ,
               numeric_precision ,
               numeric_scale
        FROM information_schema.columns
        WHERE table_schema NOT IN ('information_schema',
                                   'pg_  
catalog')
        GROUP BY COLUMN_NAME ,
                 data_type ,
                 character_maximum_length ,
                 numeric_precision ,
                 numeric_scale) derived
     GROUP BY COLUMN_NAME
     HAVING count(*) > 1)
  AND table_schema NOT IN ('information_schema',
                           'pg_catalog')
ORDER BY COLUMN_NAME ;
```


## Find relation between rows of  table
```sql
SELECT attname, n_distinct  
FROM pg_stats  
WHERE schemaname = 'public'  
AND tablename = 'ord';
```

## Cache Hit Rate
```sql
SELECT 'cache hit rate' AS name, sum(heap_blks_hit) / (sum(heap_blks_hit) + sum(heap_blks_read)) AS ratio FROM pg_statio_user_tables;
```