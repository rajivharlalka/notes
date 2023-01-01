
# Window Functions

Calculation of values(using functions such as avg) is someitme helpful using window functions.
 
Window functions generally follow the `OVER` keyword. 

```sql
SELECT name,class,roll,avg(marks) OVER (PARTITION by class) FROM CLASS_MARKS;
```

Here the students are partitoned by the class column and the aggregate function is used over it. This is more of like using the aggregate fucntions itslef, but helps as there is less computation involved.

The OVER clause determines exactly how the rows of the query are split up for processing by the window function. The PARTITION BY clause within OVER divides the rows into groups, or partitions, that share the same values of the PARTITION BY expression(s). For each row, the window function is computed across the rows that fall into the same partition as the current row.  
