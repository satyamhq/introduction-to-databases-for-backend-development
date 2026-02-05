# What Are Tables in Databases?

## Overview

Databases store and present data in a logical way through **tables**. Understanding how tables work is fundamental to working with databases effectively.

## What is a Database Table?

A **table** is made up of **rows** and **columns** which hold data. Tables are:

- Stored in a database
- A database can hold multiple tables
- Also known as **relations** because they relate to one another

### Conceptual Understanding

At a conceptual or logical level, a table is also known as:

- **Entity** (in general database terminology)
- **Object** (in Object-Oriented Databases - OODB)

An entity/object has **attributes** that are like columns or fields in a table.

**In essence:** Table = Entity = Object (all refer to the same concept)

## Structure of a Database Table

### Visual Representation

```
Employee Table
┌─────┬───────────┬──────────┬─────────────┐
│ ID  │ Name      │ Role     │ Department  │  ← Columns/Fields/Attributes
├─────┼───────────┼──────────┼─────────────┤
│ 1   │ John Doe  │ Engineer │ IT          │  ← Row/Record
│ 2   │ Jane Smith│ Manager  │ Sales       │  ← Row/Record
│ 3   │ Bob Lee   │ Engineer │ IT          │  ← Row/Record
└─────┴───────────┴──────────┴─────────────┘
     ↑           ↑          ↑
    Primary    Data       Data
     Key
```

## Columns (Fields/Attributes)

### What Are Columns?

Within every table are **columns**, also called:
- **Fields**
- **Attributes**

### Column Characteristics

Each column or field has:
- A **unique name**
- A **data type**

### Example: Employee Table

| Column Name | Data Type | Purpose |
|-------------|-----------|---------|
| ID | Integer | Unique identifier |
| Name | String/VARCHAR | Employee name |
| Role | String/VARCHAR | Job title |
| Department | String/VARCHAR | Work department |

**Key Point:** Each column can hold different types of data (numeric, string, date, etc.)

## Rows (Records)

### What Are Rows?

A set of columns or fields forms a **row**. In relational database terminology, a row is known as a **record**.

### Definition

A **record** is a combination of columns or fields that contain data.

### Example

In the Employee table, each row represents a **single employee record**:

```sql
Row 1: ID=1, Name='John Doe', Role='Engineer', Department='IT'
Row 2: ID=2, Name='Jane Smith', Role='Manager', Department='Sales'
```

## Data Types

### What Are Data Types?

The **data type** of a column defines what type of value a column can hold.

### Common Data Types

| Category | Data Type | Examples | Usage |
|----------|-----------|----------|-------|
| **String** | VARCHAR, CHAR, TEXT | 'John', 'Hello' | Store characters and strings |
| **Numeric** | INT, DECIMAL, FLOAT | 123, 45.67 | Store exact or approximate numbers |
| **Date/Time** | DATE, TIME, DATETIME | '2024-01-15', '14:30:00' | Store date and time information |
| **Binary** | BLOB, BINARY | Images, files | Store files and binary data |

### Purpose of Data Types

1. **Developer Decision:** It's up to the developer to decide the data type for each column
2. **Guideline for SQL:** Data types tell SQL:
   - What type of data to expect in each column
   - How to interact with the stored data physically

### Important Note

**Data types can vary depending on the database system!**

Different systems may have different type names:
- MySQL
- SQL Server
- PostgreSQL
- Oracle
- Microsoft Access

**Always refer to the documentation** of your specific database system to check what data types it supports.

## Domains

### What is a Domain?

A **domain** is the set of legal values that can be assigned to an attribute.

### Purpose

Domains ensure that the values a field can hold are well-defined and valid.

### Domain Rules

| Domain Type | Allowed Values | Rules |
|-------------|----------------|-------|
| **Numeric** | Numbers only | Must include length, precision, range |
| **String** | Characters only | Must define maximum length |
| **Date** | Valid dates only | Must follow date format |

### Examples

```sql
-- Numeric domain
Age INT(3)  -- Can only hold integers up to 3 digits (0-999)

-- String domain
Name VARCHAR(50)  -- Can only hold strings up to 50 characters

-- Date domain
BirthDate DATE  -- Can only hold valid dates
```

### Domain Components

Each domain must include:
- **Length values** (maximum size)
- **Type constraints** (what kind of data)
- **Other relevant rules** (range, format, etc.)

## Primary Keys

### What is a Primary Key?

A **primary key** is a column (or combination of columns) that uniquely identifies each row/record in a table.

### Characteristics

- Contains **unique values** only
- **Cannot be NULL**
- Each table should have one primary key
- Uniquely identifies each record

### Example: Employee Table

```sql
CREATE TABLE Employee (
    ID INT PRIMARY KEY,        -- Primary Key
    Name VARCHAR(50),
    Role VARCHAR(50),
    Department VARCHAR(50)
);
```

**Why ID is the Primary Key:**
- Each ID is unique (no duplicates)
- Other columns could have repeating values:
  - Two employees may have the same name
  - Multiple employees may have the same role
  - Several employees may be in the same department

### Composite Primary Keys

It's possible for a primary key to be a **combination of columns** if a single column doesn't have unique values.

**Example: Student Enrollment Table**

```sql
CREATE TABLE Enrollment (
    StudentID INT,
    CourseID INT,
    EnrollmentDate DATE,
    PRIMARY KEY (StudentID, CourseID)  -- Composite Primary Key
);
```

A student can enroll in multiple courses, and a course can have multiple students, but the combination of StudentID and CourseID is unique.

## Key Terminology Summary

| Term | Also Known As | Definition |
|------|---------------|------------|
| **Table** | Relation, Entity, Object | Structure that holds data in rows and columns |
| **Column** | Field, Attribute | Vertical division that holds specific type of data |
| **Row** | Record, Tuple | Horizontal division representing one complete entry |
| **Data Type** | Type | Defines what kind of data a column can store |
| **Domain** | Value Set | Legal values that can be assigned to an attribute |
| **Primary Key** | Unique Identifier | Column(s) that uniquely identify each record |

## Complete Example: Employee Database

### Table Structure

```sql
CREATE TABLE Employee (
    ID INT PRIMARY KEY,              -- Unique identifier
    FirstName VARCHAR(50) NOT NULL,  -- String data
    LastName VARCHAR(50) NOT NULL,   -- String data
    Role VARCHAR(50),                -- String data
    Department VARCHAR(50),          -- String data
    Salary DECIMAL(10, 2),          -- Numeric data (money)
    HireDate DATE,                   -- Date data
    Photo BLOB                       -- Binary data (image)
);
```

### Sample Data

| ID (PK) | FirstName | LastName | Role | Department | Salary | HireDate |
|---------|-----------|----------|------|------------|--------|----------|
| 1 | John | Doe | Engineer | IT | 75000.00 | 2020-01-15 |
| 2 | Jane | Smith | Manager | Sales | 85000.00 | 2019-06-20 |
| 3 | Bob | Lee | Engineer | IT | 72000.00 | 2021-03-10 |

### Analysis

- **3 records (rows)** - Each representing one employee
- **7 columns** - ID, FirstName, LastName, Role, Department, Salary, HireDate
- **Primary Key** - ID (unique for each employee)
- **Data Types** - INT, VARCHAR, DECIMAL, DATE
- **Domain Examples**:
  - ID: Positive integers only
  - FirstName/LastName: Strings up to 50 characters
  - Salary: Numbers with 2 decimal places
  - HireDate: Valid dates only

## Best Practices for Database Tables

### 1. Choose Appropriate Data Types
```sql
-- ✅ GOOD: Specific and appropriate
Age INT(3)
Email VARCHAR(100)
Price DECIMAL(10, 2)

-- ❌ BAD: Too generic or oversized
Age VARCHAR(255)
Email TEXT
```

### 2. Always Define a Primary Key
```sql
-- ✅ GOOD
CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(100)
);

-- ❌ BAD: No primary key
CREATE TABLE Student (
    Name VARCHAR(100),
    Age INT
);
```

### 3. Use Meaningful Column Names
```sql
-- ✅ GOOD: Clear and descriptive
CustomerFirstName, OrderDate, TotalAmount

-- ❌ BAD: Vague or cryptic
Name1, D1, Amt
```

### 4. Set Appropriate Constraints
```sql
CREATE TABLE Product (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(100) NOT NULL,  -- Cannot be empty
    Price DECIMAL(10, 2) CHECK (Price > 0),  -- Must be positive
    Stock INT DEFAULT 0  -- Default value
);
```

## Summary

You should now be familiar with:

### What a Database Table Is
- A structure made up of rows and columns
- Stores related data in an organized way
- Also known as relations, entities, or objects

### How Data is Structured
- **Columns** (fields/attributes): Vertical divisions with unique names and data types
- **Rows** (records): Horizontal divisions representing complete entries
- **Data Types**: Define what kind of values can be stored
- **Domains**: Define legal values for attributes
- **Primary Keys**: Uniquely identify each record

### Key Concepts
- Tables organize data logically
- Each column has a specific data type
- Each row represents a single record
- Primary keys ensure uniqueness
- Domains enforce data validity

**Great work!** You now understand the fundamental structure of database tables and how they organize and store data.
