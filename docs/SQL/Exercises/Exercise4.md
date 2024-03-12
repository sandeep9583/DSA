# Exercise 4

Let's break down and explain the SQL concepts and examples you provided, from group rollup operations to window functions, including practical use cases like generating sequences and handling hierarchical data with Common Table Expressions (CTEs).

## Group Rollup

**Purpose**: Calculate total revenue per shop and year-wise revenue.

**Explanation**: The `WITH ROLLUP` modifier is used in `GROUP BY` clauses to create subtotals and grand totals. It can aggregate data across multiple levels, producing a result set that includes rows representing higher-level summaries.

### Example: Total Revenue Calculation
```sql
SELECT
  SUM(payment_amount),
  YEAR(payment_date) AS 'Payment Year',
  store_id AS 'Store'
FROM payment
GROUP BY YEAR(payment_date), store_id WITH ROLLUP
ORDER BY YEAR(payment_date), store_id;
```
This query calculates the total revenue for each store, broken down by year, and includes subtotals for each year and a grand total at the end.

## ANY and ALL Operators

**ANY**: Compares a value to each value in a list or returned by a subquery. It returns true if any comparison is true.

**ALL**: Similar to ANY but returns true only if all comparisons are true.

## EXISTS and NOT EXISTS

**EXISTS**: Checks if a subquery returns any rows. It's useful for conditional checks in queries.

**NOT EXISTS**: The opposite of EXISTS. It checks if a subquery returns no rows.

## Window Functions

Window functions perform calculations across sets of rows related to the current row. They are powerful tools for performing complex analytics tasks like running totals, moving averages, and rankings.

### Example: Frame Clause with Rows BETWEEN
```sql
SELECT *,
       SUM(sales_amount) OVER (ORDER BY sales_date 
                               ROWS BETWEEN 1 PRECEDING AND CURRENT ROW) 
       AS running_total
FROM sales_data;
```
This calculates the running total of sales, including the current row and the one preceding it.

## Common Table Expressions (CTEs)

CTEs provide a way to write more readable and maintainable queries by allowing you to define temporary result sets that you can reference within a SELECT, INSERT, UPDATE, or DELETE statement.

### Recursive CTEs for Hierarchical Data
Recursive CTEs are used to deal with hierarchical data, like organizational structures or category trees.

### Example: Generating a Sequence of Numbers
```sql
WITH RECURSIVE number_sequence AS (
  SELECT 1 AS number
  UNION ALL
  SELECT number + 1 FROM number_sequence WHERE number < 10
)
SELECT * FROM number_sequence;
```
This CTE generates a sequence of numbers from 1 to 10.

### Example: Organizational Chart
```sql
WITH RECURSIVE org_chart AS (
  SELECT emp_id, emp_name, manager_id FROM employees WHERE manager_id IS NULL
  UNION ALL
  SELECT e.emp_id, e.emp_name, e.manager_id FROM employees e INNER JOIN org_chart oc ON e.manager_id = oc.emp_id
)
SELECT * FROM org_chart;
```
This builds an organizational chart by recursively querying employees based on their manager's relationship.

## Practical Examples
The provided SQL snippets demonstrate various operations, from data manipulation and aggregation to advanced analytics with window functions and recursive queries for hierarchical data modeling. By leveraging these techniques, you can perform complex data analysis tasks, generate reports, and extract meaningful insights from your data sets.

The above explanations provide a foundation for understanding the SQL concepts and practices you've outlined, with each section explaining the purpose and application of different SQL features and operations.

# SQL Concepts and Examples Explained

## Group Rollup
Group Rollup is used to aggregate data across multiple levels of grouped data in a single query. It allows us to create subtotals and grand totals within the result set.

### Example Queries
- Calculate total revenue of each shop per year.
- Calculate total revenue per year across all shops.

## ANY and ALL Operations
These operations compare a value to each value in a list or returned by a subquery.
- `ANY` returns true if any comparison is true.
- `ALL` returns true only if all comparisons are true.

## EXISTS and NOT EXISTS Operations
`EXISTS` and `NOT EXISTS` are used in subqueries to test for the existence of rows in a subquery.
- `EXISTS` returns true if the subquery returns one or more records.
- `NOT EXISTS` returns true if the subquery returns no records.

## Window Functions
Window functions perform calculations across a set of rows related to the current row without collapsing groups. Examples include running totals, rankings, and partitioned averages.

### Frame Clause - Rows BETWEEN
The `ROWS BETWEEN` clause in window functions defines the range of rows used to perform the calculations for the current row.

## Common Table Expressions (CTEs)
CTEs offer a way to create temporary result sets that are usable within the execution scope of a single statement. They are useful for organizing complex queries and improving readability.

## Generating Numbers Using WITH RECURSIVE
`WITH RECURSIVE` is used to generate a sequence of numbers by recursively querying the temporary result set created by the CTE.

## Organizational Chart Using Recursive CTEs
Recursive CTEs can represent hierarchical relationships, such as organizational charts, by recursively referring to itself to build a hierarchy tree.

## Examples
The given SQL snippets illustrate the application of the discussed concepts in creating tables, inserting data, and writing queries that utilize group rollup, window functions, CTEs, and other SQL features to analyze and retrieve data efficiently.


