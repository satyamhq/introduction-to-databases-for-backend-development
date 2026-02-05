# Common SQL Commands

## Overview

SQL (Structured Query Language) is the most widely used database query language. It is designed for retrieving and managing data in relational databases. SQL can perform different types of operations including:

- Accessing data
- Describing data
- Manipulating data
- Setting user roles and privileges (permissions)

## SQL Command Categories

SQL commands are grouped into **four main categories** based on their functionality:

| Category | Abbreviation | Purpose |
|----------|--------------|---------|
| Data Definition Language | **DDL** | Define, delete, and modify database structure |
| Data Query Language | **DQL** | Query and retrieve data |
| Data Manipulation Language | **DML** | Query, delete, and update data |
| Data Control Language | **DCL** | Manage user rights and permissions |
| Transaction Control Language | **TCL** | Manage database transactions |

Let's explore each category in detail.

---

## 1. DDL - Data Definition Language

DDL provides commands for **defining, deleting, and modifying** tables in a database.

### CREATE Command

**Purpose:** Create the database or tables inside the database

**Syntax to create a table:**
```sql
CREATE TABLE table_name (
    column_name1 datatype(size), 
    column_name2 datatype(size), 
    column_name3 datatype(size)
);
```

**Example:**
```sql
CREATE TABLE students (
    id INT(10),
    name VARCHAR(50),
    age INT(3)
);
```

### DROP Command

**Purpose:** Delete a database or a table inside the database

**Syntax to drop a table:**
```sql
DROP TABLE table_name;
```

**Example:**
```sql
DROP TABLE students;
```

**Warning:** This command permanently deletes the table and all its data!

### ALTER Command

**Purpose:** Change the structure of tables in the database (e.g., change table name, add primary key, add/delete columns)

**Syntax to add a column:**
```sql
ALTER TABLE table_name ADD (column_name datatype(size));
```

**Syntax to add a primary key:**
```sql
ALTER TABLE table_name ADD PRIMARY KEY (column_name);
```

**Examples:**
```sql
-- Add a new column
ALTER TABLE students ADD (email VARCHAR(100));

-- Add a primary key
ALTER TABLE students ADD PRIMARY KEY (id);
```

### TRUNCATE Command

**Purpose:** Remove all records from a table (empties the table but doesn't delete the table itself)

**Syntax:**
```sql
TRUNCATE TABLE table_name;
```

**Example:**
```sql
TRUNCATE TABLE students;
```

**Note:** Unlike DROP, TRUNCATE keeps the table structure intact—only the data is removed.

### COMMENT Command

**Purpose:** Add comments to explain or document SQL statements

**Syntax:**
```sql
-- Comment text here
SELECT * FROM table_name;
```

**Example:**
```sql
-- Retrieve all student data
SELECT * FROM students;

-- This is a comment and won't be executed
```

**Key Points:**
- Use double dash (`--`) at the start of the line
- Any text after `--` will not be executed as part of the SQL statement
- Comments are for documentation only, not for building the database

---

## 2. DQL - Data Query Language

DQL provides the ability to **query and retrieve** data from the database.

### SELECT Command

**Purpose:** Retrieve data from tables in the database

**Syntax to select all data:**
```sql
SELECT * FROM table_name;
```

**Syntax to select specific columns:**
```sql
SELECT column1, column2 FROM table_name;
```

**Examples:**
```sql
-- Select all columns
SELECT * FROM students;

-- Select specific columns
SELECT name, age FROM students;

-- Select with condition
SELECT * FROM students WHERE age > 18;
```

---

## 3. DML - Data Manipulation Language

DML provides the ability to **query, delete, and update** data in the database.

### INSERT Command

**Purpose:** Add records of data into an existing table

**Syntax:**
```sql
INSERT INTO table_name (column1, column2, column3) 
VALUES (value1, value2, value3);
```

**Example:**
```sql
INSERT INTO students (id, name, age) 
VALUES (1, 'John Doe', 20);
```

**Multiple inserts:**
```sql
INSERT INTO students (id, name, age) VALUES 
(1, 'John Doe', 20),
(2, 'Jane Smith', 22),
(3, 'Bob Johnson', 19);
```

### UPDATE Command

**Purpose:** Modify or update data contained within a table

**Syntax:**
```sql
UPDATE table_name 
SET column1 = value1, column2 = value2 
WHERE condition;
```

**Example:**
```sql
UPDATE students 
SET age = 21, name = 'John Smith' 
WHERE id = 1;
```

**Warning:** Always use a WHERE clause! Without it, all records will be updated.

### DELETE Command

**Purpose:** Delete data from a table in the database

**Syntax:**
```sql
DELETE FROM table_name WHERE condition;
```

**Example:**
```sql
DELETE FROM students WHERE id = 3;
```

**Warning:** Without a WHERE clause, all records in the table will be deleted!

---

## 4. DCL - Data Control Language

DCL deals with the **rights and permissions** of users in a database system. This category handles advanced functions for managing user privileges.

### GRANT Command

**Purpose:** Provide users with the privileges required to access and manipulate the database

**Generic Syntax:**
```sql
GRANT privilege_type ON database_object TO user_name;
```

**Example:**
```sql
GRANT SELECT, INSERT ON students TO user1;
```

### REVOKE Command

**Purpose:** Remove permissions from any user

**Generic Syntax:**
```sql
REVOKE privilege_type ON database_object FROM user_name;
```

**Example:**
```sql
REVOKE INSERT ON students FROM user1;
```

**Note:** DCL deals with advanced operations in the database and requires administrative privileges.

---

## 5. TCL - Transaction Control Language

TCL commands manage **transactions** in the database. They manage changes made to data and allow SQL statements to be grouped into logical transactions.

### COMMIT Command

**Purpose:** Save all work you have already done in the database

**Syntax:**
```sql
COMMIT;
```

**Example:**
```sql
UPDATE students SET age = 21 WHERE id = 1;
COMMIT; -- Saves the changes permanently
```

### ROLLBACK Command

**Purpose:** Restore a database to the last committed state

**Syntax:**
```sql
ROLLBACK;
```

**Example:**
```sql
UPDATE students SET age = 21 WHERE id = 1;
ROLLBACK; -- Undoes the changes since last COMMIT
```

**Note:** TCL deals with advanced operations and is crucial for maintaining data integrity during transactions.

---

## SQL Commands Summary Table

### DDL Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `CREATE` | Create database or table | `CREATE TABLE students (...);` |
| `DROP` | Delete database or table | `DROP TABLE students;` |
| `ALTER` | Modify table structure | `ALTER TABLE students ADD email VARCHAR(100);` |
| `TRUNCATE` | Remove all records from table | `TRUNCATE TABLE students;` |
| `COMMENT` | Add documentation | `-- This is a comment` |

### DQL Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `SELECT` | Retrieve data | `SELECT * FROM students;` |

### DML Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `INSERT` | Add new records | `INSERT INTO students VALUES (...);` |
| `UPDATE` | Modify existing records | `UPDATE students SET age = 21 WHERE id = 1;` |
| `DELETE` | Remove records | `DELETE FROM students WHERE id = 3;` |

### DCL Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `GRANT` | Give user privileges | `GRANT SELECT ON students TO user1;` |
| `REVOKE` | Remove user privileges | `REVOKE SELECT ON students FROM user1;` |

### TCL Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `COMMIT` | Save changes permanently | `COMMIT;` |
| `ROLLBACK` | Undo changes since last commit | `ROLLBACK;` |

---

## Command Category Quick Reference

```
DDL (Structure)          DQL (Read)           DML (Data)
├── CREATE              └── SELECT           ├── INSERT
├── DROP                                     ├── UPDATE
├── ALTER                                    └── DELETE
├── TRUNCATE
└── COMMENT

DCL (Permissions)        TCL (Transactions)
├── GRANT               ├── COMMIT
└── REVOKE              └── ROLLBACK
```

---

## Best Practices

### 1. Always Use WHERE Clauses with UPDATE and DELETE
```sql
-- ✅ GOOD
DELETE FROM students WHERE id = 3;

-- ❌ DANGEROUS (deletes everything!)
DELETE FROM students;
```

### 2. Test SELECT Before DELETE or UPDATE
```sql
-- First, check what you're about to delete
SELECT * FROM students WHERE age < 18;

-- Then delete if correct
DELETE FROM students WHERE age < 18;
```

### 3. Use COMMIT and ROLLBACK for Important Changes
```sql
-- Start transaction
UPDATE students SET age = age + 1;

-- Check if correct
SELECT * FROM students;

-- If correct, commit; if wrong, rollback
COMMIT; -- or ROLLBACK;
```

### 4. Add Comments for Complex Queries
```sql
-- Calculate average age of students by department
SELECT department, AVG(age) as average_age
FROM students
GROUP BY department;
```

---

## Key Differences

### DROP vs TRUNCATE vs DELETE

| Aspect | DROP | TRUNCATE | DELETE |
|--------|------|----------|--------|
| **Removes** | Entire table | All rows | Specific rows |
| **Structure** | Deleted | Kept | Kept |
| **WHERE clause** | Not applicable | Not applicable | Supported |
| **Rollback** | No | No (usually) | Yes |
| **Speed** | Fast | Fast | Slower |

**Example:**
```sql
DROP TABLE students;        -- Table is gone completely
TRUNCATE TABLE students;    -- Table exists but empty
DELETE FROM students;       -- Same result as TRUNCATE but slower
DELETE FROM students WHERE age < 18;  -- Only specific rows deleted
```

---

## Summary

You've learned about the main SQL commands grouped into five categories:

1. **DDL** - Defines database structure (CREATE, DROP, ALTER, TRUNCATE)
2. **DQL** - Queries data (SELECT)
3. **DML** - Manipulates data (INSERT, UPDATE, DELETE)
4. **DCL** - Controls user permissions (GRANT, REVOKE)
5. **TCL** - Manages transactions (COMMIT, ROLLBACK)

At later stages, you'll explore relevant examples and detailed explanations of SQL syntax for key operations such as creating, inserting, updating, and deleting data in databases.

**Remember:** Understanding these command categories and their purposes is fundamental to working effectively with SQL databases.
