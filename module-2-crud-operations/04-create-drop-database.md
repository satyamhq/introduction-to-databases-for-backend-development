# CREATE and DROP Database

## Overview

Imagine you've just been hired by an online bookstore to build and maintain databases that store information on millions of books and customers. How do you create and alter databases that store constantly expanding information or process millions of orders from around the world?

The answer lies in SQL's **CREATE** and **DROP** commands.

## Learning Objectives

In this lesson, you'll learn:
- How to create a database using SQL syntax
- How to drop (delete) a database using SQL syntax
- Best practices for naming databases

## Before Creating a Database

Before creating a database, you first need a **clear idea of its purpose**.

### Example: Online Bookshop Database

If you're building a database for an online bookshop, your database needs to record data such as:

- **Book titles**
- **Authors**
- **Customers**
- **Sales**

### Data Organization

The data on these topics must be:
1. **Stored** in relevant tables in a database
2. **Organized** logically
3. **Accessible** for users to retrieve and update as needed

## Creating a Database

### Syntax

```sql
CREATE DATABASE database_name;
```

### Breakdown

- **CREATE** - Keyword to create a new object
- **DATABASE** - Specifies you're creating a database
- **database_name** - The name you choose for your database
- **;** - Semicolon to end the statement

### Example: Create Bookstore Database

```sql
CREATE DATABASE bookstore_db;
```

### Example: Create Second Bookstore Database

```sql
CREATE DATABASE bookstore_db2;
```

### Steps to Create a Database

1. Type the keywords `CREATE DATABASE`
2. Follow with the name of your database
3. Add a semicolon at the end
4. Run the statement
5. The new database appears in your database list

## Database Naming Best Practices

### Rules for Database Names

| Rule | Description | Example |
|------|-------------|---------|
| **Unique** | No two databases can have the same name | ✅ `bookstore_db`, `bookstore_db2` |
| **Maximum Length** | Can only have a maximum of 63 characters | ✅ `online_bookstore_customer_database` |
| **Meaningful** | Use descriptive names | ✅ `bookstore_db` ❌ `db1` |
| **No Spaces** | Use underscores instead | ✅ `bookstore_db` ❌ `bookstore db` |

### Good vs Bad Database Names

```sql
-- ✅ GOOD: Meaningful and descriptive
CREATE DATABASE bookstore_db;
CREATE DATABASE customer_management_system;
CREATE DATABASE sales_analytics_2024;

-- ❌ BAD: Unclear or too generic
CREATE DATABASE db1;
CREATE DATABASE mydb;
CREATE DATABASE data;
```

### Why Meaningful Names Matter

- **Documentation**: Makes it easier to understand the purpose
- **Maintenance**: Helps other developers understand your work
- **Organization**: Easier to manage multiple databases
- **Clarity**: Immediately know what data is stored

### Error Handling

If your database name doesn't meet the requirements, an **error message** will appear.

**Common Errors:**
- Database already exists
- Name is too long (over 63 characters)
- Invalid characters used

```sql
-- This will fail if bookstore_db already exists
CREATE DATABASE bookstore_db;
-- Error: Database 'bookstore_db' already exists
```

## Dropping (Deleting) a Database

### Syntax

```sql
DROP DATABASE database_name;
```

### Breakdown

- **DROP** - Keyword to delete an object
- **DATABASE** - Specifies you're deleting a database
- **database_name** - The name of the database to delete
- **;** - Semicolon to end the statement

### Example: Drop Bookstore Database

```sql
DROP DATABASE bookstore_db;
```

### Steps to Drop a Database

1. Type the keywords `DROP DATABASE`
2. Follow with the name of the database you want to delete
3. Add a semicolon at the end
4. Run the statement
5. SQL deletes the database

### ⚠️ Important Warning

**Dropping a database is PERMANENT!**

- All tables are deleted
- All data is lost
- Cannot be undone
- No confirmation prompt in most systems

**Always double-check before running DROP DATABASE!**

## Practical Examples

### Scenario 1: Creating Multiple Databases

```sql
-- Create a database for books
CREATE DATABASE bookstore_db;

-- Create a database for customers
CREATE DATABASE customer_db;

-- Create a database for orders
CREATE DATABASE orders_db;
```

### Scenario 2: Replacing a Database

```sql
-- Drop the old database
DROP DATABASE old_bookstore_db;

-- Create a new database with a better name
CREATE DATABASE bookstore_main_db;
```

### Scenario 3: Testing Environment

```sql
-- Create a test database
CREATE DATABASE bookstore_test_db;

-- Do your testing...

-- Remove test database when done
DROP DATABASE bookstore_test_db;
```

## Complete Workflow Example

### Step 1: Create the Database

```sql
CREATE DATABASE bookstore_db2;
```

**Result:** Database `bookstore_db2` is created and appears in the database list.

### Step 2: Verify Database Exists

```sql
SHOW DATABASES;
```

**Output:**
```
+--------------------+
| Database           |
+--------------------+
| bookstore_db       |
| bookstore_db2      |
| mysql              |
| sys                |
+--------------------+
```

### Step 3: Use the Database

```sql
USE bookstore_db2;
```

### Step 4: Drop the Database (When Needed)

```sql
DROP DATABASE bookstore_db;
```

**Result:** Database `bookstore_db` is permanently deleted.

## SQL Syntax Summary

### CREATE DATABASE

```sql
-- Basic syntax
CREATE DATABASE database_name;

-- Example
CREATE DATABASE bookstore_db;

-- Check if exists before creating (MySQL/PostgreSQL)
CREATE DATABASE IF NOT EXISTS bookstore_db;
```

### DROP DATABASE

```sql
-- Basic syntax
DROP DATABASE database_name;

-- Example
DROP DATABASE bookstore_db;

-- Check if exists before dropping (MySQL/PostgreSQL)
DROP DATABASE IF EXISTS bookstore_db;
```

## Safety Features

### CREATE IF NOT EXISTS

Prevents errors if the database already exists:

```sql
CREATE DATABASE IF NOT EXISTS bookstore_db;
```

**Benefit:** Won't throw an error if `bookstore_db` already exists.

### DROP IF EXISTS

Prevents errors if the database doesn't exist:

```sql
DROP DATABASE IF EXISTS bookstore_db;
```

**Benefit:** Won't throw an error if `bookstore_db` doesn't exist.

## Database Naming Conventions

### Recommended Patterns

```sql
-- Environment-specific databases
CREATE DATABASE production_bookstore_db;
CREATE DATABASE development_bookstore_db;
CREATE DATABASE testing_bookstore_db;

-- Feature-specific databases
CREATE DATABASE bookstore_inventory_db;
CREATE DATABASE bookstore_sales_db;
CREATE DATABASE bookstore_analytics_db;

-- Date-based databases (for archives)
CREATE DATABASE bookstore_archive_2024_db;
CREATE DATABASE bookstore_backup_20240115_db;
```

### Common Suffixes

| Suffix | Meaning | Example |
|--------|---------|---------|
| `_db` | Database | `bookstore_db` |
| `_prod` | Production | `bookstore_prod` |
| `_dev` | Development | `bookstore_dev` |
| `_test` | Testing | `bookstore_test` |
| `_backup` | Backup | `bookstore_backup` |

## Best Practices Checklist

### Before Creating a Database

- ✅ Plan the database purpose and structure
- ✅ Choose a meaningful, descriptive name
- ✅ Verify the name is unique
- ✅ Keep the name under 63 characters
- ✅ Use underscores instead of spaces
- ✅ Consider using `IF NOT EXISTS` clause

### Before Dropping a Database

- ⚠️ **BACKUP your data first!**
- ⚠️ Verify you have the correct database name
- ⚠️ Confirm no one is using the database
- ⚠️ Check if the database contains important data
- ⚠️ Consider using `IF EXISTS` clause
- ⚠️ Document why you're dropping it

## Common Mistakes to Avoid

### 1. Forgetting the Semicolon

```sql
-- ❌ Wrong: No semicolon
CREATE DATABASE bookstore_db

-- ✅ Correct
CREATE DATABASE bookstore_db;
```

### 2. Using Spaces in Names

```sql
-- ❌ Wrong: Contains space
CREATE DATABASE bookstore db;

-- ✅ Correct: Use underscore
CREATE DATABASE bookstore_db;
```

### 3. Dropping the Wrong Database

```sql
-- ⚠️ DANGER: Always verify the name!
DROP DATABASE bookstore_db;  -- Make sure this is the right one!

-- ✅ Better: Use IF EXISTS
DROP DATABASE IF EXISTS bookstore_db;
```

### 4. Not Planning Before Creating

```sql
-- ❌ Bad: Generic, unclear purpose
CREATE DATABASE db1;

-- ✅ Good: Clear, specific purpose
CREATE DATABASE online_bookstore_customer_management_db;
```

## Summary

You've learned how to create and delete databases using SQL syntax:

### CREATE DATABASE
- **Purpose:** Create a new database
- **Syntax:** `CREATE DATABASE database_name;`
- **Use when:** Starting a new project or adding a new database

### DROP DATABASE
- **Purpose:** Delete an existing database
- **Syntax:** `DROP DATABASE database_name;`
- **Warning:** Permanent deletion—cannot be undone!

### Key Takeaways

1. Always use **meaningful names** for databases
2. Database names must be **unique** and **under 63 characters**
3. **Plan ahead** before creating a database
4. **Be careful** when dropping databases—it's permanent!
5. Use **IF NOT EXISTS** and **IF EXISTS** for safer operations
6. **Always backup** before dropping a database

**Great work!** You now know how to create and manage databases using SQL.
