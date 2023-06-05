- If your database is larger than 128 megabytes (MB), then you'll probably benefit from increasing shared_buffers, the physical cache size

- If you have a dedicated database server with 1GB or more of RAM, a reasonable starting value for `shared_buffers` is 25% of the memory in your system

Shared Buffer Heap Hit Rate
```sql
select sum(heap_blks_hit)*100/(sum(heap_blks_read)+sum(heap_blks_hit)+1) from pg_statio_all_tables ;
```

Shared Buffer TOAST hit rate
```sql
select sum(toast_blks_hit)*100/(sum(toast_blks_read)+sum(toast_blks_hit)+1) from pg_statio_all_tables ;
```

Index Hit Rate
```sql
select sum(tidx_blks_hit)*100/(sum(tidx_blks_read)+sum(tidx_blks_hit)+1) from pg_statio_all_tables ;
```

Unused Indexes
```sql 
select relname||'.'||indexrelname from pg_stat_user_indexes where idx_scan=0 and not exists (select 1 from pg_constraint where conindid=indexrelid) ORDER BY relname, indexrelname
```
```sql
select relname||'.'||indexrelname from pg_stat_user_indexes where idx_scan=0 ORDER BY relname, indexrelname
```

Ref: https://github.com/jfcoz/postgresqltuner


- If there is heavy write activity, you may want to set wal_buffers to a much higher value than the default. In fact, wal_buffers is automatically set from the value of shared_buffers, following a rule that fits most cases. However, it is always possible to specify an  
explicit value that overrides the computation for the very few cases where the rule is not good enough.

- If you're doing heavy write activity and/or large data loads, you may want to set max_wal_size and min_wal_size higher than the default to avoid wasting input/output (I/O) in excessively frequent checkpoints. You may also wish to set checkpoint_timeout an checkpoint_completion_target.

