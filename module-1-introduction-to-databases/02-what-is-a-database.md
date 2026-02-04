# What is a Database?

## Introduction

Data and databases are integral to our daily online activities. Uploading photos to social media, downloading files at work, and playing games online all involve database interactions. Understanding the fundamental concepts of data and databases is essential for working with modern information systems.

## Understanding Data

**Data** consists of facts and figures about any subject or entity. Data can represent various types of information:

**Personal Data:**
- Name
- Age
- Email address
- Date of birth

**Transactional Data:**
- Order number
- Product description
- Order quantity
- Purchase date
- Customer email

Data is crucial for both individuals and organizations, forming the foundation of decision-making and operational processes.

## Defining a Database

A **database** is a form of electronic storage in which data is organized systematically. It provides a structured environment to store and manipulate data electronically, making information more manageable, efficient, and secure.

In the digital era, databases have replaced manual filing systems, enabling rapid access, modification, and analysis of vast amounts of information.

## Real-World Database Applications

Databases power critical operations across various sectors:

- **Banking**: Store customer information, account records, and transaction histories
- **Healthcare**: Maintain patient records, staff credentials, laboratory results, and medical data

## Database Structure

A database organizes data systematically, typically resembling a spreadsheet or table format. This systematic organization means that data is structured according to identifiable elements, features, and attributes.

### Entities and Attributes

**Entities** represent specific elements or concepts and store related data in a table-like format. Entities can be:

**Physical Representations:**
- Employees
- Customers
- Products

**Conceptual Representations:**
- Orders
- Invoices
- Quotations

**Attributes** are the characteristics or features that define an entity. For example, a customer entity might include:

- First name
- Last name
- Date of birth
- Email address

Similarly, a product entity could contain:

- Product code
- Description
- Price
- Availability

### Relational Database Structure

In relational databases:

- **Entities** are known as **relations** or **tables**
- **Attributes** become the **columns** of the table
- Each **row** represents an individual instance of that entity

**Example: Online Store**

An order table might organize data into rows containing:

- Unique order number
- Customer name
- Product ordered
- Product price

This structure creates relationships between different data elements, enabling efficient data management and retrieval.

## Types of Databases

Database Engineers work with various database models, each suited to different use cases and data structures.

### Relational Databases

Data is organized in tables with rows and columns, establishing relationships between different entities through keys and constraints.

### Object-Oriented Databases

Data is stored as objects rather than tables or relations.

**Example: Online Bookstore**

The database represents authors, customers, books, and publishers as classes (sets or categories). Individual objects or instances of these classes contain the actual data.

### Graph Databases

Data is stored in the form of nodes and edges.

- **Nodes** represent entities (customers, orders, products)
- **Edges** represent the relationships between nodes

This structure is particularly effective for analyzing complex relationships and networks.

### Document Databases

Data is stored as JSON (JavaScript Object Notation) objects, organized into collections.

**Structure:**
- Collections function similarly to tables
- Within each collection, documents written in JSON record data
- Example: Customer documents in a customer collection, order and product documents in separate collections

## Database Hosting

Databases can be hosted in two primary environments:

### On-Premises Hosting

The database is hosted on dedicated machines within an organization's physical premises, providing direct control over hardware and security.

### Cloud Hosting

Currently the more popular choice, cloud databases offer several advantages:

- Store, manage, and retrieve data via cloud platforms
- Access data through the Internet from anywhere
- Lower-cost option for data management
- Scalability and flexibility
- Reduced infrastructure maintenance requirements

## Summary

A database is a systematic, electronic storage system that organizes data efficiently and securely. Understanding how data is structured through entities and attributes, and familiarity with different database types—relational, object-oriented, graph, and document databases—forms the foundation for effective database engineering and management.
