# CREATE TABLE Statement

## Overview

Building a database involves working with substantial amounts of data. But how do you organize your data so that you can find exactly what you need and make sense of it? With SQL, you can create tables within your database to hold and organize your data.

## Learning Objectives

In this lesson, you'll learn how to create tables in a database management system using SQL syntax.

## CREATE TABLE Syntax

### Basic Structure

```sql
CREATE TABLE table_name (
    column_name1 datatype(size),
    column_name2 datatype(size),
    column_name3 datatype(size)
);
```

### Syntax Breakdown

1. **CREATE TABLE** - Keywords to tell SQL you want to create a new table
2. **table_name** - The name you choose for your table
3. **( )** - Parentheses to contain column definitions
4. **column_name** - Name of each column in the table
5. **datatype** - Type of data the column will hold
6. **(size)** - Optional size specification for the datatype
7. **;** - Semicolon to end the statement

## Important Prerequisite

**Before you can create tables, you must already have a database on the server.**

In other words, you **can't build tables if there's no database** to create them in.

### Check Your Database

```sql
-- First, make sure you have a database
CREATE DATABASE bookstore_db;

-- Then, use the database
USE bookstore_db;

-- Now you can create tables
CREATE TABLE customers (...);
```

## Practical Example: Customer Table

Let's create a customer table in the bookstore database to store customer data like names and phone numbers.

### Step-by-Step Creation

**Step 1: Write the CREATE TABLE command**
```sql
CREATE TABLE customers
```

**Step 2: Add opening parenthesis**
```sql
CREATE TABLE customers (
```

**Step 3: Define first column (customer_name)**
```sql
CREATE TABLE customers (
    customer_name VARCHAR(100)
```

**Step 4: Add comma and define second column (phone_number)**
```sql
CREATE TABLE customers (
    customer_name VARCHAR(100),
    phone_number INT
```

**Step 5: Add closing parenthesis and semicolon**
```sql
CREATE TABLE customers (
    customer_name VARCHAR(100),
    phone_number INT
);
```

**Step 6: Execute the statement**

The customers table is now stored in the database!

## Understanding Data Types

### VARCHAR Data Type

```sql
customer_name VARCHAR(100)
```

**VARCHAR** means:
- **Variable Character** - Can hold text data
- The column can hold data of **any character type** (letters, numbers, symbols)
- The number in parentheses (100) specifies the **maximum length**
- More accurate description: Can hold strings up to the specified length

### INT Data Type

```sql
phone_number INT
```

**INT** means:
- **Integer** - Can only hold whole numbers
- No decimal points allowed
- Positive or negative numbers
- Useful for IDs, counts, and numeric identifiers

## Common Data Types

| Data Type | Description | Example Values | Use Case |
|-----------|-------------|----------------|----------|
| **VARCHAR(n)** | Variable-length string | 'John Doe', 'Hello' | Names, addresses, text |
| **INT** | Integer (whole number) | 1, 100, -50 | IDs, ages, quantities |
| **DECIMAL(p,s)** | Decimal number | 19.99, 100.50 | Prices, precise calculations |
| **DATE** | Date value | '2024-01-15' | Birth dates, order dates |
| **BOOLEAN** | True/False | TRUE, FALSE | Yes/no questions |
| **TEXT** | Long text | Articles, descriptions | Large text content |

## Complete Examples

### Example 1: Simple Customer Table

```sql
CREATE TABLE customers (
    customer_name VARCHAR(100),
    phone_number INT
);
```

### Example 2: More Detailed Customer Table

```sql
CREATE TABLE customers (
    customer_id INT,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100),
    phone_number VARCHAR(20),
    date_of_birth DATE
);
```

### Example 3: Books Table

```sql
CREATE TABLE books (
    book_id INT,
    title VARCHAR(200),
    author VARCHAR(100),
    price DECIMAL(10, 2),
    publication_date DATE,
    in_stock BOOLEAN
);
```

### Example 4: Orders Table

```sql
CREATE TABLE orders (
    order_id INT,
    customer_id INT,
    order_date DATE,
    total_amount DECIMAL(10, 2),
    status VARCHAR(20)
);
```

## Best Practices for Creating Tables

### 1. Use Meaningful Table Names

```sql
-- ✅ GOOD: Clear and descriptive
CREATE TABLE customers (...);
CREATE TABLE book_inventory (...);
CREATE TABLE customer_orders (...);

-- ❌ BAD: Unclear or too generic
CREATE TABLE table1 (...);
CREATE TABLE data (...);
CREATE TABLE temp (...);
```

### 2. Use Meaningful Column Names

```sql
-- ✅ GOOD: Self-explanatory
CREATE TABLE customers (
    customer_id INT,
    first_name VARCHAR(50),
    last_name VARCHAR(50)
);

-- ❌ BAD: Cryptic or unclear
CREATE TABLE customers (
    id INT,
    fn VARCHAR(50),
    ln VARCHAR(50)
);
```

### 3. Choose Appropriate Data Types

```sql
-- ✅ GOOD: Appropriate types
CREATE TABLE products (
    product_id INT,
    product_name VARCHAR(100),
    price DECIMAL(10, 2),
    quantity_in_stock INT
);

-- ❌ BAD: Wrong or inefficient types
CREATE TABLE products (
    product_id VARCHAR(100),  -- Should be INT
    product_name TEXT,        -- VARCHAR is more efficient
    price VARCHAR(20),        -- Should be DECIMAL
    quantity_in_stock VARCHAR(10)  -- Should be INT
);
```

### 4. Specify Appropriate Sizes

```sql
-- ✅ GOOD: Reasonable sizes
CREATE TABLE users (
    username VARCHAR(50),      -- Most usernames are < 50 chars
    email VARCHAR(100),        -- Most emails are < 100 chars
    bio VARCHAR(500)          -- Bios can be longer
);

-- ❌ BAD: Too large or too small
CREATE TABLE users (
    username VARCHAR(5),       -- Too small, will truncate
    email VARCHAR(1000),       -- Unnecessarily large
    bio VARCHAR(10)           -- Way too small for a bio
);
```

## Table Creation Workflow

### Complete Workflow Example

```sql
-- Step 1: Create the database (if it doesn't exist)
CREATE DATABASE bookstore_db;

-- Step 2: Use the database
USE bookstore_db;

-- Step 3: Create your first table
CREATE TABLE customers (
    customer_id INT,
    customer_name VARCHAR(100),
    email VARCHAR(100),
    phone_number VARCHAR(20)
);

-- Step 4: Create additional tables
CREATE TABLE books (
    book_id INT,
    title VARCHAR(200),
    author VARCHAR(100),
    price DECIMAL(10, 2)
);

CREATE TABLE orders (
    order_id INT,
    customer_id INT,
    book_id INT,
    order_date DATE,
    quantity INT
);

-- Step 5: Verify tables were created
SHOW TABLES;
```

## Viewing Table Structure

After creating a table, you can view its structure:

### MySQL/MariaDB

```sql
DESCRIBE customers;
-- or
SHOW COLUMNS FROM customers;
```

**Output:**
```
+---------------+--------------+------+-----+---------+-------+
| Field         | Type         | Null | Key | Default | Extra |
+---------------+--------------+------+-----+---------+-------+
| customer_name | varchar(100) | YES  |     | NULL    |       |
| phone_number  | int          | YES  |     | NULL    |       |
+---------------+--------------+------+-----+---------+-------+
```

### PostgreSQL

```sql
\d customers
```

### SQL Server

```sql
sp_help customers;
```

## Common Mistakes to Avoid

### 1. Forgetting to Use the Database

```sql
-- ❌ Wrong: No database selected
CREATE TABLE customers (...);
-- Error: No database selected

-- ✅ Correct: Select database first
USE bookstore_db;
CREATE TABLE customers (...);
```

### 2. Missing Commas Between Columns

```sql
-- ❌ Wrong: No comma between columns
CREATE TABLE customers (
    customer_name VARCHAR(100)
    phone_number INT
);

-- ✅ Correct: Comma after each column (except last)
CREATE TABLE customers (
    customer_name VARCHAR(100),
    phone_number INT
);
```

### 3. Forgetting Parentheses

```sql
-- ❌ Wrong: No parentheses
CREATE TABLE customers
    customer_name VARCHAR(100),
    phone_number INT;

-- ✅ Correct: Columns enclosed in parentheses
CREATE TABLE customers (
    customer_name VARCHAR(100),
    phone_number INT
);
```

### 4. Table Already Exists

```sql
-- ❌ Will fail if table exists
CREATE TABLE customers (...);

-- ✅ Better: Check if exists first
CREATE TABLE IF NOT EXISTS customers (...);
```

## Advanced CREATE TABLE Features

### Adding Constraints

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    phone_number VARCHAR(20),
    registration_date DATE DEFAULT CURRENT_DATE
);
```

**Constraints explained:**
- `PRIMARY KEY` - Unique identifier for each row
- `NOT NULL` - Column cannot be empty
- `UNIQUE` - No duplicate values allowed
- `DEFAULT` - Default value if none provided

### Auto-Increment ID

```sql
CREATE TABLE customers (
    customer_id INT AUTO_INCREMENT PRIMARY KEY,
    customer_name VARCHAR(100),
    email VARCHAR(100)
);
```

The `customer_id` will automatically increment for each new record.

## Summary

You've learned how to create tables in a database using SQL syntax.

### Key Points

1. **Prerequisite:** Must have a database before creating tables
2. **Syntax:** `CREATE TABLE table_name (columns...);`
3. **Components:**
   - Table name
   - Column names
   - Data types
   - Optional sizes

### Basic CREATE TABLE Structure

```sql
CREATE TABLE table_name (
    column1 datatype(size),
    column2 datatype(size),
    column3 datatype(size)
);
```

### Example

```sql
CREATE TABLE customers (
    customer_name VARCHAR(100),
    phone_number INT
);
```

**Remember:**
- Use meaningful names
- Choose appropriate data types
- Specify reasonable sizes
- Format for readability
- Always end with a semicolon

**Well done!** You now know how to create tables to organize and store your data in SQL databases.
