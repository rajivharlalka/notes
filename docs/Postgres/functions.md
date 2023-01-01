---
id: ujnosfbryqsmvpj5n621ueh
title: Functions
desc: ""
updated: 1657774924683
created: 1657774812752
---

# Function creation

example:

```sql
 CREATE FUNCTION concat_lower_or_upper(a text, b text, uppercase boolean DEFAULT false)
RETURNS text
AS
$$
 SELECT CASE
        WHEN $3 THEN UPPER($1 || ' ' || $2)
        ELSE LOWER($1 || ' ' || $2)
        END;
$$
LANGUAGE SQL IMMUTABLE STRICT;
```

# Function Calling

```sql
SELECT concat_lower_or_upper('postgres','rocks');
```

## Some Special Fucntions

## SERIAL

```sql
CREATE TABLE products(
    product_id SERIAL
    price numeric
    date TIMESTAMP
)
```

SERIAL auto-increments a value based on previous value and make the colum not necessary.

## GENERATED COLUMNS

if a column depends on the value of another column, then it's vlaue can be filled using the `GENERATED COLUMNS` keyword.

```sql
CREATE TABLE people (
    ...,
    height_cm numeric,
    height_in numeric GENERATED ALWAYS AS (height_cm / 2.54) STORED
);
```
