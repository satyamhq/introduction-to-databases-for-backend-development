# 01-numeric-data-types.md

## Overview

Database tables store data in columns and rows. **Data types** ensure each column accepts the correct kind of data—for example, making sure a cost column stores decimals while a product quantity column accepts whole numbers.

## What Are Data Types?

When creating a table in a database, you must define:
- Column names
- Data type for each column

**Purpose of data types:**
- Tell the database management system (e.g., MySQL) how to interpret column values
- Maintain data in the correct format
- Ensure values meet expected criteria

### Common Data Types

- **Numeric** - Numbers (whole or fractional)
- **String** - Text data
- **Date and Time** - Temporal data

### Example Table

| Column Name      | Data Type |
|------------------|-----------|
| Customer Name    | String    |
| Order Date       | Date      |
| Product Quantity | Integer   |
| Total Price      | Decimal   |

## Numeric Data Types

Numeric data types allow columns to store numerical values. The two most common types are:

### 1. Integer Data Type

Used for **whole numbers** only.

- Fractional numbers are automatically rounded up or down to the nearest whole number
- Example: Product Quantity column (1, 2, 3, etc.)

#### Integer Variants in MySQL

| Type      | Alias    | Max Value (Positive) | Notes                    |
|-----------|----------|----------------------|--------------------------|
| TINYINT   | TINYINT  | 255                  | Very small integer values|
| INT       | INTEGER  | ~4 billion           | Very large integer values|

### 2. Decimal Data Type

Used for **numbers with fractional values**.

- Stores both whole and fractional parts
- Whole numbers are stored with a decimal point and `.0` fraction
- Example: Total Price column ($80.90)

**Example:**
- `80.90` → 80 is whole, 90 is fractional (cents)
- `100` → Stored as `100.0`

## Signed vs Unsigned Values

Most numeric data types can accept both:
- **Negative values** (e.g., -50)
- **Positive values** (e.g., 50)

In some database management systems, you can **force columns to accept only positive numbers**. This increases the maximum value they can store.

## Key Takeaways

- **Data types** ensure columns store the correct kind of data
- **Integer** is for whole numbers
- **Decimal** is for fractional numbers
- Different integer and decimal types exist for different value ranges
- Choose the appropriate data type based on the data you need to store
