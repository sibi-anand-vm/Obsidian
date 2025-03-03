### **Keys in DBMS: A Comprehensive Explanation**

Keys are a fundamental concept in relational databases. They are used to uniquely identify records in a table and establish relationships between tables. Let’s dive into the different types of keys, their purposes, and examples.

---
### **1. What is a Key?**

A **key** is an attribute (or a set of attributes) that uniquely identifies a record (row) in a table. Keys ensure data integrity and help in establishing relationships between tables.

---

### **2. Types of Keys**

#### **A. Primary Key**

- A **primary key** uniquely identifies each record in a table.
    
- It cannot contain **NULL** values.
    
- A table can have only **one primary key**.
    
#### **Example:**
```
CREATE TABLE Students (
    Student_ID INT PRIMARY KEY,
    Student_Name VARCHAR(50),
    Age INT
);
```
- **Student_ID** is the primary key.
    

#### **B. Foreign Key**

- A **foreign key** is a column (or set of columns) in one table that refers to the primary key in another table.
    
- It establishes a relationship between two tables.
    
- It can contain **NULL** values.
    
#### **Example:**
```
CREATE TABLE Enrollments (
    Enrollment_ID INT PRIMARY KEY,
    Student_ID INT,
    Course_ID INT,
    FOREIGN KEY (Student_ID) REFERENCES Students(Student_ID),
    FOREIGN KEY (Course_ID) REFERENCES Courses(Course_ID)
);
```
- **Student_ID** and **Course_ID** are foreign keys.
    

#### **C. Unique Key**

- A **unique key** ensures that all values in a column are unique.
    
- Unlike a primary key, it can contain **NULL** values.
    
- A table can have **multiple unique keys**.
    
#### **Example:**
```
CREATE TABLE Employees (
    Employee_ID INT PRIMARY KEY,
    Email VARCHAR(100) UNIQUE,
    Phone VARCHAR(15) UNIQUE
);
```
- **Email** and **Phone** are unique keys.
    
#### **D. Composite Key**

- A **composite key** is a combination of two or more columns that uniquely identify a record.
    
- It is used when a single column is not sufficient to ensure uniqueness.
    
#### **Example:**
```
CREATE TABLE Orders (
    Order_ID INT,
    Product_ID INT,
    Quantity INT,
    PRIMARY KEY (Order_ID, Product_ID)
);
```
- **Customer_ID**, **Email**, and **Phone** are candidate keys.
    
#### **F. Super Key**

- A **super key** is a set of attributes that can uniquely identify a record.
    
- It may contain additional attributes that are not necessary for uniqueness.
#### **Example:**
```
CREATE TABLE Employees (
    Employee_ID INT,
    Email VARCHAR(100),
    Phone VARCHAR(15),
    PRIMARY KEY (Employee_ID)
);
```
#### **F. Super Key**
- A **super key** is a set of attributes that can uniquely identify a record.
    
- It may contain additional attributes that are not necessary for uniqueness.
#### **Example:**

```
CREATE TABLE Employees (
    Employee_ID INT,
    Email VARCHAR(100),
    Phone VARCHAR(15),
    PRIMARY KEY (Employee_ID)
);
```
- **Employee_ID**, **Employee_ID + Email**, and **Employee_ID + Phone** are super keys.
    
#### **G. Alternate Key**

- An **alternate key** is a candidate key that is not chosen as the primary key.
    
- It can still uniquely identify a record.
    
#### **Example:**
```
CREATE TABLE Customers (
    Customer_ID INT PRIMARY KEY,
    Email VARCHAR(100) UNIQUE,
    Phone VARCHAR(15) UNIQUE
);
```

- **Email** and **Phone** are alternate keys.