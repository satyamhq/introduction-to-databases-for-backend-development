# How is Data Related?

## Scenario

You're managing the database of a large online store. Your database must be able to:

1. Retrieve customer details from one table
2. Find the order recorded against another table

**Question:** How does the database establish a relationship between these pieces of data?

## Why Data Must Be Related

Data stored in a database **cannot exist in isolation**. It must have a relationship with other data so that it can be processed into **meaningful information**.

## Example: Online Store Database

### Database Structure

In the online store database, you could have:

- **Order table**
- **Customer table**

### Finding Customer Orders

To locate the details of a customer's order:

1. Check the **order number**
2. Match it against the **customer ID**
3. The database establishes a **link** between the data in the tables

## The Customer Table

### Table Structure

| Customer ID | FirstName | LastName | Email |
|-------------|-----------|----------|-------|
| C1 | Sarah | Hogan | sarah@email.com |
| C2 | John | Smith | john@email.com |
| C3 | Maria | Garcia | maria@email.com |
| C4 | Katrina | Langley | katrina@email.com |

### Relational Database Terms

**Columns:**
- Also called **fields**
- Examples: Customer ID, FirstName, LastName, Email

**Rows:**
- Also called **records**
- Each row contains data for all fields

**Entity:**
- All fields and rows work together to store information
- Example: Customer entity

### Customer Instances

Every row/record in the customer table is an **instance** of the customer entity.

**Examples:**
- Sarah Hogan (Customer ID: C1) - one customer instance
- Katrina Langley (Customer ID: C4) - another customer instance

## The Primary Key

### The Problem

What if two or more customers share similar info?
- Same first name
- Same last name

**Example:**
- Two customers named "John Smith"
- How does the database distinguish between them?

### The Solution: Primary Key

A **primary key** field contains **unique values** that cannot be replicated elsewhere in the table.

**In the Customer Table:**
- **Primary Key:** Customer ID
- Each customer has a separate customer ID
- Even if two customers share the same name, they have different IDs

### Primary Key Characteristics

- Contains **unique values**
- **Cannot be replicated** in the table
- Ensures each record is **uniquely identifiable**
- Database can determine which customer is required

## The Order Table

### Table Structure

| Order ID | Product | Quantity | Price | Customer ID |
|----------|---------|----------|-------|-------------|
| O1 | Laptop | 1 | $999 | C1 |
| O2 | Mouse | 2 | $25 | C2 |
| O3 | Keyboard | 1 | $75 | C1 |
| O4 | Monitor | 1 | $300 | C4 |

### Fields and Records

Just like the customer table, the order table also has:
- **Fields** (columns)
- **Records** (rows)

### Primary Key

**In the Order Table:**
- **Primary Key:** Order ID

## The Foreign Key

### Customer ID in Order Table

Notice there's also a field named **Customer ID** in the order table with the exact same data as in the customer table.

**Purpose:** The Customer ID helps identify who placed the order.

### Establishing Relationships

By adding the Customer ID field to the order table:
- A **relationship** is established between the customer table and order table
- You can pull data in a meaningful way from both tables

### Foreign Key Definition

A **foreign key** is a field in one table that connects to the **primary key** field in the original table.

**In Our Example:**
- **Customer ID** is the primary key of the customer table
- **Customer ID** becomes a foreign key in the order table
- This establishes the relationship between tables

## How Relationships Work

### Visual Representation

```
Customer Table                Order Table
┌─────────────────┐          ┌──────────────────┐
│ Customer ID (PK)│◄─────────┤ Customer ID (FK) │
│ FirstName       │          │ Order ID (PK)    │
│ LastName        │          │ Product          │
│ Email           │          │ Quantity         │
└─────────────────┘          └──────────────────┘
```

**Legend:**
- PK = Primary Key
- FK = Foreign Key
- ◄──── = Relationship

### The Connection

1. **Customer Table:** Customer ID is the **primary key**
2. **Order Table:** Customer ID is the **foreign key**
3. This creates a **relationship** between the tables
4. Data in these two tables is now **related**

## Key Database Terms

### Field
- A column in a table
- Examples: Customer ID, FirstName, Email

### Record
- A row in a table
- Contains data for all fields

### Entity
- The object being stored
- Examples: Customer, Order, Product

### Instance
- A single record/occurrence of an entity
- Example: One specific customer

### Primary Key
- Unique identifier for each record
- Cannot be duplicated in the table
- Example: Customer ID in Customer table

### Foreign Key
- Links to a primary key in another table
- Establishes relationships between tables
- Example: Customer ID in Order table

## Benefits of Related Data

### Data Integrity
- Ensures accuracy and consistency
- Prevents duplicate or orphaned records

### Meaningful Queries
- Can pull data from multiple tables
- Create comprehensive reports

### Organized Structure
- Reduces data redundancy
- Improves database efficiency

### Example Queries

**Find all orders for a specific customer:**
```sql
SELECT * FROM Orders 
WHERE Customer_ID = 'C1'
```

**Find customer details for a specific order:**
```sql
SELECT Customers.FirstName, Customers.LastName, Orders.Product
FROM Customers
JOIN Orders ON Customers.Customer_ID = Orders.Customer_ID
WHERE Orders.Order_ID = 'O1'
```

## Real-World Example

### Scenario

Sarah Hogan (Customer ID: C1) places two orders:

**Customer Table:**
- Customer ID: C1
- Name: Sarah Hogan
- Email: sarah@email.com

**Order Table:**
- Order O1: Laptop, Customer ID: C1
- Order O3: Keyboard, Customer ID: C1

### The Relationship

Because both orders have Customer ID = C1:
- The database knows both orders belong to Sarah Hogan
- You can retrieve all of Sarah's orders
- You can see Sarah's contact information for each order

## Why Relationships Matter

Without relationships:
- ❌ Data exists in isolation
- ❌ Cannot connect customer to orders
- ❌ Difficult to track who bought what
- ❌ Redundant data storage

With relationships:
- ✅ Data is connected and meaningful
- ✅ Easy to track customer purchases
- ✅ Efficient data storage
- ✅ Accurate and consistent information

## Summary

### What We Learned

1. **Data cannot exist in isolation** - must be related to be meaningful
2. **Fields** (columns) and **Records** (rows) store data
3. **Entity** is the object being stored (Customer, Order)
4. **Instance** is a single occurrence of an entity
5. **Primary Key** uniquely identifies each record
6. **Foreign Key** links tables together
7. **Relationships** allow meaningful data retrieval

### Key Concepts

**Primary Key:**
- Unique identifier
- One per table
- Cannot be duplicated

**Foreign Key:**
- Links to primary key in another table
- Establishes relationships
- Can appear multiple times

**Relationship:**
- Connection between tables
- Enables complex queries
- Makes data meaningful

### Pattern to Remember

```
Table A                    Table B
├─ Field 1 (Primary Key)   ├─ Field A
├─ Field 2                 ├─ Field B
└─ Field 3                 └─ Field 1 (Foreign Key)
                                    ↑
                                    └─── Links to Table A
```

By establishing relationships through primary and foreign keys, databases can store data efficiently while maintaining the ability to retrieve it in meaningful and useful ways!
