# Exercise 3
Below is a comprehensive explanation of the SQL concepts and queries discussed, covering key SQL functionalities such as filtering, grouping, concatenating, subqueries, joins, and the use of the `HAVING` clause.

### Comprehensive SQL Guide

#### 1. Filtering with `IS NULL` and `IS NOT NULL`

In SQL, `IS NULL` and `IS NOT NULL` are used to filter rows based on whether a column's value is `NULL` or not. `NULL` represents a missing or unknown value in a database.

```sql
-- Filter employees with NULL age
SELECT * FROM employee WHERE age IS NULL;

-- Filter employees with non-NULL salary
SELECT * FROM employee WHERE salary IS NOT NULL;
```

#### 2. Grouping and Aggregate Functions

The `GROUP BY` clause groups rows that have the same values in specified columns into summary rows. Aggregate functions like `SUM`, `MAX`, `MIN`, `AVG`, and `COUNT` are used to perform calculations on grouped data.

```sql
-- Calculate total orders placed by each country
SELECT country, COUNT(*) AS order_count FROM orders_data GROUP BY country;

-- Aggregate salary information by age group
SELECT age, SUM(salary) AS total_salary, MAX(salary), MIN(salary), AVG(salary), COUNT(*) FROM employee GROUP BY age;
```

#### 3. Concatenating Grouped Data with `GROUP_CONCAT`

`GROUP_CONCAT` function concatenates values from multiple rows into a single string for each group. You can specify a separator and control the order and distinctness of the concatenated values.

```sql
-- Concatenate distinct states for each country
SELECT country, GROUP_CONCAT(DISTINCT state ORDER BY state DESC SEPARATOR ', ') AS states FROM orders_data GROUP BY country;
```

#### 4. Subqueries

Subqueries are queries nested within another query. They can be used in various places including the `WHERE` clause, `FROM` clause, and `SELECT` clause, providing flexibility in forming complex queries.

```sql
-- Find employees earning more than Rohit
SELECT * FROM employees WHERE salary > (SELECT salary FROM employees WHERE name = 'Rohit');
```

#### 5. Using `IN` and `NOT IN`

The `IN` operator allows you to specify multiple values in a `WHERE` clause, filtering rows that match any of the values in the list. `NOT IN` does the opposite, excluding the listed values.

```sql
-- Find orders from specific states
SELECT * FROM orders_data WHERE state IN ('Seattle', 'Goa');
```

#### 6. Joins

Joins are used to combine rows from two or more tables based on a related column. Types of joins include `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, and `FULL JOIN`.

```sql
-- Example of an INNER JOIN
SELECT o.*, c.* FROM orders o INNER JOIN customers c ON o.cust_id = c.cust_id;
```

#### 7. Group By with Having Clause

The `HAVING` clause is used to filter groups made by `GROUP BY` based on the result of aggregate functions. It's similar to `WHERE`, but for grouped data.

```sql
-- Find countries with exactly one order
SELECT country FROM orders_data GROUP BY country HAVING COUNT(*) = 1;
```

#### 8. `GROUP_CONCAT` for Concatenating Values

This function is useful for concatenating values from multiple rows into a single string within each group, optionally applying `DISTINCT`, ordering the results, and using a custom separator.

```sql
-- Concatenate distinct states for each country
SELECT country, GROUP_CONCAT(DISTINCT state ORDER BY state DESC SEPARATOR ', ') FROM orders_data GROUP BY country;
```

These explanations provide a structured overview of fundamental and advanced SQL functionalities, demonstrating how to efficiently query and manipulate data in a relational database system.