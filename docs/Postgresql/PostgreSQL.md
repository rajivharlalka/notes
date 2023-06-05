- Maintenance commands: ANALYZE, VACUUM, VACUUM FULL/CLUSTER 
- Index commands: CREATE INDEX, REINDEX
- Backup/replication: BASE BACKUP
- Data load/unload: COPY

--- 
- ANALYZE: pg_stat_progress_analyze
- VACUUM: pg_stat_progress_vacuum
- VACUUM FULL, CLUSTER: pg_stat_progress_cluster
- CREATE INDEX,REINDEX: pg_stat_progress_create_index
- BASE BACKUP: pg_stat_progress_basebackup
- COPY: pg_stat_progress_copy
---

### Progress Meter

#### base_backup
```sql
SELECT pid, phase,
100.0*((backup_streamed*1.0)/backup_total) AS "progress%"
FROM pg_stat_progress_basebackup;
```

#### COPY FROM % progress will be as follows:
```sql
SELECT (SELECT relname FROM pg_class WHERE oid = relid),
100.0*((bytes_processed*1.0)/bytes_total) AS "progress%"
FROM pg_stat_progress_copy;
```

#### COPY TO % progress will be as follows:
```sql
SELECT relname,
100.0*((tuples_processed*1.0)/(case reltuples WHEN 0 THEN 
10 WHEN -1 THEN 10 ELSE reltuples END)) AS "progress%"
FROM pg_stat_progress_copy JOIN pg_class on oid = relid;
```

---
Killing in-transaction sessions
```sql
SELECT pg_terminate_backend(pid)
 FROM pg_stat_activity
WHERE state = 'idle in transaction'
 AND current_timestamp – state_change > '10 min';
```