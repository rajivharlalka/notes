## Costs Variables

- seq_page_cost : 1.0
	- Sets the planner's estimate of the cost of a disk page fetch that is part of a series of sequential fetches.
- random_page_cost: 4.0
	- Reducing Value almost equal to `seq_page_cost` would prefer index scans more and increasing the value would make index scans look more expensive.
- cpu_tuple_cost: 0.01
	- planner's estimate of the cost of processing each row during a query.
- cpu_index_tuple_cost: 0.005
	- planner's estimate of cost of processing each index entry during an index scan.
- cpu_operator_cost: 0.0025


## Explanations with various scenarios

1. Simple Sorting on Seq Scan

Query Plan: 
```
> EXPLAIN SELECT * from pg_class ORDER BY relfilenode ;
                            QUERY PLAN
-------------------------------------------------------------------
 Sort  (cost=35.89..36.92 rows=410 width=265)
   Sort Key: relfilenode
   ->  Seq Scan on pg_class  (cost=0.00..18.10 rows=410 width=265)
(3 rows)
```
COST: the value of cost returns us with two values. abc..xyz
	`abc` is the starting cost of returning the first row from the output after performing the process. 
	`xyz` is the total cost of the operation after which all the rows planned would be returned.

Estimated total cost is done using: `(disk pages read * seq_page_cost) + (rows scanned * cpu_tuple_cost)` 
ROWS: The number of rows the planner thinks that would be returned. All calculations are made based on this value.
WIDTH: PostgreSQL's idea about the number of bytes one row of the returned value would contain.





## Disable Different Query Planners


- SET enable_indexscan = TRUE/FALSE
- SET enable_bitmapscan = TRUE/FALSE;


### List all query planners
```sql
SELECT name, setting, short_desc || COALESCE(E'\n' || extra_desc, '')
FROM pg_settings WHERE name ~ '^enable_';
```



Ref: 
1. https://www.depesz.com/2013/04/16/explaining-the-unexplainable/
2. 
