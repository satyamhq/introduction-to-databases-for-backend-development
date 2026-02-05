# 03-how-is-data-related.md

## Introduction

Data stored in a database cannot exist in isolation. It must have relationships with other data to be processed into meaningful information. Understanding how data relates across tables is fundamental to effective database design and management.

## Database Relationships: An Example

Consider a large online store database that needs to retrieve customer details from one table and find orders recorded in another table. The database establishes relationships between these pieces of data through specific mechanisms.

### Example Structure

In an online store database, you might have:

- An **Order Table**
- A **Customer Table**

To locate the details of a customer's order, you check the order number against the customer ID. The database establishes a link between the data in these tables.

## Understanding Tables, Fields, and Records

### The Customer Table

A typical customer table contains the following structure:

| Customer ID | FirstName | LastName | Email                 |
|-------------|-----------+----------+-----------------------|
| C1          | Sarah     | Hogan    | sarah@example.com     |
| C2          | John      | Smith    | john@example.com      |
| C3          | Maria     | Garcia   | maria@example.com     |
| C4          | Katrina   | Langley  | katrina@example.com   |

**Key terminology:**

- **Fields:** The columns in the table (Customer ID, FirstName, LastName, Email)
- **Records:** The rows containing data for each field
- **Entity:** The subject the table represents (in this case, Customer)
- **Instance:** Each individual record or row (e.g., Sarah Hogan is one customer instance)

## Primary Keys

### Purpose

Each record in a table must be uniquely identifiable. If two or more customers share similar information (such as the same first or last name), the database needs a way to distinguish between them.

### Definition

A **Primary Key** is a field that contains only unique values that cannot be replicated elsewhere in the table.

In the customer table, the **Customer ID** serves as the primary key. Even if two customers share the same name, they will have separate customer IDs, allowing the database to determine which customer is required.

## Foreign Keys

### The Order Table

The order table has its own structure:

| Order ID | Product  | Quantity | Customer ID |
|----------|----------|----------|-------------|
| O101     | Laptop   | 1        | C1          |
| O102     | Mouse    | 2        | C3          |
| O103     | Keyboard | 1        | C1          |
| O104     | Monitor  | 1        | C4          |

- **Primary Key:** Order ID (unique to the order table)
- **Foreign Key:** Customer ID (references the customer table)

### Definition

A **Foreign Key** is a field in one table that connects to the primary key field in another table.

In the order table, the Customer ID field serves as a foreign key that establishes a relationship with the customer table, where Customer ID is the primary key.

## Establishing Relationships

By including the Customer ID field in the order table:

1. A relationship is established between the customer table and the order table
2. Data can be retrieved in a meaningful way from both tables
3. The database can determine which customer placed which order

### How It Works

- The **Customer ID** is the **primary key** of the customer table
- The **Customer ID** becomes a **foreign key** in the order table
- This connection creates a relationship between the two tables
- Related data can now be queried and processed together

## Summary

Database relationships enable:

- **Data integrity:** Ensuring accurate connections between related information
- **Efficient queries:** Retrieving related data from multiple tables
- **Meaningful information:** Processing connected data to generate insights

Understanding primary keys, foreign keys, and table relationships is essential for designing robust relational databases that can effectively store and retrieve interconnected data.
