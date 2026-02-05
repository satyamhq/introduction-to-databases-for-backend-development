# 02-string-data-types.md

## Overview

When creating a table in a database, you must define column names and data types. **String data types** are used for columns that accept both numeric and text characters, ensuring data integrity by allowing only valid values.

## What Are String Data Types?

String data types store data containing a mix of character types:
- **Alphabet characters** (A-Z, a-z)
- **Numeric characters** (0-9)
- **Special characters** (@, #, $, %, etc.)

### Example: Student Table

A college database stores student login information with the following columns:

| Column         | Content Type              |
|----------------|---------------------------|
| Student Name   | Alphabet characters only  |
| Username       | Alphanumeric characters   |
| Password       | Mix of character types    |
| Email Address  | Mix of character types    |

## Common String Data Types

String data type is a generic term for different types of string storage in databases.

### 1. CHAR (Character)

Used for **fixed-length** character storage.

**Syntax:**
```sql
CHAR(length)
```

**Characteristics:**
- Length is predetermined and cannot be changed after declaration
- Always occupies the full declared space, even if the actual data is shorter
- Best for predefined, consistent character lengths

**Example:**
```sql
username CHAR(50)
```

If you store `"Mark123"` (7 characters) in a `CHAR(50)` column, it still occupies 50 characters of space—the remaining 43 characters are padded.

### 2. VARCHAR (Variable Character)

Used for **variable-length** character storage.

**Syntax:**
```sql
VARCHAR(max_length)
```

**Characteristics:**
- Length is variable and not fixed
- Only occupies space needed for the actual data stored
- Best when unsure of exact character length
- Maximum length can be specified

**Example:**
```sql
student_name VARCHAR(50)
```

If you store `"Mark Simpson"` (12 characters) in a `VARCHAR(50)` column, it only occupies 12 characters of space, not the full 50.

### CHAR vs VARCHAR Comparison

| Feature          | CHAR              | VARCHAR           |
|------------------|-------------------|-------------------|
| Length           | Fixed             | Variable          |
| Space Usage      | Always full size  | Only actual size  |
| Performance      | Faster (fixed)    | Slightly slower   |
| Best Use Case    | Consistent length | Varying length    |

## Other String Data Types

### TINYTEXT
- Stores up to **255 characters**
- Use case: Short paragraphs

### TEXT
- Stores up to **65,000 characters**
- Use case: Articles

### MEDIUMTEXT
- Stores up to **16.7 million characters**
- Use case: Book text

### LONGTEXT
- Stores up to **4 GB** of text data
- Use case: Very large documents

## Key Takeaways

- **String data types** store mixed character data (text, numbers, symbols)
- **CHAR** is for fixed-length strings
- **VARCHAR** is for variable-length strings
- Choose the appropriate string type based on:
  - Expected data length
  - Storage efficiency needs
  - Performance requirements
