---
id: g7sd2yoeuu1cj3jgtiu4uea
title: Joins
desc: ''
updated: 1657965342790
created: 1657959040462
---


# JOINS in SQL

```sql
-- sample sql table to demonstrate joins
CREATE TABLE one (num integer,name varchar);

CREATE TABLE two (num integer,value varchar);

INSERT INTO one(num,name)
    VALUES 
        (1,'a'),
        (2,'b'),
        (3,'c'),
        (4,'d'),
        (5,'e');


INSERT INTO two(num,value)
    VALUES 
        (1,'xxx'),
        (3,'yyy'),
        (5,'zzz'),
        (6,'aaa');
```

## CROSS JOIN

Every row of table t1 is matched with every row of table t2.

```SQL
postgres=# SELECT * FROM one CROSS JOIN two;
 num | name | num | value
-----+------+-----+-------
   1 | a    |   1 | xxx
   1 | a    |   3 | yyy
   1 | a    |   5 | zzz
   2 | b    |   1 | xxx
   2 | b    |   3 | yyy
   2 | b    |   5 | zzz
   3 | c    |   1 | xxx
   3 | c    |   3 | yyy
   3 | c    |   5 | zzz
   4 | d    |   1 | xxx
   4 | d    |   3 | yyy
   4 | d    |   5 | zzz
   5 | e    |   1 | xxx
   5 | e    |   3 | yyy
   5 | e    |   5 | zzz
```

## INNER JOIN

Columns which are present in both i.e. intersection

```SQL
postgres=# SELECT * FROM one t1 INNER JOIN two t2 ON t1.num=t2.num;
 num | name | num | value
-----+------+-----+-------
   1 | a    |   1 | xxx
   3 | c    |   3 | yyy
   5 | e    |   5 | zzz
```

## OUTER JOIN

Missing columns are present based on type of join

```SQL
postgres=# SELECT * FROM one t1 RIGHT OUTER JOIN two t2 ON t1.num=t2.num;
 num | name | num | value
-----+------+-----+-------
   1 | a    |   1 | xxx
   3 | c    |   3 | yyy
   5 | e    |   5 | zzz
     |      |   6 | aaa
(4 rows)

postgres=# SELECT * FROM one t1 LEFT JOIN two t2 ON t1.num=t2.num;
 num | name | num | value
-----+------+-----+-------
   1 | a    |   1 | xxx
   2 | b    |     |
   3 | c    |   3 | yyy
   4 | d    |     |
   5 | e    |   5 | zzz
(5 rows)

postgres=# SELECT * FROM one t1 LEFT OUTER JOIN two t2 ON t1.num=t2.num;
 num | name | num | value
-----+------+-----+-------
   1 | a    |   1 | xxx
   2 | b    |     |
   3 | c    |   3 | yyy
   4 | d    |     |
   5 | e    |   5 | zzz
(5 rows)

postgres=# SELECT * FROM one t1 FULL JOIN two t2 ON t1.num=t2.num;
 num | name | num | value
-----+------+-----+-------
   1 | a    |   1 | xxx
   2 | b    |     |
   3 | c    |   3 | yyy
   4 | d    |     |
   5 | e    |   5 | zzz
     |      |   6 | aaa
```

NOTE:
- When the type of join is not specified , Inner join occurs
- There isnt anything like left inner or left outer join. 
- If Left/Right keyword is used, it means it's an outer join
- The following three sntax are identical
```sql
FROM a, b WHERE a.id = b.id AND b.val > 5
-- and:

FROM a INNER JOIN b ON (a.id = b.id) WHERE b.val > 5
-- or perhaps even:

FROM a NATURAL JOIN b WHERE b.val > 5
```