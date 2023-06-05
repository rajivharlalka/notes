
Link: ![https://youtu.be/rCzSNdUOEdg](https://youtu.be/rCzSNdUOEdg)

## Short-forms:
- TPS - Transaction per second.

- high tps 
- consistent low latency
## Common IO performance Issues
Due to wrongly configured `share_buffers` which causes high io.

tuning autovacuum is difficult and mostly changes for every workload. Need to look into autovacuum frequency.

## PostgreSQL I/O Tuning Targets
- shared_bufers
- background writer
- checkpointer
- autovacuum


### I/O statistics views
- pg_stat_database
- pg_statio_all_tables
- pg_stat_bgwriter
- pg_stat_statements
---

pg_stat_io in PG 16

---

### Data driven tuning with pg_stat_io

- data might not always fit in shared_buffers
 ![[Pasted image 20230605130938.png]]

client-backend normal relation write is high which is not is needed. This write is not related to insert/update write but a client looking for shared buffers it can find a buffer and it has to flush the data thats in buffer. This technically should be zero and instead background writer and checkpointer to take up this workload.

probable sol: decrease background delay and increase background_writer_max_lru_pages
(Background writer tuning)



![[Pasted image 20230605131401.png]]

- shared buffers is too small.
- theres almost write for every read: bad
- most likely evicting and reading from the same blocks over and over again.
- signal to increase shared_buffers

Cache Hit ration query
```sql
SELECT (hits/(reads+hits)::float) *100 
FROM pg_stat_io
WHERE
	backend_type ='client backend' AND
	io_object = 'relation' AND
	io_context = 'normal';
```


![[Pasted image 20230605131829.png]]
- avoid premature io
![[Pasted image 20230605132010.png]]
No need to increase shared-buffers here as actual cache-hit ratio is large-enough to handle it.
