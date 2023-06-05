![Row-Estimates](https://www.youtube.com/watch?v=CQmvelOnFJU)


- hash joins, merge joins
- nested loops are good where the relation(no of rows) on one side is smaller. 
- check : analyse the table, collect statistics again.
- we can analyse a single column
- also happens as a part of auto vacuum
- auto vacuum has three task: 
	- vacuuming
	- prevent transaction from freezing
	- auto analyzing
	- maintaining free space map and visibility map
- explain analyze and vacuum analyze are completely different
- explain only doesn't help us to learn anything actually
- Only Explain helps us to know how planner thinks about the data
- we can check when analyze ran
	- all log entries should be there
	- pg_stat_user_tables
- default_statistics_target -> increases show significant higher disk io
- systematic approach - analyse depends on table size and no, of packets to analyse

### holistic approach

- if we increase no. of buckets the queries should not slow down.
- any other parts of workload which struggle from our change and ensure that we changed something then other parts atleast remain the same.
- query plans is where the mis-estimate happen.

## More relevant links
* ANALYZE (docs) [https://www.postgresql.org/docs/curre...](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbGRpRWV3b2h0cjV3Vk8zRm9HcTI1dlhUamlDZ3xBQ3Jtc0trTUhXWk1UcjlWcVo2MWN3cVI0akl1RTZTaUJMODlGck5xVXhJYUNUTGVWSEJyV0tNMmZtUlAtbEEtYXpzRjNJcDUyV3FUWHRQbUQxOFhmWEVTQk9Rb0NqX1A5NHpVSXppektuNjhKYXZaZ19kUEJjYw&q=https%3A%2F%2Fwww.postgresql.org%2Fdocs%2Fcurrent%2Fsql-analyze.html&v=CQmvelOnFJU)
- Autovacuum config (docs) [https://www.postgresql.org/docs/curre...](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqa0FWSGxvM2lnLUNiaWpyeGFvUXpnVG85UEtqUXxBQ3Jtc0ttUzdDZ2dLTUJVVTQ3NkcwcW12NENydjhBMFVUQllDX3pMQlRlYVoyTGR5RGUzOElJdnJzN05zT2ljSU1fR0MwVWtFVlZLMjIwQmNlVnk3Z2VTeDA4WnNLdjFiZEktd3Yya2NDSjRtQ19qYWk5VDNyaw&q=https%3A%2F%2Fwww.postgresql.org%2Fdocs%2Fcurrent%2Fruntime-config-autovacuum.html&v=CQmvelOnFJU) 
- Statistics used by the planner (docs) [https://www.postgresql.org/docs/curre...](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbmRWcnJVWjBPX0kwWmJtVk9UekhMc2wyZVpLZ3xBQ3Jtc0tuSEYtQkRhSEx0SDQwcGFkUDVTcF9INGVOcjJJN0RLazZBNnJJU1F2Ynk1S1lycG1PUTlkZGxPLUltR3RyNnIzMkRRdEdXc2UyeldnS1c0WncxQ0lGcl8xeVlIVU54NXRHWVFQWlZTZ1c0YlB3MDZLNA&q=https%3A%2F%2Fwww.postgresql.org%2Fdocs%2Fcurrent%2Fplanner-stats.html&v=CQmvelOnFJU) 
- CREATE STATISTICS (docs) [https://www.postgresql.org/docs/curre...](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbUpQMWNNbUJpZ2VPUTZfdHZycDVoeEQyRW5LQXxBQ3Jtc0trYy1iZ1N0OE9SOWJDSElJdkNBb2I4NXFVSVNhaU1GUHB3azhFTTd6Q2pNUHpMWkhtTHdFbnp0WVdCcWp1NEhzUFc2OTBXSU9fWmt2dnVWQjJYMnZHbzdNUHhheEM1N1g3WW5jRXg4bFhOVUx1bElWZw&q=https%3A%2F%2Fwww.postgresql.org%2Fdocs%2Fcurrent%2Fsql-createstatistics.html&v=CQmvelOnFJU) 
- Row count estimates (pgMustard blog post) [https://www.pgmustard.com/blog/2018/1...](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbEQtRnQ3OV9tdDMwb1FWdnAxR2hnaFpqa19tUXxBQ3Jtc0ttNDlydXJBSjJkSThPdkg0V3VzaFNYemxXY25rdE13dkhib3FCNG5xQXJha09CTnB2VW56c0ZyRzZCbFlPdkxKQk11RFh5dVVBY0pBWFdRUXJkaDh4SURzWEpUbW1KTWR0RU5KcjJKX05zemphSU1VSQ&q=https%3A%2F%2Fwww.pgmustard.com%2Fblog%2F2018%2F12%2F14%2Frow-count-estimates-in-postgres&v=CQmvelOnFJU) 
- pg_hint_plan [https://github.com/ossc-db/pg_hint_plan](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbXp6WVRLRV8way11akI4MFhORkE2RF9nMmc5UXxBQ3Jtc0ttejVPUnFuR0FnUG1RSnJRbVZEOHVnNzRwRjlJeU51dnlod01FQm5NcER1My1tanNORFlSeEJnVTktWUt4U09MY24zazBVbGhOUlRLb0VnbmtzQlBjMW1BS1hwb0FhdHBvNzlOZmZmTklmMkdnNTZjNA&q=https%3A%2F%2Fgithub.com%2Fossc-db%2Fpg_hint_plan&v=CQmvelOnFJU)
- Optimizer methodology (talk by Robert Haas)    [![](https://www.gstatic.com/youtube/img/watch/yt_favicon.png)PostgreSQL Optimi...](https://www.youtube.com/watch?v=XA3SBgcZwtE&t=0s)   
- Tomáš Vondra on statistics and hints (an excellent interview we forgot to mention, sorry!)    [![](https://www.gstatic.com/youtube/img/watch/yt_favicon.png) • s01e06 Tomáš Vondra](https://www.youtube.com/watch?v=8la-OWfD3VI&t=0s)