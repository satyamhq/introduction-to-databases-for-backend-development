# SQL Syntax Introduction

## Overview

To interact with databases using SQL, you need experience with SQL syntax and its subsets. This lesson covers the fundamental SQL syntax and demonstrates how to use the three main subsets of SQL to create, manipulate, and query data.

## SQL Subsets Overview

SQL has several subsets, each serving a specific purpose:

| Subset | Full Name | Purpose |
|--------|-----------|---------|
| **DDL** | Data Definition Language | Create and modify database structure |
| **DML** | Data Manipulation Language | Populate and modify data |
| **DQL** | Data Query Language | Read and query data |

## Example: College Database

Throughout this lesson, we'll build a college database to demonstrate SQL commands. This demonstration provides a working familiarity with SQL—you'll explore these concepts in more depth later in the program.

## 1. DDL - Data Definition Language

DDL is used to create and modify the structure of databases and tables.

### Creating a Database

**Syntax:**
```sql
CREATE DATABASE database_name;
```

**Example: Create College Database**
```sql
CREATE DATABASE college;
```

### Creating Tables

**Syntax:**
```sql
CREATE TABLE table_name;
```

**Example: Create Student Table**
```sql
CREATE TABLE student (
    ID INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    date_of_birth DATE
);
```

**Key Points:**
- Use `CREATE DATABASE` followed by the database name
- Use `CREATE TABLE` followed by the table name
- End each statement with a semicolon (`;`)
- Repeat the same steps for each new table you want to add

## 2. DML - Data Manipulation Language

DML is used to populate and modify data within tables.

### Inserting Data (INSERT)

**Syntax:**
```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

**Example: Add Student Data**
```sql
INSERT INTO student (ID, first_name, last_name, date_of_birth)
VALUES (1, 'John', 'Murphy', '2000-05-15');
```

**Steps:**
1. Type `INSERT INTO` followed by the table name
2. List the required columns within parentheses
3. Add the `VALUES` keyword
4. Specify values for each field in the same order as the columns

### Updating Data (UPDATE)

**Syntax:**
```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

**Example: Update Student Date of Birth**
```sql
UPDATE student
SET date_of_birth = '2000-06-20'
WHERE ID = 2;
```

**Steps:**
1. Add the `UPDATE` keyword followed by the table name
2. Use the `SET` keyword followed by column-value pairings
3. Add the `WHERE` clause with a condition to filter records

**Important:** Always use a `WHERE` clause to avoid updating all records in the table!

### Deleting Data (DELETE)

**Syntax:**
```sql
DELETE FROM table_name
WHERE condition;
```

**Example: Delete Student with ID 3**
```sql
DELETE FROM student
WHERE ID = 3;
```

**Steps:**
1. Type `DELETE FROM` followed by the table name
2. Add the `WHERE` clause with a condition (e.g., `ID = 3`)
3. This removes all data matching the condition

**Warning:** Without a `WHERE` clause, all records in the table will be deleted!

## 3. DQL - Data Query Language

DQL is used to read and query data from database tables.

### Selecting Data (SELECT)

**Syntax:**
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

**Example: Find Student Name by ID**
```sql
SELECT first_name, last_name
FROM student
WHERE ID = 1;
```

**Result:**
```
first_name | last_name
-----------|----------
John       | Murphy
```

**Steps:**
1. Write the `SELECT` keyword followed by the columns you need
2. Use the `FROM` keyword followed by the table name
3. Optionally add the `WHERE` keyword with a condition to filter results

### Selecting All Columns

**Syntax:**
```sql
SELECT * FROM table_name;
```

**Example: Get All Student Data**
```sql
SELECT * FROM student;
```

The asterisk (`*`) selects all columns from the table.

## Complete Example: College Database Workflow

### Step 1: Create Database
```sql
CREATE DATABASE college;
```

### Step 2: Create Table
```sql
CREATE TABLE student (
    ID INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    date_of_birth DATE
);
```

### Step 3: Insert Data
```sql
INSERT INTO student (ID, first_name, last_name, date_of_birth)
VALUES (1, 'John', 'Murphy', '2000-05-15');

INSERT INTO student (ID, first_name, last_name, date_of_birth)
VALUES (2, 'Jane', 'Smith', '1999-08-22');

INSERT INTO student (ID, first_name, last_name, date_of_birth)
VALUES (3, 'Bob', 'Johnson', '2001-03-10');
```

### Step 4: Query Data
```sql
SELECT * FROM student;
```

### Step 5: Update Data
```sql
UPDATE student
SET date_of_birth = '2000-06-20'
WHERE ID = 2;
```

### Step 6: Delete Data
```sql
DELETE FROM student
WHERE ID = 3;
```

### Step 7: Query Updated Data
```sql
SELECT first_name, last_name
FROM student
WHERE ID = 1;
```

## SQL Syntax Cheat Sheet

### DDL Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `CREATE DATABASE` | Create a new database | `CREATE DATABASE college;` |
| `CREATE TABLE` | Create a new table | `CREATE TABLE student (...);` |
| `ALTER TABLE` | Modify existing table | `ALTER TABLE student ADD email VARCHAR(100);` |
| `DROP TABLE` | Delete a table | `DROP TABLE student;` |

### DML Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `INSERT INTO` | Add new data | `INSERT INTO student VALUES (...);` |
| `UPDATE` | Modify existing data | `UPDATE student SET ... WHERE ...;` |
| `DELETE FROM` | Remove data | `DELETE FROM student WHERE ...;` |

### DQL Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `SELECT` | Retrieve data | `SELECT * FROM student;` |
| `WHERE` | Filter results | `SELECT * FROM student WHERE ID = 1;` |

## Important SQL Keywords

| Keyword | Purpose |
|---------|---------|
| `CREATE` | Create database objects |
| `INSERT` | Add new records |
| `UPDATE` | Modify existing records |
| `DELETE` | Remove records |
| `SELECT` | Retrieve data |
| `FROM` | Specify table |
| `WHERE` | Filter conditions |
| `SET` | Specify new values |
| `VALUES` | Provide data values |

## Best Practices

### 1. Always Use WHERE Clauses
```sql
-- ✅ GOOD: Updates specific record
UPDATE student SET date_of_birth = '2000-06-20' WHERE ID = 2;

-- ❌ BAD: Updates ALL records
UPDATE student SET date_of_birth = '2000-06-20';
```

### 2. End Statements with Semicolons
```sql
CREATE DATABASE college;
SELECT * FROM student;
```

### 3. Use Clear Column Names
```sql
-- ✅ GOOD
SELECT first_name, last_name FROM student;

-- ⚠️ Less clear
SELECT * FROM student;
```

### 4. Format for Readability
```sql
-- Well formatted
SELECT first_name, last_name
FROM student
WHERE ID = 1;

-- Less readable
SELECT first_name, last_name FROM student WHERE ID = 1;
```

## Common Pitfalls to Avoid

❌ **Forgetting WHERE clause** - Can update/delete all records  
❌ **Missing semicolon** - Statement won't execute  
❌ **Wrong column names** - Errors or unexpected results  
❌ **Incorrect data types** - Data won't insert properly  
❌ **Case sensitivity** - Depends on database system  

## Summary

You're now familiar with the basics of SQL syntax and its subsets:

### DDL (Data Definition Language)
- **CREATE DATABASE** - Create databases
- **CREATE TABLE** - Create tables
- Used for defining database structure

### DML (Data Manipulation Language)
- **INSERT INTO** - Add new data
- **UPDATE** - Modify existing data
- **DELETE FROM** - Remove data
- Used for manipulating data within tables

### DQL (Data Query Language)
- **SELECT** - Retrieve data from databases
- **WHERE** - Filter query results
- Used for reading and querying data

Don't worry if you're still trying to figure out these subsets—you'll explore each of them in more depth later in this specialization, and you'll get opportunities to practice them yourself.

**Key Takeaway:** SQL provides a simple, standardized way to create databases, populate them with data, modify that data, and query information whenever you need it.
