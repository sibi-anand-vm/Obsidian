# 📌 PreparedStatement in Java (JDBC)

### 🔹 What is `PreparedStatement`?

- `PreparedStatement` is an **interface** in JDBC (extends `Statement`).
- It is used to **execute parameterized SQL queries** (queries with `?` placeholders).
- Unlike `Statement`, it **precompiles the SQL query** once and reuses it → better performance.
    
---
📒 **Notes: Why use `PreparedStatement`?**

- Prevents **SQL Injection** ✅
- Allows **dynamic queries** with placeholders (`?`)
- More **efficient** (compiled once, executed many times)
- Methods:
    - `setInt(index, value)`
    - `setString(index, value)`
    - `setDouble(index, value)`
    - `executeQuery()` → SELECT
    - `executeUpdate()` → INSERT, UPDATE, DELETE

```java

String insertQuery = "INSERT INTO student VALUES(?,?,?)";
PreparedStatement st = conn.prepareStatement(insertQuery);

st.setInt(1, 5);         // sid
st.setString(2, "User5"); // sname
st.setDouble(3, 8.6);    // cgpa

int rows = st.executeUpdate();
System.out.println("Rows inserted: " + rows);
    
```

|Feature|**Statement**|**PreparedStatement**|
|---|---|---|
|**Definition**|Used to execute static SQL queries.|Used to execute **precompiled parameterized SQL queries**.|
|**SQL Injection**|❌ Vulnerable (user input can be injected).|✅ Safe (placeholders `?` prevent injection).|
|**Parameters**|No support for parameters – query must be built as a string.|Supports parameters using `?` and `setXXX()` methods.|
|**Performance**|Query is compiled **every time** it runs.|Query is **compiled once**, reused → faster for repeated executions.|
|**Use Case**|Good for simple, one-time queries.|Best for dynamic queries and repeated executions (e.g., batch inserts).|
|**Code Complexity**|More prone to messy string concatenations.|Cleaner, more readable, easier to maintain.|
|**Execution Methods**|`executeQuery()`, `executeUpdate()`, `execute()`|Same methods, but work with bound parameters.|