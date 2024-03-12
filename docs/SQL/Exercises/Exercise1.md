
## SQL Commands

### Show Databases
```sql
SHOW DATABASES;
```

### Create Database
```sql
CREATE DATABASE noob_db;
```

### Drop Database
```sql
DROP DATABASE first_demo;
```

### Use Database
```sql
USE noob_db;
```

### Create Table
```sql
CREATE TABLE IF NOT EXISTS employee (
    id INT,
    emp_name VARCHAR(20)
);
```

### Show Tables
```sql
SHOW TABLES;
```

### Show Table Definition
```sql
SHOW CREATE TABLE employee;
```

The `SHOW CREATE TABLE` statement in SQL is a useful command that displays the `CREATE TABLE` statement that would create an exact copy of the existing table specified. This command is particularly handy when you want to understand how a table is structured, including its column definitions, data types, default values, and any constraints like primary keys, foreign keys, unique constraints, check constraints, and indexes associated with the table.

### Create Table with More Columns
```sql
CREATE TABLE IF NOT EXISTS employee_v1 (
    id INT,
    name VARCHAR(50),
    salary DOUBLE, 
    hiring_date DATE 
);
```

### Insert Data Syntax 1
```sql
INSERT INTO employee_v1 VALUES(1, 'Shashank', 1000, '2021-09-15');
```

### Insert Data Syntax 2
```sql
INSERT INTO employee_v1(salary, name, id) VALUES(2000, 'Rahul', 2);
```

### Insert Multiple Records
```sql
INSERT INTO employee_v1 VALUES
    (3, 'Amit', 5000, '2021-10-28'),
    (4, 'Nitin', 3500, '2021-09-16'),
    (5, 'Kajal', 4000, '2021-09-20');
```

### Fetch Data from Table
```sql
SELECT * FROM employee_v1;
```

### Table with Integrity Constraints
```sql
CREATE TABLE IF NOT EXISTS employee_with_constraints (
    id INT,
    name VARCHAR(50) NOT NULL,
    salary DOUBLE, 
    hiring_date DATE DEFAULT '2021-01-01',
    UNIQUE (id),
    CHECK (salary > 1000)
);
```

- **Column-level constraints** are defined immediately after the column definition. This includes `NOT NULL` and `DEFAULT` values, which are attributes of individual columns.
- **Table-level constraints** are defined after all columns have been defined. Examples include `UNIQUE`, `PRIMARY KEY`, `FOREIGN KEY`, and `CHECK` constraints that might span multiple columns.

### Integrity Constraint Failure 1
```sql
-- Exception: Column 'name' cannot be null
INSERT INTO employee_with_constraints VALUES(1, null, 3000, '2021-11-20');
```

### Correct Record for Integrity Constraint 1
```sql
INSERT INTO employee_with_constraints VALUES(1, 'Shashank', 3000, '2021-11-20');
```

### Integrity Constraint Failure 2
```sql
-- Exception: Duplicate entry '1' for key 'employee_with_constraints.id'
INSERT INTO employee_with_constraints VALUES(1, 'Rahul', 5000, '2021-10-23');
```

### Correct Record for Unique Constraint
```sql
-- Unique can accept NULL
INSERT INTO employee_with_constraints VALUES(null, 'Rahul', 5000, '2021-10-23');
```

### Integrity Constraint Failure 3
```sql
-- Exception: Duplicate entry NULL for key 'employee_with_constraints.id'
INSERT INTO employee_with_constraints VALUES(null, 'Rajat', 2000, '2020-09-20');
```

### Integrity Constraint Failure 4
```sql
-- Exception: Check constraint 'employee_with_constraints_chk_1' is violated
INSERT INTO employee_with_constraints VALUES(5, 'Amit', 500, '2023-10-24');
```

### Test Default Date Constraint
```sql
-- Test for Default Date Constraint
INSERT INTO employee_with_constraints(id, name, salary) VALUES(7, 'Neeraj', 3000);
```

### Select Data from Table with Constraints
```sql
SELECT * FROM employee_with_constraints;
```

### Table with Constraints (Alternate Syntax)
```sql
CREATE TABLE IF NOT EXISTS employee_with_constraints_tmp (
    id INT,
    name VARCHAR(50) NOT NULL,
    salary DOUBLE, 
    hiring_date DATE DEFAULT '2021-01-01',
    CONSTRAINT unique_emp_id UNIQUE (id),
    CONSTRAINT salary_check CHECK (salary > 1000)
);
```

### Check Constraint Failure with Name
```sql
-- Exception: Check constraint 'salary_check' is violated
INSERT INTO employee_with_constraints_tmp VALUES(5, 'Amit', 500, '2023-10-24');
```
