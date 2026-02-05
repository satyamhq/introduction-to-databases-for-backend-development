# SQL Usage

## Scenario: College Database

Imagine you've just been hired to create a database for a college. Your tasks include:

1. **Create tables** to hold data for all aspects of the college
2. **Insert data** into these tables
3. **Modify data** whenever something changes

That's a lot of work! But it's all possible with the use of **SQL and CRUD operations**.

## CRUD Operations

Performing CRUD operations is the **most common task** when working with databases.

### What is CRUD?

**CRUD** stands for:

- **C**reate - Add or insert data
- **R**ead - Retrieve data
- **U**pdate - Modify existing data
- **D**elete - Remove data

These operations form the foundation of database management.

## SQL Subsets (Sub-Languages)

SQL can be divided into many subsections or **sub-languages**, depending on what it's used for:

1. **DDL** - Data Definition Language
2. **DML** - Data Manipulation Language
3. **DQL** - Data Query Language
4. **DCL** - Data Control Language

Let's explore each one in detail.

## 1. Data Definition Language (DDL)

### Purpose

DDL helps you **define data** in your database.

**What does it mean to define data?**
Before you can store data, you need to create the database and related objects (like tables) where your data will be stored.

### DDL Commands

#### CREATE
Create database objects (databases, tables, etc.)

```sql
CREATE DATABASE college;

CREATE TABLE students (
    student_id INT,
    name VARCHAR(100),
    email VARCHAR(100)
);
```

**Use case:** Creating a new database or table

#### ALTER
Modify existing database objects

```sql
ALTER TABLE students
ADD COLUMN phone VARCHAR(15);
```

**Use case:** Adding a new column to a table, changing data types

#### DROP
Remove database objects

```sql
DROP TABLE students;
```

**Use case:** Deleting a table or database

### DDL Summary

| Command | Purpose | Example |
|---------|---------|---------|
| **CREATE** | Create new objects | `CREATE TABLE students` |
| **ALTER** | Modify existing objects | `ALTER TABLE students ADD COLUMN` |
| **DROP** | Remove objects | `DROP TABLE students` |

## 2. Data Manipulation Language (DML)

### Purpose

DML commands are used to **manipulate data** in the database.

**Note:** Most CRUD operations fall under DML.

### DML Commands

#### INSERT
Add data to a table

```sql
INSERT INTO students (student_id, name, email)
VALUES (1, 'John Doe', 'john@email.com');
```

**Use case:** Adding new records

#### UPDATE
Edit data that's already in a table

```sql
UPDATE students
SET email = 'newemail@email.com'
WHERE student_id = 1;
```

**Use case:** Modifying existing records

#### DELETE
Remove data from a table

```sql
DELETE FROM students
WHERE student_id = 1;
```

**Use case:** Removing specific records

### DML Summary

| Command | Purpose | Example |
|---------|---------|---------|
| **INSERT** | Add new data | `INSERT INTO students VALUES` |
| **UPDATE** | Modify existing data | `UPDATE students SET` |
| **DELETE** | Remove data | `DELETE FROM students WHERE` |

## 3. Data Query Language (DQL)

### Purpose

DQL is used to **read or retrieve data** from the database.

### DQL Command

#### SELECT
Retrieve data from one or multiple tables

```sql
SELECT * FROM students;
```

**Basic retrieval:**
```sql
SELECT name, email FROM students;
```

**With filter criteria:**
```sql
SELECT * FROM students
WHERE student_id = 1;
```

**From multiple tables:**
```sql
SELECT students.name, courses.course_name
FROM students
JOIN enrollments ON students.student_id = enrollments.student_id
JOIN courses ON enrollments.course_id = courses.course_id;
```

### DQL Features

- Retrieve data from one or multiple tables
- Specify which fields to retrieve
- Apply filter criteria
- Sort and group results
- Join related tables

### DQL Summary

| Command | Purpose | Example |
|---------|---------|---------|
| **SELECT** | Retrieve data | `SELECT * FROM students` |

## 4. Data Control Language (DCL)

### Purpose

DCL is used to **control access** to the database.

### DCL Commands

#### GRANT
Give users access privileges to data

```sql
GRANT SELECT, INSERT ON students TO user_name;
```

**Use case:** Allowing a user to read and add data

#### REVOKE
Remove access privileges from users

```sql
REVOKE INSERT ON students FROM user_name;
```

**Use case:** Removing a user's permission to add data

### DCL Summary

| Command | Purpose | Example |
|---------|---------|---------|
| **GRANT** | Give access privileges | `GRANT SELECT ON students` |
| **REVOKE** | Remove access privileges | `REVOKE INSERT ON students` |

## Complete SQL Sub-Languages Overview

### Visual Breakdown

```
SQL
├── DDL (Data Definition Language)
│   ├── CREATE
│   ├── ALTER
│   └── DROP
│
├── DML (Data Manipulation Language)
│   ├── INSERT
│   ├── UPDATE
│   └── DELETE
│
├── DQL (Data Query Language)
│   └── SELECT
│
└── DCL (Data Control Language)
    ├── GRANT
    └── REVOKE
```

## College Database Example

### Step 1: Create the Database (DDL)

```sql
CREATE DATABASE college;

CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100)
);

CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(100)
);
```

### Step 2: Insert Data (DML)

```sql
INSERT INTO students (student_id, name, email)
VALUES (1, 'Alice Johnson', 'alice@college.edu');

INSERT INTO courses (course_id, course_name)
VALUES (101, 'Database Systems');
```

### Step 3: Read Data (DQL)

```sql
SELECT * FROM students;

SELECT name, email FROM students
WHERE student_id = 1;
```

### Step 4: Update Data (DML)

```sql
UPDATE students
SET email = 'alice.j@college.edu'
WHERE student_id = 1;
```

### Step 5: Delete Data (DML)

```sql
DELETE FROM students
WHERE student_id = 1;
```

### Step 6: Control Access (DCL)

```sql
GRANT SELECT ON students TO professor;

REVOKE SELECT ON students FROM professor;
```

## SQL as an Interface

SQL acts as the **interface between the database and its users**.

### The Workflow

```
User
  ↓
SQL Commands
  ↓
DBMS
  ↓
Database
  ↓
Results
  ↓
User
```

## Summary Table

| Category | Acronym | Purpose | Main Commands |
|----------|---------|---------|---------------|
| **Data Definition Language** | DDL | Define database structure | CREATE, ALTER, DROP |
| **Data Manipulation Language** | DML | Manipulate data | INSERT, UPDATE, DELETE |
| **Data Query Language** | DQL | Retrieve data | SELECT |
| **Data Control Language** | DCL | Control access | GRANT, REVOKE |

## CRUD Mapping to SQL

| CRUD Operation | SQL Command | SQL Sub-Language |
|----------------|-------------|------------------|
| **Create** | INSERT | DML |
| **Read** | SELECT | DQL |
| **Update** | UPDATE | DML |
| **Delete** | DELETE | DML |

## Key Takeaways

### What SQL Can Do

1. **Define** database structures (DDL)
2. **Manipulate** data (DML)
3. **Query** data (DQL)
4. **Control** access (DCL)

### Why It Matters

- **Comprehensive:** Handles all database operations
- **Standardized:** Consistent across database systems
- **Powerful:** Enables complex data management
- **Essential:** Required skill for database work

### Most Common Operations

**DDL:**
- Creating and modifying tables
- Database structure management

**DML:**
- Day-to-day data operations
- CRUD functionality

**DQL:**
- Data retrieval
- Reporting and analysis

**DCL:**
- Security and access control
- User permission management

## Practice Exercise

Try creating your own college database:

1. **CREATE** a students table
2. **INSERT** student records
3. **SELECT** all students
4. **UPDATE** a student's email
5. **DELETE** a student record
6. **GRANT** access to another user

## Conclusion

SQL provides a complete toolkit for database management through its sub-languages:

- **DDL** defines structure
- **DML** manipulates data
- **DQL** retrieves information
- **DCL** controls access

Together, these sub-languages enable you to build, manage, and secure databases effectively. SQL truly acts as the interface between databases and their users, making data management accessible and powerful!
