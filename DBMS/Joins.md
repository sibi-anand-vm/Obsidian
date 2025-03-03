### **📌 SQL Joins Overview**

Joins are used to **combine rows** from two or more tables based on a related column.

---
## **🔹 Types of Joins in SQL**

| **Join Type**       | **Description**                                                        |
| ------------------- | ---------------------------------------------------------------------- |
| **INNER JOIN**      | Returns matching rows from both tables.                                |
| **LEFT JOIN**       | Returns all rows from the left table and matching rows from the right. |
| **RIGHT JOIN**      | Returns all rows from the right table and matching rows from the left. |
| **FULL OUTER JOIN** | Returns all rows from both tables (MySQL doesn't support it directly). |
| **CROSS JOIN**      | Returns the Cartesian product of both tables.                          |

---
## **🔹 Sample Tables**

### **Table: Employees**

| EmpID | EmpName | DeptID |
| ----- | ------- | ------ |
| 1     | Alice   | 10     |
| 2     | Bob     | 20     |
| 3     | Charlie | NULL   |
| 4     | David   | 30     |

### **Table: Departments**

| DeptID | DeptName |
| ------ | -------- |
| 10     | HR       |
| 20     | IT       |
| 30     | Finance  |
| 40     | Sales    |

---

## **🔹 1️⃣ INNER JOIN**

👉 Returns rows where there is a match in both tables.
```
SELECT Employees.EmpID, Employees.EmpName, Departments.DeptName FROM Employees INNER JOIN Departments ON Employees.DeptID = Departments.DeptID;`
```
**🔹 Output:**

| EmpID | EmpName | DeptName |
| ----- | ------- | -------- |
| 1     | Alice   | HR       |
| 2     | Bob     | IT       |
| 4     | David   | Finance  |

---
## **🔹 2️⃣ LEFT JOIN**

👉 Returns **all rows from the left table** and matching rows from the right. If no match, NULL appears.

**🔹 Output:**

| EmpID | EmpName | DeptName |
| ----- | ------- | -------- |
| 1     | Alice   | HR       |
| 2     | Bob     | IT       |
| 3     | Charlie | NULL     |
| 4     | David   | Finance  |

---

## **🔹 3️⃣ RIGHT JOIN**

👉 Returns **all rows from the right table** and matching rows from the left.

**🔹 Output:**

| EmpID | EmpName | DeptName |
| ----- | ------- | -------- |
| 1     | Alice   | HR       |
| 2     | Bob     | IT       |
| 4     | David   | Finance  |
| NULL  | NULL    | Sales    |
|       |         |          |

---

## **🔹 4️⃣ FULL OUTER JOIN (Not Supported in MySQL)**

👉 Returns **all rows from both tables**.

🔴 **MySQL does not support FULL OUTER JOIN directly**, but you can achieve it using **UNION**:
```
SELECT Employees.EmpID, Employees.EmpName, Departments.DeptName FROM Employees LEFT JOIN Departments ON Employees.DeptID = Departments.DeptID UNION SELECT Employees.EmpID, Employees.EmpName, Departments.DeptName FROM Employees RIGHT JOIN Departments ON Employees.DeptID = Departments.DeptID;`
```

---

## **🔹 5️⃣ CROSS JOIN**

👉 Returns **all possible combinations** (Cartesian Product).

**🔹 Output (16 Rows in Total, 4 × 4):**

| EmpName | DeptName |
| ------- | -------- |
| Alice   | HR       |
| Alice   | IT       |
| Alice   | Finance  |
| Alice   | Sales    |
| Bob     | HR       |
| Bob     | IT       |
| Bob     | Finance  |
| Bob     | Sales    |

---

## **🔹 Which Join Should You Use?**

| **Scenario**                               | **Use This Join**               |
| ------------------------------------------ | ------------------------------- |
| Get matching records in both tables        | `INNER JOIN`                    |
| Get all left table records + right matches | `LEFT JOIN`                     |
| Get all right table records + left matches | `RIGHT JOIN`                    |
| Get all records from both tables           | `FULL OUTER JOIN` (Use `UNION`) |
| Combine every row with every row           | `CROSS JOIN`                    |
