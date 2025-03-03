Normalization is the process of organizing data in a database to reduce redundancy and improve data integrity. It involves breaking down a table into smaller, more manageable tables while ensuring that relationships between the tables are maintained. Let’s go through all the normalization forms (1NF to 5NF) with examples.
### **1. First Normal Form (1NF)**

#### **Rules for 1NF:**

- Each table cell must contain a single value.
    
- Each column must have a unique name.
    
- The order of data does not matter.
    

#### **Example: Unnormalized Table**

| **Student_ID** | **Student_Name** | **Courses**     |
| -------------- | ---------------- | --------------- |
| 101            | John Doe         | Math, Physics   |
| 102            | Jane Smith       | Chemistry       |
| 103            | Alice Johnson    | Math, Chemistry |
**Problem:**

- The **Courses** column contains multiple values.
    

**Solution:**

- Split the **Courses** column into individual rows.
    

#### **1NF Table**

| **Student_ID** | **Student_Name** | **Course** |
| -------------- | ---------------- | ---------- |
| 101            | John Doe         | Math       |
| 101            | John Doe         | Physics    |
| 102            | Jane Smith       | Chemistry  |
| 103            | Alice Johnson    | Math       |
| 103            | Alice Johnson    | Chemistry  |

---

### **2. Second Normal Form (2NF)**

#### **Rules for 2NF:**

- The table must be in 1NF.
    
- All non-key attributes must depend on the entire primary key.
    

#### **Example: 1NF Table**

| **Student_ID** | **Course_ID** | **Course_Name** | **Instructor** |
| -------------- | ------------- | --------------- | -------------- |
| 101            | C101          | Math            | Dr. Smith      |
| 101            | C102          | Physics         | Dr. Brown      |
| 102            | C101          | Math            | Dr. Smith      |
| 103            | C103          | Chemistry       | Dr. Green      |
|                |               |                 |                |

**Problem:**

- **Course_Name** and **Instructor** depend only on **Course_ID** (partial dependency).
    

**Solution:**

- Split the table into two tables:
    
    1. **Enrollments** (Student_ID, Course_ID)
        
    2. **Courses** (Course_ID, Course_Name, Instructor)
        

#### **2NF Tables**

**Enrollments Table**

| **Student_ID** | **Course_ID** |
| -------------- | ------------- |
| 101            | C101          |
| 101            | C102          |
| 102            | C101          |
| 103            | C103          |

**Courses Table**

| **Course_ID** | **Course_Name** | **Instructor** |
| ------------- | --------------- | -------------- |
| C101          | Math            | Dr. Smith      |
| C102          | Physics         | Dr. Brown      |
| C103          | Chemistry       | Dr. Green      |

---

### **3. Third Normal Form (3NF)**

#### **Rules for 3NF:**

- The table must be in 2NF.
    
- There should be no transitive dependency (non-key attributes should not depend on other non-key attributes).
    

#### **Example: 2NF Courses Table**

| **Course_ID** | **Course_Name** | **Instructor** | **Instructor_Office** |
| ------------- | --------------- | -------------- | --------------------- |
| C101          | Math            | Dr. Smith      | Room 101              |
| C102          | Physics         | Dr. Brown      | Room 102              |
| C103          | Chemistry       | Dr. Green      | Room 103              |

**Problem:**

- **Instructor_Office** depends on **Instructor**, which is a non-key attribute.
    

**Solution:**

- Split the table into two tables:
    
    1. **Courses** (Course_ID, Course_Name, Instructor)
        
    2. **Instructors** (Instructor, Instructor_Office)
        

#### **3NF Tables**

**Courses Table**

| **Course_ID** | **Course_Name** | **Instructor** |
| ------------- | --------------- | -------------- |
| C101          | Math            | Dr. Smith      |
| C102          | Physics         | Dr. Brown      |
| C103          | Chemistry       | Dr. Green      |

**Instructors Table**

| **Instructor** | **Instructor_Office** |
| -------------- | --------------------- |
| Dr. Smith      | Room 101              |
| Dr. Brown      | Room 102              |
| Dr. Green      | Room 103              |

---

### **4. Boyce-Codd Normal Form (BCNF)**

#### **Rules for BCNF:**

- The table must be in 3NF.
    
- For every functional dependency X→YX→Y, XX must be a superkey.
    

#### **Example: 3NF Courses Table**

| **Course_ID** | **Course_Name** | **Instructor** |
| ------------- | --------------- | -------------- |
| C101          | Math            | Dr. Smith      |
| C102          | Physics         | Dr. Brown      |
| C103          | Chemistry       | Dr. Green      |

**Functional Dependencies:**

1. **Course_ID → Course_Name, Instructor**
    
2. **Instructor → Course_ID**
    

**Problem:**

- The second functional dependency (**Instructor → Course_ID**) violates BCNF because **Instructor** is not a superkey.
    

**Solution:**

- Split the table into two tables:
    
    1. **Courses** (Course_ID, Course_Name)
        
    2. **Course-Instructor** (Course_ID, Instructor)
        

#### **BCNF Tables**

**Courses Table**

| **Course_ID** | **Course_Name** |
| ------------- | --------------- |
| C101          | Math            |
| C102          | Physics         |
| C103          | Chemistry       |

**Course-Instructor Table**

| **Course_ID** | **Instructor** |
| ------------- | -------------- |
| C101          | Dr. Smith      |
| C102          | Dr. Brown      |
| C103          | Dr. Green      |

---

### **5. Fourth Normal Form (4NF)**

#### **Rules for 4NF:**

- The table must be in BCNF.
    
- It should not have multi-valued dependencies (MVDs) unless they are trivial.
    

#### **Example: Student-Skills-Interests Table**

| **Student_ID** | **Skill** | **Interest** |
| -------------- | --------- | ------------ |
| 101            | Math      | Chess        |
| 101            | Math      | Music        |
| 101            | Physics   | Chess        |
| 101            | Physics   | Music        |
| 102            | Chemistry | Painting     |

**Problem:**

- **Student_ID** determines multiple **Skills** and **Interests** independently.
    

**Solution:**

- Split the table into two tables:
    
    1. **Student-Skills** (Student_ID, Skill)
        
    2. **Student-Interests** (Student_ID, Interest)
        

#### **4NF Tables**

**Student-Skills Table**

| **Student_ID** | **Skill** |
| -------------- | --------- |
| 101            | Math      |
| 101            | Physics   |
| 102            | Chemistry |

**Student-Interests Table**

| **Student_ID** | **Interest** |
| -------------- | ------------ |
| 101            | Chess        |
| 101            | Music        |
| 102            | Painting     |

---

### **6. Fifth Normal Form (5NF)**

#### **Rules for 5NF:**

- The table must be in 4NF.
    
- It cannot be further decomposed without losing information.
    

#### **Example: Supplier-Part-Project Table**

| **Supplier_ID** | **Part_ID** | **Project_ID** |
| --------------- | ----------- | -------------- |
| S1              | P1          | J1             |
| S1              | P2          | J2             |
| S2              | P1          | J1             |
| S2              | P1          | J2             |

**Problem:**

- The table represents a ternary relationship where a supplier supplies parts to projects.
    

**Solution:**

- Decompose the table into three tables:
    
    1. **Supplier-Part** (Supplier_ID, Part_ID)
        
    2. **Supplier-Project** (Supplier_ID, Project_ID)
        
    3. **Part-Project** (Part_ID, Project_ID)
        

#### **5NF Tables**

**Supplier-Part Table**

| **Supplier_ID** | **Part_ID** |
| --------------- | ----------- |
| S1              | P1          |
| S1              | P2          |
| S2              | P1          |

**Supplier-Project Table**

| **Supplier_ID** | **Project_ID** |
| --------------- | -------------- |
| S1              | J1             |
| S1              | J2             |
| S2              | J1             |
| S2              | J2             |

**Part-Project Table**

| **Part_ID** | **Project_ID** |
| ----------- | -------------- |
| P1          | J1             |
| P1          | J2             |
| P2          | J2             |
### Summary

| **Normal Form** | **Key Concept**                      | **Fixes**                                       |
| --------------- | ------------------------------------ | ----------------------------------------------- |
| **1NF**         | Atomicity                            | No multi-valued attributes.                     |
| **2NF**         | No Partial Dependency                | Every non-key depends on the whole primary key. |
| **3NF**         | No Transitive Dependency             | Non-key columns depend only on the primary key. |
| **BCNF**        | Every Determinant is a Candidate Key | Stronger 3NF rule.                              |
| **4NF**         | No Multi-Valued Dependency           | Separate independent relationships.             |
| **5NF**         | No Join Dependency                   | Eliminate unnecessary table joins.              |
### Key functions of Normailization
### **Key Steps in Logical Table Breakdown (Normalization Process)**

1. **Identify repeating groups** → Convert to **1NF**
2. **Remove partial dependencies** → Convert to **2NF**
3. **Eliminate transitive dependencies** → Convert to **3NF**
4. **Ensure all determinants are candidate keys** → Convert to **BCNF**
5. **Break multi-valued dependencies** → Convert to **4NF**
6. **Remove join dependencies** → Convert to **5NF**

### **🚀 Final Takeaways**

- **Normalization improves database efficiency, eliminates redundancy, and avoids anomalies.**
- **1NF to 3NF are commonly used in most applications.**
- **BCNF, 4NF, and 5NF are useful for complex databases.**
