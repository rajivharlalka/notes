# Data Types

## Numeric DataTypes

| name       | size     |
| ---------- | -------- |
| small int  | 2 bytes  |
| integer    | 4 bytes  |
| bigint     | 8 bytes  |
| decimal    | variable |
| numeric    | variable |
| serail     | 4 bytes  |
| big serial | 8 bytes  |

- Syntax for numeric datatype: NUMERIC(precision,scale) where in 12.343 5 is precision and 3 is scale.

## Serials

```sql
CREATE TABLE tablename (
    colname SERIAL
);
-- is equivalent to specifying:

CREATE SEQUENCE tablename_colname_seq AS integer;
CREATE TABLE tablename (
    colname integer NOT NULL DEFAULT nextval('tablename_colname_seq')
);
ALTER SEQUENCE tablename_colname_seq OWNED BY tablename.colname;
```

P.S.: The sequence is marked Owned by the column so that it will be dropped off if the column or table is dropped

## Character Data Type

| Name                             | Description                |
| -------------------------------- | -------------------------- |
| character varying(n), varchar(n) | variable-length with limit |
| character(n), char(n)            | fixed-length, blank padded |
| text                             | variable unlimited length  |

## Date Time Data Types

| Name                                    | Storage Size                  | Description                           | Low Value        | High Value      | Resolution    |
| --------------------------------------- | ----------------------------- | ------------------------------------- | ---------------- | --------------- | ------------- |
| timestamp [ (p) ] [ without time zone ] | 8 bytes                       | both date and time (no time zone)     | 4713 BC          | 294276 AD       | 1 microsecond |
| timestamp [ (p) ] with time zone        | 8 bytes                       | both date and time, with time zone    | 4713 BC          | 294276 AD       | 1 microsecond |
| date                                    | 4 bytes                       | date (no time of day)                 | 4713 BC          | 5874897 AD      | 1 day         |
| time [ (p) ] [ without time zone ]      | 8 bytes time of day (no date) | 00:00:00                              | 24:00:00         | 1 microsecond   |
| time [ (p) ] with time zone             | 12 bytes                      | time of day (no date), with time zone | 00:00:00+1559    | 24:00:00-1559   | 1 microsecond |
| interval [ fields ] [ (p) ]             | 16 bytes                      | time interval                         | -178000000 years | 178000000 years | 1 microsecond |

## Boolean Data Type

| Name    | Size   |
| ------- | ------ |
| boolean | 1 byte |

```sql
CREATE TYPE mood AS ENUM ('sad', 'ok', 'happy');
```

- All normal comparator functions work the same way as they would do with other data types.
- two custom enums cannot be comparaed directly

```sql
SELECT person.name, holidays.num_weeks FROM person, holidays
  WHERE person.current_mood = holidays.happiness;
-- to do this, below is the correct method
SELECT person.name, holidays.num_weeks FROM person, holidays
  WHERE person.current_mood::text = holidays.happiness::text;
```

- enums are case-sensitive
- occupies 4 bytes disk space
- all enums can be found from the `pg_enum` table.

## Arrays

```sql
CREATE TABLE array_table (
  name  text,
  pay_by_quater integer[],
  schedule text[][]
);
```

- array elements can be selected with the `[]` notation
- multi dimension arrays can also be inserted.
- arrays are inserted like this -> `{1,2,3,4}` , `{{1,2,3,4},{5,6,7,8}}`
- array can also be referred as slices using the `[lower_bound: upper_bound]` reference.
- `array_dims` function returns the dimesnion of array.
- arrays can be concatenated with `||` operator.

## Domain

Domains are extensios to underlying datatypes usually with some contraints premade for easy usage.

```sql
CREATE DOMAIN posint AS integer CHECK (VALUE>0);
CREATE TABLE mytable (id posint);
INSERT INTO mytable VALUES (1); --works
INSERT INTO mytable VALUES (-1); --fails
```

