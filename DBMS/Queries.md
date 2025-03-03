## **SQL Commands: DDL, DML, and TCL**

SQL commands are categorized into **three main types**:

1. **DDL (Data Definition Language)**
2. **DML (Data Manipulation Language)**
3. **TCL (Transaction Control Language)**

---

## **1️⃣ DDL (Data Definition Language)**

DDL commands **define and manage database objects** such as tables, indexes, and schemas.  
✅ **These commands affect the database structure, not the data inside.**  
✅ **Auto-committed (cannot be rolled back).**

### **DDL Commands**:

|Command|Description|
|---|---|
|`CREATE`|Creates a new database/table/view/index.|
|`ALTER`|Modifies an existing database/table.|
|`DROP`|Deletes a table/database permanently.|
|`TRUNCATE`|Deletes all data from a table but keeps structure.|
|`RENAME`|Renames a table or column.|`
```
-- 1. Create Table
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    name VARCHAR(100),
    salary DECIMAL(10,2)
);

-- 2. Alter Table (Add a new column)
ALTER TABLE employees ADD department VARCHAR(50);

-- 3. Drop Table (Deletes table permanently)
DROP TABLE employees;

-- 4. Truncate Table (Deletes all data but keeps table)
TRUNCATE TABLE employees;

-- 5. Rename Table
RENAME TABLE employees TO staff;

```

## **2️⃣ DML (Data Manipulation Language)**

DML commands **manipulate the data** inside tables.  
✅ **Affect only the data, not the structure.**  
✅ **Can be rolled back using TCL commands.**

### **DML Commands**:

| Command  | Description                   |
| -------- | ----------------------------- |
| `INSERT` | Adds new records to a table.  |
| `UPDATE` | Modifies existing records.    |
| `DELETE` | Removes records from a table. |
### Example DML Commands
```
-- 1. Insert Data
INSERT INTO employees (emp_id, name, salary, department) 
VALUES (1, 'John Doe', 50000, 'HR');

-- 2. Update Data
UPDATE employees SET salary = 60000 WHERE emp_id = 1;

-- 3. Delete Data
DELETE FROM employees WHERE emp_id = 1;

```
## **3️⃣ TCL (Transaction Control Language)**

TCL commands **manage transactions** and ensure data integrity.  
✅ **Used with DML commands (`INSERT`, `UPDATE`, `DELETE`).**  
✅ **Helps in rolling back or committing transactions.**

### **TCL Commands**:

| Command     | Description                               |
| ----------- | ----------------------------------------- |
| `COMMIT`    | Saves all changes permanently.            |
| `ROLLBACK`  | Undoes changes since last COMMIT.         |
| `SAVEPOINT` | Creates a savepoint within a transaction. |
### Example TCL Commands
```
-- Start Transaction
BEGIN;

-- Insert Employee
INSERT INTO employees (emp_id, name, salary, department) 
VALUES (2, 'Jane Smith', 70000, 'IT');

-- Savepoint
SAVEPOINT sp1;

-- Update Employee Salary
UPDATE employees SET salary = 75000 WHERE emp_id = 2;

-- Rollback to Savepoint (Undo salary update)
ROLLBACK TO sp1;

-- Commit Transaction (Save changes permanently)
COMMIT;

```
## **📝 Summary Table**

| Category | Commands                                        | Description                              |
| -------- | ----------------------------------------------- | ---------------------------------------- |
| **DDL**  | `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME` | Defines/modifies the database structure. |
| **DML**  | `INSERT`, `UPDATE`, `DELETE`                    | Modifies data inside the table.          |
| **TCL**  | `COMMIT`, `ROLLBACK`, `SAVEPOINT`               | Manages transactions and data integrity. |

---

## **🔥 Key Differences**

| Feature                | DDL                      | DML              | TCL                   |
| ---------------------- | ------------------------ | ---------------- | --------------------- |
| **Purpose**            | Defines database objects | Manipulates data | Controls transactions |
| **Affects**            | Table structure          | Table data       | Transaction process   |
| **Rollback Possible?** | ❌ No                     | ✅ Yes            | ✅ Yes                 |
| **Auto-Commit?**       | ✅ Yes                    | ❌ No             | ❌ No                  |
### Procedures
### **📌 Stored Procedures in MySQL**

A **Stored Procedure** is a **precompiled SQL code** that can be executed multiple times. It helps in **reducing redundancy** and **improving performance** by allowing users to encapsulate logic in the database itself.

---

## **🔹 Syntax to Create a Stored Procedure**

![[Pasted image 20250303224706.png]]
---
## **🔹 Example 1: Simple Procedure Without Parameters**

👉 A procedure to fetch all users from a `Users` table.
![[Pasted image 20250303224743.png]]
![[Pasted image 20250303224823.png]]
---

## **🔹 Example 2: Procedure with Input Parameters**

👉 A procedure to get user details by `UserID`.
![[Pasted image 20250303224843.png]]
---

## **🔹 Example 3: Procedure with Input & Output Parameters**

👉 A procedure to **return a user's email** based on their `UserID`.
![[Pasted image 20250303224907.png]]
---

## **🔹 Example 4: Procedure with Transactions (Deposit Money)**

👉 A procedure to **deposit money into a bank account** securely.
![[Pasted image 20250303224933.png]]
---

![[Pasted image 20250303224956.png]]

---

## **🔹 Benefits of Stored Procedures**

✅ **Improves Performance** – Precompiled queries execute faster.  
✅ **Increases Security** – Users can be restricted from direct table access.  
✅ **Reduces Redundancy** – Common SQL logic can be reused easily