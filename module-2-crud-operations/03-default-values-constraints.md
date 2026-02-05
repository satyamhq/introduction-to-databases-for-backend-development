# Default Values and Database Constraints

## Purpose of Database Constraints

To ensure the **accuracy and reliability** of data in your database, you must limit the type of data that can go into your database table.

**Database constraints** are used to limit the type of data that can be stored in a table, ensuring that all inserted data is accurate and reliable.

## How Constraints Work

### Violation Handling

If a database detects a **violation** between a constraint and a data operation, it **aborts the operation**.

**Example of violation:**
- Attempting to insert invalid data into a table
- Database recognizes the data is invalid
- Database rejects the operation

### Constraint Levels

**Column Level:**
- Rule applies to a specific column

**Table Level:**
- Rule applies to entire table
- Example: Foreign key constraints prevent actions that destroy links between tables

## Common Database Constraints

Two of the most used database constraints:

1. **NOT NULL** - Prevents empty value fields
2. **DEFAULT** - Assigns default values

## 1. NOT NULL Constraint

### Purpose

The NOT NULL SQL constraint ensures that data fields are **always completed** and **never left blank**.

### Example: Online Store Customer Table

**Scenario:**
- Table records customer IDs and names
- Columns: `customer_id` and `customer_name`
- Both columns must always contain data

**Result:**
- If no data is inserted into either column
- Creation of new customer record is **aborted**

### SQL Implementation

```sql
CREATE TABLE customer (
    customer_id INT NOT NULL,
    customer_name VARCHAR(100) NOT NULL
);
```

### Breaking Down the Statement

1. **CREATE TABLE customer** - Create a table named "customer"
2. **customer_id INT NOT NULL** - Integer column that cannot be null
3. **customer_name VARCHAR(100) NOT NULL** - String column that cannot be null

### How It Works

- Any operation attempting to place a **null value** in these columns will **fail**
- Applies to INSERT and UPDATE operations
- Ensures data integrity

### Example: Valid Insert

```sql
INSERT INTO customer (customer_id, customer_name)
VALUES (1, 'John Doe');
-- ✅ Success - Both values provided
```

### Example: Invalid Insert

```sql
INSERT INTO customer (customer_id, customer_name)
VALUES (1, NULL);
-- ❌ Error - customer_name cannot be NULL
```

## 2. DEFAULT Constraint

### Purpose

The DEFAULT constraint sets a **default value** for a column if no value is specified.

**How it works:**
- If no data is entered for a specific field
- Table automatically inserts a default value instead

### Example: Football Club Player Table

**Scenario:**
- Table: `player`
- Columns: `player_name` and `city`
- Most players are from Barcelona

**Solution:**
- Set default value of `city` column to "Barcelona"
- Don't need to enter "Barcelona" repeatedly
- Automatically filled if no value entered

### SQL Implementation

```sql
CREATE TABLE player (
    player_name VARCHAR(100) NOT NULL,
    city VARCHAR(50) DEFAULT 'Barcelona'
);
```

### Breaking Down the Statement

1. **CREATE TABLE player** - Create a table named "player"
2. **player_name VARCHAR(100) NOT NULL** - String column, required
3. **city VARCHAR(50) DEFAULT 'Barcelona'** - String column with default value

### How It Works

**Insert with city specified:**
```sql
INSERT INTO player (player_name, city)
VALUES ('Lionel Messi', 'Rosario');
-- Result: player_name = 'Lionel Messi', city = 'Rosario'
```

**Insert without city (uses default):**
```sql
INSERT INTO player (player_name)
VALUES ('Gerard Pique');
-- Result: player_name = 'Gerard Pique', city = 'Barcelona' (default)
```

**Insert with explicit NULL (if allowed):**
```sql
INSERT INTO player (player_name, city)
VALUES ('Player Name', NULL);
-- Result: player_name = 'Player Name', city = NULL (not default)
```

## Complete Examples

### Example 1: Customer Table with NOT NULL

```sql
CREATE TABLE customer (
    customer_id INT NOT NULL,
    customer_name VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL
);

-- Valid insert
INSERT INTO customer (customer_id, customer_name, email)
VALUES (1, 'Alice Johnson', 'alice@email.com');

-- Invalid insert - will fail
INSERT INTO customer (customer_id, customer_name)
VALUES (2, 'Bob Smith');
-- Error: email cannot be NULL
```

### Example 2: Product Table with DEFAULT

```sql
CREATE TABLE product (
    product_id INT NOT NULL,
    product_name VARCHAR(100) NOT NULL,
    status VARCHAR(20) DEFAULT 'Available',
    category VARCHAR(50) DEFAULT 'General'
);

-- Insert with all values
INSERT INTO product (product_id, product_name, status, category)
VALUES (1, 'Laptop', 'In Stock', 'Electronics');

-- Insert with defaults
INSERT INTO product (product_id, product_name)
VALUES (2, 'Mouse');
-- Result: status = 'Available', category = 'General' (defaults)
```

### Example 3: Combined NOT NULL and DEFAULT

```sql
CREATE TABLE employee (
    employee_id INT NOT NULL,
    name VARCHAR(100) NOT NULL,
    department VARCHAR(50) DEFAULT 'Unassigned',
    hire_date DATE NOT NULL,
    status VARCHAR(20) DEFAULT 'Active'
);

-- Insert with some defaults
INSERT INTO employee (employee_id, name, hire_date)
VALUES (101, 'Sarah Johnson', '2024-01-15');
-- Result: department = 'Unassigned', status = 'Active' (defaults)
```

## Comparison: NOT NULL vs DEFAULT

| Feature | NOT NULL | DEFAULT |
|---------|----------|---------|
| **Purpose** | Prevent empty values | Provide automatic values |
| **When triggered** | On INSERT/UPDATE | When value not specified |
| **Error handling** | Rejects operation | Inserts default value |
| **Required value** | Yes | No |
| **Can combine** | Yes | Yes |

## Common Use Cases

### NOT NULL Use Cases

- **Unique identifiers** (IDs, usernames)
- **Critical information** (names, emails)
- **Required fields** (status, type)
- **Timestamps** (created_at, updated_at)

### DEFAULT Use Cases

- **Status fields** (Active, Pending, Available)
- **Boolean flags** (is_active, is_deleted)
- **Timestamps** (CURRENT_TIMESTAMP)
- **Location fields** (country, city)
- **Categories** (General, Uncategorized)

## Benefits of Using Constraints

### Data Integrity
- Ensures accuracy of stored data
- Prevents invalid data entry
- Maintains database reliability

### Reduced Errors
- Catches mistakes at database level
- Prevents null pointer errors in applications
- Enforces business rules

### Improved Efficiency
- Default values reduce repetitive data entry
- Automatic value assignment
- Cleaner application code

### Consistency
- Ensures all records have required data
- Standardizes data format
- Maintains data quality

## Best Practices

### When to Use NOT NULL

✅ **Use for:**
- Primary keys
- Required business data
- Critical identifiers

❌ **Avoid for:**
- Optional fields
- Future expansion fields
- Fields that might not apply to all records

### When to Use DEFAULT

✅ **Use for:**
- Common values (status, category)
- Boolean flags
- Timestamps
- Location data with common values

❌ **Avoid for:**
- Unique identifiers
- Data that should be explicitly specified
- Critical business decisions

## Syntax Summary

### NOT NULL Syntax

```sql
column_name data_type NOT NULL
```

**Example:**
```sql
customer_id INT NOT NULL
email VARCHAR(100) NOT NULL
```

### DEFAULT Syntax

```sql
column_name data_type DEFAULT default_value
```

**Example:**
```sql
status VARCHAR(20) DEFAULT 'Active'
country VARCHAR(50) DEFAULT 'USA'
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
```

### Combined Syntax

```sql
column_name data_type NOT NULL DEFAULT default_value
```

**Example:**
```sql
status VARCHAR(20) NOT NULL DEFAULT 'Pending'
is_active BOOLEAN NOT NULL DEFAULT TRUE
```

## Summary

### Key Concepts

**Database Constraints:**
- Limit the type of data stored in tables
- Ensure accuracy and reliability
- Enforce rules at column or table level
- Abort operations that violate constraints

**NOT NULL Constraint:**
- Prevents empty values
- Fields must always be completed
- Required for critical data
- Ensures data completeness

**DEFAULT Constraint:**
- Sets automatic values
- Used when no value specified
- Reduces repetitive data entry
- Improves efficiency

### Important Points

1. **Constraints enforce rules** automatically
2. **NOT NULL** ensures required data
3. **DEFAULT** provides automatic values
4. Can be **combined** for powerful validation
5. **Violations abort** operations
6. Improve **data integrity** and **reliability**

### Pattern to Remember

```sql
CREATE TABLE table_name (
    required_column data_type NOT NULL,
    optional_column data_type,
    default_column data_type DEFAULT 'value',
    both_column data_type NOT NULL DEFAULT 'value'
);
```

By using database constraints effectively, you ensure that your database maintains high-quality, accurate, and reliable data!
