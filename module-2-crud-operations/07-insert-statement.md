# INSERT Statement

## Overview

When working with databases, you'll often have to add new rows and columns to existing tables or create new tables from scratch. For example, if you run a college database, you'll have to add new rows for every new student. With SQL, you can perform these tasks quickly using the **INSERT** statement.

## Learning Objectives

By the end of this lesson, you'll be able to:
- Identify and understand INSERT SQL syntax
- Insert data into tables using the INSERT INTO clause
- Insert single and multiple records at once

## INSERT INTO Syntax

### Basic Structure

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

### Syntax Breakdown

1. **INSERT INTO** - Clause that starts the insert operation
2. **table_name** - Name of the table to insert data into
3. **(column1, column2, ...)** - List of columns (within parentheses, separated by commas)
4. **VALUES** - Keyword indicating the values to insert
5. **(value1, value2, ...)** - List of values (within parentheses, separated by commas)

### Important Rules

- Each value **corresponds to a specific column**
- Values must **reflect the same datatype** as their columns
- Values must be in the **same order** as the columns
- **Non-numeric values** must be placed within quotation marks

## Inserting a Single Row

### Example: Sports Club Players Table

Let's insert new player data into a `players` table from a sports club database.

**Step 1: Write INSERT INTO command**
```sql
INSERT INTO players
```

**Step 2: Specify column names**
```sql
INSERT INTO players (ID, Name, Age, Start_Date)
```

**Step 3: Add VALUES keyword and data**
```sql
INSERT INTO players (ID, Name, Age, Start_Date)
VALUES (1, 'Yuval', 25, '2020-10-15');
```

**Step 4: Execute the statement**

### Column-Value Correspondence

| Column | Value | Data Type |
|--------|-------|-----------|
| ID | 1 | Integer |
| Name | 'Yuval' | String (in quotes) |
| Age | 25 | Integer |
| Start_Date | '2020-10-15' | Date (in quotes) |

### Important Notes

#### 1. Date Format
Use the correct format: **YYYY-MM-DD** (Year-Month-Day)

```sql
-- ✅ Correct
'2020-10-15'

-- ❌ Wrong (will cause error)
'15/10/2020'
'10-15-2020'
```

#### 2. Order Matters!
Values must match the order of columns:

```sql
-- ✅ Correct: Values match column order
INSERT INTO players (ID, Name, Age, Start_Date)
VALUES (1, 'Yuval', 25, '2020-10-15');

-- ❌ Wrong: Values in wrong order
INSERT INTO players (ID, Name, Age, Start_Date)
VALUES ('Yuval', 1, '2020-10-15', 25);  -- Data goes to wrong columns!
```

#### 3. Quotation Marks
Non-numeric values require quotes:

```sql
-- ✅ Correct
VALUES (1, 'Yuval', 25, '2020-10-15');
       ↑   ↑       ↑    ↑
      No  Yes     No   Yes

-- ❌ Wrong
VALUES (1, Yuval, 25, 2020-10-15);  -- Missing quotes!
```

### Using CURRENT_DATE Function

You can use functions instead of typing the date:

```sql
INSERT INTO players (ID, Name, Age, Start_Date)
VALUES (1, 'Yuval', 25, CURRENT_DATE());
```

or simply:

```sql
INSERT INTO players (ID, Name, Age, Start_Date)
VALUES (1, 'Yuval', 25, CURRENT_DATE);
```

## Inserting Multiple Rows

### Syntax

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES 
    (value1a, value2a, value3a, ...),
    (value1b, value2b, value3b, ...),
    (value1c, value2c, value3c, ...);
```

### Example: Insert Two Players at Once

Two new players have joined the team:
- **Mark**: Age 27, ID 2, Start date 2020-10-12
- **Karl**: Age 26, ID 3, Start date 2020-10-07

**Step 1: Write INSERT INTO command**
```sql
INSERT INTO players (ID, Name, Age, Start_Date)
```

**Step 2: Add VALUES for both players**
```sql
INSERT INTO players (ID, Name, Age, Start_Date)
VALUES 
    (2, 'Mark', 27, '2020-10-12'),
    (3, 'Karl', 26, '2020-10-07');
```

**Step 3: Execute the statement**

### Key Points for Multiple Rows

- Each row is within its own **pair of parentheses**
- Rows are **separated by commas**
- All rows follow the **same column order**
- Execute once to insert all rows

## Viewing Inserted Data

After inserting data, you can verify it was added correctly using a SELECT statement:

```sql
SELECT * FROM players;
```

**Breakdown:**
- **SELECT** - Retrieve data
- **\*** - Asterisk returns all columns
- **FROM** - Keyword indicating the source table
- **players** - Table name

**Output example:**
```
+----+-------+-----+------------+
| ID | Name  | Age | Start_Date |
+----+-------+-----+------------+
| 1  | Yuval | 25  | 2020-10-15 |
| 2  | Mark  | 27  | 2020-10-12 |
| 3  | Karl  | 26  | 2020-10-07 |
+----+-------+-----+------------+
```

## Complete Examples

### Example 1: Student Records

```sql
-- Insert single student
INSERT INTO students (student_id, first_name, last_name, email, enrollment_date)
VALUES (101, 'John', 'Doe', 'john.doe@email.com', '2024-01-15');

-- Insert multiple students
INSERT INTO students (student_id, first_name, last_name, email, enrollment_date)
VALUES 
    (102, 'Jane', 'Smith', 'jane.smith@email.com', '2024-01-16'),
    (103, 'Bob', 'Johnson', 'bob.johnson@email.com', '2024-01-16'),
    (104, 'Alice', 'Williams', 'alice.w@email.com', '2024-01-17');
```

### Example 2: Product Inventory

```sql
-- Insert single product
INSERT INTO products (product_id, product_name, price, quantity, category)
VALUES (1001, 'Laptop', 999.99, 50, 'Electronics');

-- Insert multiple products
INSERT INTO products (product_id, product_name, price, quantity, category)
VALUES 
    (1002, 'Mouse', 19.99, 200, 'Electronics'),
    (1003, 'Keyboard', 49.99, 150, 'Electronics'),
    (1004, 'Monitor', 299.99, 75, 'Electronics');
```

### Example 3: Book Store

```sql
-- Insert books with various data types
INSERT INTO books (book_id, title, author, price, publication_date, in_stock)
VALUES 
    (501, 'SQL Basics', 'John Smith', 29.99, '2023-05-10', TRUE),
    (502, 'Advanced Databases', 'Jane Doe', 39.99, '2023-08-15', TRUE),
    (503, 'Data Science Guide', 'Bob Lee', 49.99, '2023-11-20', FALSE);
```

## Inserting Without Specifying Columns

If you provide values for **all columns** in the **correct order**, you can omit the column list:

```sql
-- With column names (recommended)
INSERT INTO players (ID, Name, Age, Start_Date)
VALUES (4, 'Sarah', 24, '2020-10-20');

-- Without column names (must include ALL columns in correct order)
INSERT INTO players
VALUES (4, 'Sarah', 24, '2020-10-20');
```

**⚠️ Warning:** It's better to always specify columns for clarity and to avoid errors.

## Inserting Partial Data

You can insert data into specific columns only (other columns will be NULL or use default values):

```sql
-- Insert only some columns
INSERT INTO players (ID, Name)
VALUES (5, 'Tom');

-- Age and Start_Date will be NULL or default values
```

## Best Practices

### 1. Always Specify Column Names

```sql
-- ✅ GOOD: Explicit column names
INSERT INTO players (ID, Name, Age, Start_Date)
VALUES (1, 'Yuval', 25, '2020-10-15');

-- ❌ RISKY: Assumes column order
INSERT INTO players
VALUES (1, 'Yuval', 25, '2020-10-15');
```

### 2. Use Correct Data Types

```sql
-- ✅ GOOD: Correct types
INSERT INTO players (ID, Name, Age, Start_Date)
VALUES (1, 'Yuval', 25, '2020-10-15');
       (int) (string) (int) (date)

-- ❌ WRONG: Wrong types
INSERT INTO players (ID, Name, Age, Start_Date)
VALUES ('1', 'Yuval', '25', 20201015);
```

### 3. Match Column and Value Counts

```sql
-- ✅ GOOD: Same number of columns and values
INSERT INTO players (ID, Name, Age, Start_Date)
VALUES (1, 'Yuval', 25, '2020-10-15');
       (4 columns match 4 values)

-- ❌ WRONG: Mismatched counts
INSERT INTO players (ID, Name, Age, Start_Date)
VALUES (1, 'Yuval', 25);  -- Only 3 values for 4 columns!
```

### 4. Use Transactions for Multiple Inserts

```sql
START TRANSACTION;

INSERT INTO players (ID, Name, Age, Start_Date)
VALUES (2, 'Mark', 27, '2020-10-12');

INSERT INTO players (ID, Name, Age, Start_Date)
VALUES (3, 'Karl', 26, '2020-10-07');

COMMIT;  -- or ROLLBACK if there's an error
```

### 5. Validate Data Before Inserting

```sql
-- Check if ID already exists before inserting
SELECT * FROM players WHERE ID = 1;

-- If no results, safe to insert
INSERT INTO players (ID, Name, Age, Start_Date)
VALUES (1, 'Yuval', 25, '2020-10-15');
```

## Common Mistakes to Avoid

### 1. Wrong Date Format

```sql
-- ❌ WRONG
INSERT INTO players (ID, Name, Age, Start_Date)
VALUES (1, 'Yuval', 25, '10/15/2020');

-- ✅ CORRECT
INSERT INTO players (ID, Name, Age, Start_Date)
VALUES (1, 'Yuval', 25, '2020-10-15');
```

### 2. Missing Quotes on Strings

```sql
-- ❌ WRONG
INSERT INTO players (ID, Name, Age, Start_Date)
VALUES (1, Yuval, 25, 2020-10-15);

-- ✅ CORRECT
INSERT INTO players (ID, Name, Age, Start_Date)
VALUES (1, 'Yuval', 25, '2020-10-15');
```

### 3. Values in Wrong Order

```sql
-- ❌ WRONG: Age and Name swapped
INSERT INTO players (ID, Name, Age, Start_Date)
VALUES (1, 25, 'Yuval', '2020-10-15');

-- ✅ CORRECT
INSERT INTO players (ID, Name, Age, Start_Date)
VALUES (1, 'Yuval', 25, '2020-10-15');
```

### 4. Missing Commas Between Multiple Rows

```sql
-- ❌ WRONG: No comma between rows
INSERT INTO players (ID, Name, Age, Start_Date)
VALUES 
    (2, 'Mark', 27, '2020-10-12')
    (3, 'Karl', 26, '2020-10-07');

-- ✅ CORRECT: Comma after first row
INSERT INTO players (ID, Name, Age, Start_Date)
VALUES 
    (2, 'Mark', 27, '2020-10-12'),
    (3, 'Karl', 26, '2020-10-07');
```

## Data Type Examples

| Data Type | Example Values | Needs Quotes? |
|-----------|----------------|---------------|
| **INT** | 1, 25, 100 | ❌ No |
| **VARCHAR/TEXT** | 'Yuval', 'John' | ✅ Yes |
| **DATE** | '2020-10-15' | ✅ Yes |
| **DECIMAL** | 99.99, 100.50 | ❌ No |
| **BOOLEAN** | TRUE, FALSE | ❌ No |
| **DATETIME** | '2024-01-15 14:30:00' | ✅ Yes |

## Summary

You can now identify and make sense of the INSERT syntax and insert new data into tables with the INSERT INTO clause.

### Key Concepts

**Single Row Insert:**
```sql
INSERT INTO table_name (column1, column2, column3)
VALUES (value1, value2, value3);
```

**Multiple Row Insert:**
```sql
INSERT INTO table_name (column1, column2, column3)
VALUES 
    (value1a, value2a, value3a),
    (value1b, value2b, value3b);
```

**View Inserted Data:**
```sql
SELECT * FROM table_name;
```

### Remember

- ✅ Specify column names for clarity
- ✅ Match value order to column order
- ✅ Use correct data types
- ✅ Put non-numeric values in quotes
- ✅ Use YYYY-MM-DD format for dates
- ✅ Separate multiple rows with commas
- ✅ Verify data with SELECT after inserting

**Good luck!** You're now ready to insert data into your database tables efficiently.
