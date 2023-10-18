Data Manipulation Language sentences are used to manage data records stored within the database tables.

- **SELECT**: Used to query or fetch selected fields or columns from a database table
- **INSERT**: Used to insert new data records or rows in the database table
- **UPDATE**: Used to set the value of a field or column for a particular record to a new value
- **DELETE**: 	Used to remove one or more rows from the database table.

## SELECT
``` SQL
SELECT <column list, constants, functions, subqueries>
FROM <table list, views, subqueries>
WHERE <condition> [AND, OR, NOT] <condition> 
GROUP BY <column list>
HAVING <condition> [AND, OR, NOT] <condition> 
ORDER BY <column list> [DESC, ASC];
```

### GROUP BY
Complete Here

### HAVING
Complete here

### ORDER BY
Complete Here
### Single Row Functions
Single row function in SQL are the ones who work on a single row and return one output per row.

Single row function in SQL can be character, numeric, date, and conversion functions. these functions are used to modify data items.

See https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/Single-Row-Functions.html#GUID-C4201DFA-90C5-46DA-B528-0B6D4E8C647A for a full list

### Aggregate Functions
Aggregate functions return a single result row based on groups of rows, rather than on single rows. Aggregate functions can appear in select lists and in `ORDER` `BY` and `HAVING` clauses. They are commonly used with the `GROUP` `BY` clause in a `SELECT` statement, where Oracle Database divides the rows of a queried table or view into groups.
## INSERT
``` SQL
INSERT INTO table_name (column_name_1, column_name_2, column_name_3, ...) VALUES (value1, value2, value3, ...)
```

## UPDATE
``` SQL
UPDATE table_name 
SET column_name_1 = value1, column_name_2 = value2, ... 
WHERE condition;
```

## DELETE
``` SQL
DELETE FROM table_name WHERE condition;
```