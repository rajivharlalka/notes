Block Range Index

- helps in searching over large time series data.
- takes up significantly less space compared to B+ trees.
- An entry in BRIN index points to a page and stores two values
	- page's minimum and maximum value.
- BRIN outperforms B+ tree when working on large datasets. [1]

"handling very large tables in which certain columns have some natural correlation with their physical location within the table"

 - extremely low insert costs
 - extremely small index sizes






























References:
[1] https://www.crunchydata.com/blog/postgresql-brin-indexes-big-data-performance-with-minimal-storage
https://www.crunchydata.com/blog/postgres-indexing-when-does-brin-win
