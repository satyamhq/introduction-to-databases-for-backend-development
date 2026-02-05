# ALTER TABLE Statement

## Overview

No table is ever static. Database developers are always restructuring tables—sometimes they need to add new columns, delete old ones, or edit the data they contain. You can complete many of these basic restructuring actions using SQL syntax.

## Learning Objectives

In this lesson, you'll learn how to:
- Alter a database table by adding and removing columns
- Modify the attributes of a database table
- Use various ALTER TABLE commands

## ALTER TABLE Syntax

### Basic Structure

```sql
ALTER TABLE table_name
action (column_definition);
```

### Syntax Breakdown

1. **ALTER TABLE** - Keywords to inform the database that a table's contents must be altered
2. **table_name** - Name of the table to be altered
3. **action** - What you want to do (ADD, DROP, MODIFY, etc.)
4. **column_definition** - Details of the column (name, data type, etc.)

## Important Prerequisites

Before you can begin altering tables, you must:

1. **Already have a database** on the server
2. **Already have a table** in your database
3. **Have data** that you can alter (optional, but recommended for learning)

### Example Setup

```sql
-- Make sure you have a database
CREATE DATABASE college;

-- Use the database
USE college;

-- Create a table with data
CREATE TABLE students (
    student_id INT,
    student_name VARCHAR(100),
    email VARCHAR(100)
);
```

## Example: Students Table

Throughout this lesson, we'll work with a **students** table in the **college** database.

**Initial table structure:**
- `student_id` - INT
- `student_name` - VARCHAR(100)
- `email` - VARCHAR(100)

## Adding Columns

### Syntax

```sql
ALTER TABLE table_name
ADD (
    column_name1 datatype(size),
    column_name2 datatype(size)
);
```

### Example: Add Three New Columns

Let's add three new columns: `age`, `nationality`, and `country`.

**Step 1: Write the ALTER TABLE command**
```sql
ALTER TABLE students
```

**Step 2: Use the ADD command**
```sql
ALTER TABLE students
ADD (
```

**Step 3: Define the columns**
```sql
ALTER TABLE students
ADD (
    age INT,
    country VARCHAR(50),
    nationality VARCHAR(255)
);
```

**Step 4: Execute the statement**

**Result:** The students table now has five columns:
- `student_id`
- `student_name`
- `email`
- `age` (new)
- `country` (new)
- `nationality` (new)

### Column Definitions Explained

```sql
age INT
```
- Holds data in **integer format** (whole numbers)

```sql
country VARCHAR(50)
```
- Holds **string data** (VARCHAR)
- **Character limit of 50**

```sql
nationality VARCHAR(255)
```
- Holds **string data** (VARCHAR)
- **Character limit of 255**

### Adding a Single Column

```sql
ALTER TABLE students
ADD phone_number VARCHAR(20);
```

## Dropping (Deleting) Columns

### Syntax

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

### Example: Remove the Nationality Column

Since `country` and `nationality` are very similar and will probably hold the same type of information, we can remove the `nationality` column.

**Step 1: Write the ALTER TABLE command**
```sql
ALTER TABLE students
```

**Step 2: Use the DROP COLUMN command**
```sql
ALTER TABLE students
DROP COLUMN nationality;
```

**Step 3: Execute the statement**

A notification message may appear requesting confirmation of deletion. Press OK to confirm.

**Result:** The `nationality` column has been dropped from the table.

### ⚠️ Warning

Dropping a column is **permanent**! All data in that column will be lost.

## Modifying Columns

### Syntax

Different database systems use different keywords:

**MySQL:**
```sql
ALTER TABLE table_name
MODIFY column_name new_datatype(new_size);
```

**PostgreSQL:**
```sql
ALTER TABLE table_name
ALTER COLUMN column_name TYPE new_datatype(new_size);
```

**SQL Server:**
```sql
ALTER TABLE table_name
ALTER COLUMN column_name new_datatype(new_size);
```

### Example: Change Country Column Character Limit

The `country` column currently has a limit of 50 characters. Let's change it to 100 characters.

**Step 1: Write the ALTER TABLE command**
```sql
ALTER TABLE students
```

**Step 2: Use the MODIFY command (MySQL)**
```sql
ALTER TABLE students
MODIFY country VARCHAR(100);
```

**Step 3: Execute the query**

**Result:** The `country` column's limit has been updated to 100 characters.

### PostgreSQL Equivalent

```sql
ALTER TABLE students
ALTER COLUMN country TYPE VARCHAR(100);
```

### SQL Server Equivalent

```sql
ALTER TABLE students
ALTER COLUMN country VARCHAR(100);
```

## Complete ALTER TABLE Operations

### 1. ADD Operations

#### Add Single Column
```sql
ALTER TABLE students
ADD date_of_birth DATE;
```

#### Add Multiple Columns
```sql
ALTER TABLE students
ADD (
    address VARCHAR(200),
    city VARCHAR(50),
    postal_code VARCHAR(10)
);
```

#### Add Column with Constraints
```sql
ALTER TABLE students
ADD enrollment_date DATE NOT NULL DEFAULT CURRENT_DATE;
```

### 2. DROP Operations

#### Drop Single Column
```sql
ALTER TABLE students
DROP COLUMN phone_number;
```

#### Drop Multiple Columns (MySQL)
```sql
ALTER TABLE students
DROP COLUMN address,
DROP COLUMN city,
DROP COLUMN postal_code;
```

### 3. MODIFY Operations

#### Change Data Type
```sql
-- MySQL
ALTER TABLE students
MODIFY age SMALLINT;

-- PostgreSQL
ALTER TABLE students
ALTER COLUMN age TYPE SMALLINT;
```

#### Change Column Size
```sql
-- MySQL
ALTER TABLE students
MODIFY email VARCHAR(150);

-- PostgreSQL
ALTER TABLE students
ALTER COLUMN email TYPE VARCHAR(150);
```

#### Add NOT NULL Constraint
```sql
-- MySQL
ALTER TABLE students
MODIFY student_name VARCHAR(100) NOT NULL;

-- PostgreSQL
ALTER TABLE students
ALTER COLUMN student_name SET NOT NULL;
```

### 4. RENAME Operations

#### Rename Column
```sql
-- MySQL
ALTER TABLE students
CHANGE old_column_name new_column_name datatype;

-- PostgreSQL
ALTER TABLE students
RENAME COLUMN old_column_name TO new_column_name;
```

**Example:**
```sql
-- MySQL
ALTER TABLE students
CHANGE student_name full_name VARCHAR(100);

-- PostgreSQL
ALTER TABLE students
RENAME COLUMN student_name TO full_name;
```

#### Rename Table
```sql
ALTER TABLE students
RENAME TO college_students;
```

## Practical Examples

### Example 1: Restructure Students Table

```sql
-- Initial table
CREATE TABLE students (
    student_id INT,
    name VARCHAR(50),
    email VARCHAR(50)
);

-- Add new columns
ALTER TABLE students
ADD (
    age INT,
    enrollment_date DATE,
    gpa DECIMAL(3, 2)
);

-- Modify email column to allow longer emails
ALTER TABLE students
MODIFY email VARCHAR(100);

-- Rename name column to full_name
ALTER TABLE students
CHANGE name full_name VARCHAR(100);

-- Drop age column (decided not to track it)
ALTER TABLE students
DROP COLUMN age;
```

### Example 2: Add Constraints to Existing Table

```sql
-- Add primary key
ALTER TABLE students
ADD PRIMARY KEY (student_id);

-- Add unique constraint to email
ALTER TABLE students
ADD UNIQUE (email);

-- Add check constraint
ALTER TABLE students
ADD CONSTRAINT check_gpa CHECK (gpa >= 0 AND gpa <= 4.0);
```

### Example 3: Expand Product Table

```sql
-- Original table
CREATE TABLE products (
    product_id INT,
    product_name VARCHAR(50),
    price DECIMAL(8, 2)
);

-- Add inventory tracking
ALTER TABLE products
ADD (
    quantity_in_stock INT DEFAULT 0,
    reorder_level INT DEFAULT 10,
    supplier_id INT
);

-- Increase product name length
ALTER TABLE products
MODIFY product_name VARCHAR(200);

-- Add category
ALTER TABLE products
ADD category VARCHAR(50);
```

## Best Practices

### 1. Backup Before Altering

```sql
-- Create a backup table before making changes
CREATE TABLE students_backup AS
SELECT * FROM students;

-- Now safely alter the original
ALTER TABLE students
ADD new_column VARCHAR(100);
```

### 2. Test on Development First

```sql
-- Test changes on development database
ALTER TABLE dev_students
ADD phone_number VARCHAR(20);

-- If successful, apply to production
ALTER TABLE prod_students
ADD phone_number VARCHAR(20);
```

### 3. Add Columns with Default Values

```sql
-- Better: Provide default for existing rows
ALTER TABLE students
ADD status VARCHAR(20) DEFAULT 'active';

-- Avoid: NULL for all existing rows
ALTER TABLE students
ADD status VARCHAR(20);
```

### 4. Be Careful with Data Loss

```sql
-- ⚠️ DANGER: This will lose data if column has more than 50 chars
ALTER TABLE students
MODIFY email VARCHAR(50);  -- Originally VARCHAR(100)

-- ✅ Better: Only reduce size if you've verified data fits
SELECT MAX(LENGTH(email)) FROM students;  -- Check first
-- If result is <= 50, then it's safe to reduce size
```

## Common Mistakes to Avoid

### 1. Forgetting to Check Data First

```sql
-- ❌ Wrong: Modify without checking
ALTER TABLE students
MODIFY age SMALLINT;  -- What if there are large values?

-- ✅ Correct: Check data first
SELECT MAX(age) FROM students;
-- If max age is < 32767, SMALLINT is safe
ALTER TABLE students
MODIFY age SMALLINT;
```

### 2. Dropping Columns Without Backup

```sql
-- ❌ Risky: No backup
ALTER TABLE students
DROP COLUMN nationality;

-- ✅ Better: Create backup first
CREATE TABLE students_backup AS SELECT * FROM students;
ALTER TABLE students
DROP COLUMN nationality;
```

### 3. Wrong Syntax for Your Database

```sql
-- ❌ Wrong: Using MySQL syntax in PostgreSQL
ALTER TABLE students
MODIFY email VARCHAR(150);  -- This is MySQL syntax

-- ✅ Correct: Use PostgreSQL syntax
ALTER TABLE students
ALTER COLUMN email TYPE VARCHAR(150);
```

### 4. Adding NOT NULL Without Defaults

```sql
-- ❌ Will fail if table has existing rows
ALTER TABLE students
ADD phone_number VARCHAR(20) NOT NULL;

-- ✅ Better: Provide default or make nullable first
ALTER TABLE students
ADD phone_number VARCHAR(20) DEFAULT 'N/A';
```

## Database-Specific Syntax Comparison

| Operation | MySQL | PostgreSQL | SQL Server |
|-----------|-------|------------|------------|
| **Modify column** | `MODIFY column` | `ALTER COLUMN column TYPE` | `ALTER COLUMN column` |
| **Rename column** | `CHANGE old new` | `RENAME COLUMN old TO new` | `sp_rename` |
| **Add multiple columns** | `ADD (col1, col2)` | `ADD col1, ADD col2` | `ADD col1, col2` |
| **Drop multiple columns** | `DROP col1, DROP col2` | `DROP col1, DROP col2` | `DROP COLUMN col1, col2` |

## Complete Workflow Example

```sql
-- Step 1: Create initial table
CREATE TABLE students (
    student_id INT,
    student_name VARCHAR(100),
    email VARCHAR(100)
);

-- Step 2: Add new columns
ALTER TABLE students
ADD (
    age INT,
    country VARCHAR(50),
    nationality VARCHAR(255)
);

-- Step 3: Verify changes
DESCRIBE students;  -- or SHOW COLUMNS FROM students;

-- Step 4: Drop unnecessary column
ALTER TABLE students
DROP COLUMN nationality;

-- Step 5: Modify column size
ALTER TABLE students
MODIFY country VARCHAR(100);

-- Step 6: Verify final structure
DESCRIBE students;
```

## Summary

You've learned how to alter and modify tables in a database using SQL syntax.

### Key Operations

1. **ADD columns** - Add new columns to existing tables
2. **DROP columns** - Remove columns from tables
3. **MODIFY columns** - Change data types and sizes

### Syntax Summary

```sql
-- Add columns
ALTER TABLE table_name
ADD column_name datatype(size);

-- Drop columns
ALTER TABLE table_name
DROP COLUMN column_name;

-- Modify columns (MySQL)
ALTER TABLE table_name
MODIFY column_name new_datatype(new_size);

-- Modify columns (PostgreSQL)
ALTER TABLE table_name
ALTER COLUMN column_name TYPE new_datatype(new_size);
```

### Remember

- Always **backup** before altering tables
- **Test** changes on development environment first
- **Check data** before reducing column sizes
- Use **appropriate syntax** for your database system
- **Document** your changes for future reference

**Well done!** You now know how to restructure and modify database tables using ALTER TABLE statements.
