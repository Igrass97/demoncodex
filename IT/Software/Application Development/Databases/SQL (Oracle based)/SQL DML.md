Data Manipulation Language sentences are used to manage data records stored within the database tables.

- **SELECT**: Used to query or fetch selected fields or columns from a database table.
- **INSERT**: Used to insert new data records or rows in the database table.
- **UPDATE**: Used to set the value of a field or column for a particular record to a new value.
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

---
### WHERE

``` SQL
SELECT * FROM Customers  
WHERE Country='Mexico';
```

| Operator       | Description                                                     |
| -------------- | --------------------------------------------------------------- |
| =              | Equal                                                           |
| <              | Less than                                                       |
| >              | Greater than                                                    |
| <>             | Not equal                                                       |
| = ANY/ALL      | Compares with all values in a list; = ANY is equivalent to IN   |
| < ALL          | Less than all values in a list or subquery                      |
| > ALL          | Greater than all values in a list or subquery                   |
| <= ALL         | Detects the smallest value in a list or subquery                |
| >= ALL         | Detects the largest value in a list or subquery                 |
| < ANY          | Less than some values in a list or subquery                     |
| > ANY          | Greater than some values in a list or subquery                  |
| IN             | Equal to at least one value in a list or subquery               |
| NOT IN         | Not equal to at least one value in a list or subquery           |
| BETWEEN        | Within an inclusive range defined by lower and upper bounds     |
| NOT BETWEEN    | Outside an inclusive range defined by lower and upper bounds    |
| LIKE           | Matches a pattern with % (wildcards for multiple values)        |
| _ (underscore) | Matches a pattern with a single character wildcard              |
| NOT LIKE       | Does not match a pattern with % (wildcards for multiple values) |
| NOT LIKE _     | Does not match a pattern with a single character wildcard       |
| EXISTS         | Existence test in a subquery                                    |
| NOT EXISTS     | Non-existence test in a subquery                                |               |                                                                 |

---
### GROUP BY
The `GROUP BY` statement groups rows that have the same values into summary rows, like "find the number of customers in each country".

The `GROUP BY` statement is often used with aggregate functions (`COUNT()`, `MAX()`, `MIN()`, `SUM()`, `AVG()`) to group the result-set by one or more columns.

``` SQL
SELECT COUNT(customer_id), country  
FROM customers
GROUP BY country;
```

---
### HAVING
The `HAVING` clause was added to SQL because the `WHERE` keyword cannot be used with aggregate functions.
Filters GROUPS created using `GROUP BY`.

``` SQL
SELECT COUNT(customer_id), country  
FROM customers  
GROUP BY country  
HAVING COUNT(customer_id) > 5;
```

---
### ORDER BY
``` SQL
SELECT * 
FROM Products  
ORDER BY Price DESC|ASC;
```

---
### Single Row Functions
Single row function in SQL are the ones who work on a single row and return one output per row.

Single row function in SQL can be character, numeric, date, and conversion functions. these functions are used to modify data items.

See https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/Single-Row-Functions.html#GUID-C4201DFA-90C5-46DA-B528-0B6D4E8C647A for a full list.

### Aggregate Functions
Aggregate functions return a single result row based on groups of rows, rather than on single rows. Aggregate functions can appear in select lists and in `ORDER` `BY` and `HAVING` clauses. They are commonly used with the `GROUP` `BY` clause in a `SELECT` statement, where Oracle Database divides the rows of a queried table or view into groups.

- **Count()**
- **Sum()**
- **Avg()**
- **Min()**
- **Max()**

``` SQL
SELECT AVG(salary)
FROM employees;

/* Count Distinct or All employee names */ 
SELECT COUNT(DISTINCT | ALL name)
FROM employees;
```

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