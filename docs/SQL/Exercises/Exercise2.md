# Exercise2

In this guide, we'll explore various SQL database operations, including creating databases and tables, inserting and selecting data, modifying table structures, enforcing data integrity through constraints, and more. Each operation will be explained with SQL examples for a practical understanding.

## Creating and Selecting from Tables

### Creating a Database

To start, we create a database named `class2_db`. This serves as the container for our tables and data.

```sql
CREATE DATABASE class2_db;
```

### Selecting a Database

Before performing operations, we select our newly created database.

```sql
USE class2_db;
```

### Creating the Employee Table

We create an `employee` table to store employee details. Initially, it includes columns for an ID, name, address, and city.

```sql
CREATE TABLE IF NOT EXISTS employee(
    id INT,
    name VARCHAR(50),
    address VARCHAR(50),
    city VARCHAR(50)
);
```

### Inserting Data

Insert a record into the `employee` table. This adds an employee with ID 1, named Shashank, residing in RJPM, Lucknow.

```sql
INSERT INTO employee VALUES(1, 'Shashank', 'RJPM', 'Lucknow');
```

### Selecting Data

Retrieve and display all records from the `employee` table to verify our insert operation.

```sql
SELECT * FROM employee;
```

## Modifying Table Structure and Data Integrity

### Adding a New Column

We realize the need to store employees' dates of birth (DOB), so we add a `DOB` column.

```sql
ALTER TABLE employee ADD DOB date;
```

### Modifying Column Specifications

To accommodate longer names, we modify the `name` column to allow up to 100 characters.

```sql
ALTER TABLE employee MODIFY COLUMN name VARCHAR(100);
```

### Removing a Column

We decide that the `city` column is no longer needed and remove it from the table.

```sql
ALTER TABLE employee DROP COLUMN city;
```

### Renaming a Column

To make the `name` column's purpose clearer, we rename it to `full_name`.

```sql
ALTER TABLE employee RENAME COLUMN name TO full_name;
```

## Enforcing Data Integrity

### Adding a Unique Constraint

To ensure each employee has a unique ID, we add a unique constraint to the `id` column.

```sql
ALTER TABLE employee ADD CONSTRAINT id_unique UNIQUE(id);
```

### Removing Constraints

If the unique constraint on `id` is no longer needed, we can remove it.

```sql
ALTER TABLE employee DROP CONSTRAINT id_unique;
```

## Primary Key and Foreign Key Demonstrations

### Creating a Table with a Primary Key

We create a `persons` table, ensuring each person has a unique `id` through a primary key constraint.

```sql
CREATE TABLE persons
(
    id INT, 
    name VARCHAR(50), 
    age INT,
    CONSTRAINT pk PRIMARY KEY (id) 
);
```

### Demonstrating Foreign Key Usage

To illustrate relationships between tables, we create `customer` and `orders` tables. Orders are linked to customers through a foreign key constraint.

```sql
CREATE TABLE customer
(
    cust_id INT,
    name VARCHAR(50), 
    age INT,
    CONSTRAINT pk PRIMARY KEY (cust_id) 
);

CREATE TABLE orders
(
    order_id INT,
    order_num INT,
    customer_id INT,
    CONSTRAINT pk PRIMARY KEY (order_id),
    CONSTRAINT fk FOREIGN KEY (customer_id) REFERENCES customer(cust_id)
);
```

## Data Manipulation and Analysis

### Updating Data

We can update records, such as increasing each employee's salary by 20%.

```sql
UPDATE employee SET salary = salary + salary * 0.2;
```

### Deleting Data

If certain records are no longer needed, like employees who joined on a specific date, we can remove them.

```sql
DELETE FROM employee WHERE hiring_date = '2021-08-10';
```

### Filtering and Sorting Data

SQL provides powerful tools for querying and analyzing data. For instance, we can find employees who joined within a specific date range or those earning within a certain salary range.

```sql
-- Find employees who joined between August 5, 2021, and August 11, 2021.
SELECT * FROM employee WHERE hiring_date BETWEEN '2021-08-05' AND '2021-08-11';

-- Find employees earning between 10,000 and 28,000.
SELECT * FROM employee WHERE salary BETWEEN 10000 AND 28000;
```

### Using `LIKE` for Pattern Matching

The `LIKE` clause allows for flexible string matching, such as finding employees whose names start with 'S' or end with 'l'.

```sql
-- Names starting with 'S'
SELECT * FROM employee WHERE name LIKE 'S%';

-- Names ending with 'l'
SELECT

 * FROM employee WHERE name LIKE '%l';
```

This guide provides a foundational understanding of managing databases with SQL, from creating and modifying tables to querying and analyzing data with a focus on syntax and practical examples.