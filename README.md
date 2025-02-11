# SQL Cheat Sheet

## \ud83d\udccc Table of Contents
- [Introduction](#introduction)
- [Database Basics](#database-basics)
- [Data Types](#data-types)
- [DDL (Data Definition Language)](#ddl-data-definition-language)
- [DML (Data Manipulation Language)](#dml-data-manipulation-language)
- [DQL (Data Query Language)](#dql-data-query-language)
- [TCL (Transaction Control Language)](#tcl-transaction-control-language)
- [DCL (Data Control Language)](#dcl-data-control-language)
- [Joins](#joins)
- [Subqueries](#subqueries)
- [Indexes](#indexes)
- [Views](#views)
- [Stored Procedures](#stored-procedures)
- [Triggers](#triggers)
- [Window Functions](#window-functions)
- [Common Table Expressions (CTE)](#common-table-expressions-cte)
- [Performance Optimization](#performance-optimization)
- [LIKE and Regex Search](#like-and-regex-search)

---
## Introduction
SQL (Structured Query Language) is a standard language for accessing and managing databases.

---
## Database Basics
```sql
-- Create a database
CREATE DATABASE my_database;

-- Use a database
USE my_database;

-- Drop a database
DROP DATABASE my_database;
```

---
## Data Types
**Common SQL Data Types:**
- `INT` – Integer
- `VARCHAR(n)` – Variable-length string
- `TEXT` – Large text data
- `BOOLEAN` – True/False
- `DATE` – Date value
- `DATETIME` – Date and time
- `FLOAT` – Floating point number
- `DECIMAL(p,s)` – Fixed precision number

---
## DDL (Data Definition Language)
```sql
-- Create Table
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Alter Table
ALTER TABLE users ADD COLUMN age INT;
ALTER TABLE users DROP COLUMN age;

-- Drop Table
DROP TABLE users;
```

---
## DML (Data Manipulation Language)
```sql
-- Insert Data
INSERT INTO users (name, email) VALUES ('John Doe', 'john@example.com');

-- Update Data
UPDATE users SET name = 'Jane Doe' WHERE id = 1;

-- Delete Data
DELETE FROM users WHERE id = 1;
```

---
## DQL (Data Query Language)
```sql
-- Select Data
SELECT * FROM users;
SELECT name, email FROM users WHERE id = 2;
SELECT COUNT(*) FROM users;
```

---
## TCL (Transaction Control Language)
```sql
-- Transactions
START TRANSACTION;
UPDATE users SET name = 'Alice' WHERE id = 3;
ROLLBACK; -- Undo the change
COMMIT; -- Save the change
```

---
## DCL (Data Control Language)
```sql
-- Grant Permissions
GRANT SELECT, INSERT ON users TO 'username'@'localhost';

-- Revoke Permissions
REVOKE INSERT ON users FROM 'username'@'localhost';
```

---
## Joins
```sql
-- INNER JOIN
SELECT users.name, orders.amount FROM users
INNER JOIN orders ON users.id = orders.user_id;

-- LEFT JOIN
SELECT users.name, orders.amount FROM users
LEFT JOIN orders ON users.id = orders.user_id;

-- RIGHT JOIN
SELECT users.name, orders.amount FROM users
RIGHT JOIN orders ON users.id = orders.user_id;

-- FULL JOIN (some databases support this)
SELECT users.name, orders.amount FROM users
FULL JOIN orders ON users.id = orders.user_id;
```

---
## Subqueries
```sql
-- Using a subquery in WHERE clause
SELECT name FROM users WHERE id IN (SELECT user_id FROM orders WHERE amount > 100);
```

---
## Indexes
```sql
-- Create an index
CREATE INDEX idx_users_email ON users(email);

-- Drop an index
DROP INDEX idx_users_email;
```

---
## Views
```sql
-- Create a view
CREATE VIEW user_orders AS
SELECT users.name, orders.amount FROM users
JOIN orders ON users.id = orders.user_id;

-- Use a view
SELECT * FROM user_orders;
```

---
## Stored Procedures
```sql
-- Create a stored procedure
DELIMITER //
CREATE PROCEDURE GetUsers()
BEGIN
    SELECT * FROM users;
END //
DELIMITER ;

-- Call the stored procedure
CALL GetUsers();
```

---
## Triggers
```sql
-- Create a trigger
CREATE TRIGGER before_user_insert
BEFORE INSERT ON users
FOR EACH ROW
SET NEW.created_at = NOW();
```

---
## Window Functions
```sql
-- Using ROW_NUMBER() function
SELECT name, email, ROW_NUMBER() OVER(PARTITION BY age ORDER BY created_at) AS row_num
FROM users;
```

---
## Common Table Expressions (CTE)
```sql
WITH user_cte AS (
    SELECT id, name FROM users WHERE created_at > '2023-01-01'
)
SELECT * FROM user_cte;
```

---
## Performance Optimization
- Use **indexes** on frequently searched columns.
- Avoid `SELECT *`; specify required columns.
- Use **EXPLAIN** to analyze queries.
- Normalize tables to reduce redundancy.
- Use **LIMIT** in queries with large datasets.

```sql
-- Analyze query performance
EXPLAIN SELECT * FROM users WHERE email = 'test@example.com';
```

---
## LIKE and Regex Search
```sql
-- Using LIKE for pattern matching
SELECT * FROM users WHERE name LIKE 'A%';  -- Names starting with 'A'
SELECT * FROM users WHERE email LIKE '%@gmail.com';  -- Emails ending in gmail.com
SELECT * FROM users WHERE name LIKE '_a%';  -- Names where second letter is 'a'

-- Searching with regex (MySQL example)
SELECT * FROM users WHERE name REGEXP '^A.*';  -- Names starting with 'A'
SELECT * FROM users WHERE email REGEXP 'gmail\.com$';  -- Emails ending in gmail.com
```

---
## \ud83d\udccc Conclusion
This SQL Cheat Sheet covers basic to advanced concepts. Use it as a quick reference guide for writing efficient SQL queries. \ud83d\ude80
