1. `repeat(text,number)` - repeats the text number times.
   - eg: repeat('hello',4) -> hellohellohellohello
2. `num_nulls(arguments)` and `num_nonnulls(arguments)` -> returns the number of nulls and non-null characters in the list of arguments.
   - eg: num_nonnulls(1,2,3,NULL) -> 3
3. [Date Time formatting template patterns](https://www.postgresql.org/docs/current/functions-formatting.html#FUNCTIONS-FORMATTING-DATETIME-TABLE)
4. `overlaps` - returns if two intervl of time overlaps or not.
   - eg: (start1, end1) OVERLAPS (start2, end2)
     (start1, length1) OVERLAPS (start2, length2)
     SELECT (DATE '2001-02-16', DATE '2001-12-21') OVERLAPS
     (DATE '2001-10-30', DATE '2002-10-30');
     Result: true
5. `gen_random_uuid()` -> generates a random uuid version 4
