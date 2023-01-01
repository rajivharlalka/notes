Choose a timezone from:

```sql
SELECT * FROM pg_timezone_names;
```

And set as below given example:

```sql
ALTER DATABASE postgres SET timezone TO 'Europe/Berlin';
```

Use your DB name in place of postgres in above statement.

Alternatively,

```sql
SET TIME ZONE 'Asia/Kolkata'
```

The `pg_timezone_names` table contains the list of all timezone names and the `pg_timezone_abbrevs` table contains all the abbreviations of the timezones.
