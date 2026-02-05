# Types of Keys in a Database Table

At this stage, you're probably familiar with the relational database model. To fully understand how it works, you first need to understand how tables within a database are related. Essentially, relationships are established between tables with the use of **keys**.

## The Relational Database Model

The relational database model is based on two main concepts:
- **Entities** - defined as tables
- **Relations** - connections between related tables

## Example: Sports Competition Database

Let's use a sports competition example with three tables:

### League Table
| Position | Team_Name | State |
|----------|-----------|-------|
| 1 | Eagles | California |
| 2 | Tigers | Texas |
| 3 | Lions | Florida |

### Teams Table
| Team_Name | Team_Captain | Team_Coach |
|-----------|--------------|------------|
| Eagles | John Smith | Mike Johnson |
| Tigers | Sarah Lee | Tom Brown |
| Lions | David Clark | Emma Wilson |

### Points Table
| Position | Team_Name | Points |
|----------|-----------|--------|
| 1 | Eagles | 85 |
| 2 | Tigers | 78 |
| 3 | Lions | 72 |

Notice that **team_name** appears in multiple tables - this is how relationships are established.

## Types of Attributes

### Simple Attribute
Holds a single value.

**Example: Staff Table**
| Staff_Name | Department |
|------------|------------|
| Alice Brown | IT |
| Bob Wilson | HR |

Each staff name holds only one value per row.

### Multi-Value Attribute
Can hold multiple values (like a list).

**Example (Not Recommended):**
| Staff_Name | Subjects_Taught |
|------------|-----------------|
| Dr. Smith | Math, Physics, Chemistry |

**Note:** Multi-value attributes should be avoided in relational database design.

## Key Attributes

### Key Attribute
A value used to uniquely identify an individual record of data in a table.

**Example: Staff Table**
| Staff_ID | Staff_Name | Contact_Number |
|----------|------------|----------------|
| 101 | Alice Brown | 555-1234 |
| 102 | Bob Wilson | 555-5678 |
| 103 | Carol Davis | 555-9012 |

`Staff_ID` is the key attribute - it has a unique value in each row.

### Candidate Key
Any attribute that contains a unique value in each row of the table.

**Example:**
| Staff_ID | Staff_Name | Contact_Number | Email |
|----------|------------|----------------|-------|
| 101 | Alice Brown | 555-1234 | alice@company.com |
| 102 | Bob Wilson | 555-5678 | bob@company.com |
| 103 | Carol Davis | 555-9012 | carol@company.com |

Both `Staff_ID`, `Contact_Number`, and `Email` are candidate keys (each has unique values).

### Composite Key
A key composed of two or more attributes to form a unique value in each row.

**Example: Enrollment Table**
| Student_ID | Course_ID | Semester | Grade |
|------------|-----------|----------|-------|
| S001 | C101 | Fall2024 | A |
| S001 | C102 | Fall2024 | B |
| S002 | C101 | Fall2024 | A |

Composite Key: `Student_ID` + `Course_ID` (together they uniquely identify each enrollment)

**Example: Staff Table (Alternative)**
| Staff_Name | Staff_Title | Department |
|------------|-------------|------------|
| John Smith | Professor | Computer Science |
| John Smith | Assistant | Library |
| Sarah Lee | Professor | Mathematics |

Composite Key: `Staff_Name` + `Staff_Title` (assuming no duplicate combinations)

### Primary Key
The main unique identifier for a table.

**Example: Staff Table**
| **Staff_ID** (PK) | Staff_Name | Contact_Number |
|-------------------|------------|----------------|
| 101 | Alice Brown | 555-1234 |
| 102 | Bob Wilson | 555-5678 |
| 103 | Carol Davis | 555-9012 |

`Staff_ID` is the primary key - unique for each record and cannot be null.

### Alternate Key (Secondary Key)
A candidate key that was not selected to be the primary key.

**Example:**
| **Staff_ID** (PK) | Staff_Name | Contact_Number (AK) | Email (AK) |
|-------------------|------------|---------------------|------------|
| 101 | Alice Brown | 555-1234 | alice@company.com |
| 102 | Bob Wilson | 555-5678 | bob@company.com |
| 103 | Carol Davis | 555-9012 | carol@company.com |

`Contact_Number` and `Email` are alternate keys - they could have been primary keys but weren't chosen.

### Foreign Key
An attribute in a table that references a unique key in another table.

**Example:**

**Department Table (Parent Table)**
| **Dept_ID** (PK) | Department_Name |
|------------------|-----------------|
| D01 | IT |
| D02 | HR |
| D03 | Finance |

**Staff Table (Child Table)**
| **Staff_ID** (PK) | Staff_Name | Dept_ID (FK) |
|-------------------|------------|--------------|
| 101 | Alice Brown | D01 |
| 102 | Bob Wilson | D02 |
| 103 | Carol Davis | D01 |

`Dept_ID` in the Staff Table is a foreign key that references `Dept_ID` (primary key) in the Department Table.

## Complete Example: College Database

### Students Table
| **Student_ID** (PK) | Student_Name | Email (AK) | Dept_ID (FK) |
|---------------------|--------------|------------|--------------|
| S001 | John Doe | john@college.edu | D01 |
| S002 | Jane Smith | jane@college.edu | D02 |

### Departments Table
| **Dept_ID** (PK) | Department_Name | Building |
|------------------|-----------------|----------|
| D01 | Computer Science | Tech Hall |
| D02 | Mathematics | Science Building |

### Courses Table
| **Course_ID** (PK) | Course_Name | Dept_ID (FK) |
|--------------------|-------------|--------------|
| C101 | Programming | D01 |
| C102 | Calculus | D02 |

### Enrollment Table
| **Student_ID + Course_ID** (Composite PK, both FK) | Semester | Grade |
|---------------------------------------------------|----------|-------|
| S001 + C101 | Fall2024 | A |
| S001 + C102 | Fall2024 | B |
| S002 + C101 | Fall2024 | A |

## Summary

Keys are essential for establishing relationships in a relational database. Understanding the different types of keys is fundamental to database design and management:

- **Candidate Key**: Any attribute with unique values
- **Primary Key**: The chosen unique identifier
- **Alternate Key**: Candidate keys not chosen as primary
- **Composite Key**: Multiple attributes combined for uniqueness
- **Foreign Key**: Links tables together by referencing primary keys
