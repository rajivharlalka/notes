# Aggregate Functions

## max

Returns max value of the column

```sql
SELECT max(temp_lo) FROM weather;
```
P.S.: Aggregate Functions dont work directly on a where clause.
A sub query is required in that case.

eg;
```sql
-- WRONG
SELECT city FROM weather WHERE temp_lo = max(temp_lo); 

-- Right
SELECT city FROM weather WHERE temp_lo = (SELECT max(temp_lo) FROM weather);
```
