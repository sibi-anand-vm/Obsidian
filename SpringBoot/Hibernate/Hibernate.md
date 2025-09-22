### Definition

Hibernate provides a way to map Java objects (classes, attributes) to database tables and columns, so you can interact with databases using Java objects instead of writing SQL queries directly.

---
### Why it is used

1. **Object–Relational Mapping (ORM):**  
    Converts Java objects into database rows and vice versa automatically.
    
2. **Eliminates Boilerplate JDBC Code:**  
    No need to write repetitive `Connection`, `Statement`, and `ResultSet` handling code.
    
3. **Database Independence:**  
    Works with many databases (MySQL, PostgreSQL, Oracle, etc.) without changing much code.
    
4. **Automatic SQL Generation:**  
    Hibernate generates SQL queries behind the scenes for CRUD (Create, Read, Update, Delete) operations.
    
5. **Caching Support:**  
    Improves performance with first-level (session) and second-level (global) caching.
    
6. **Transaction Management:**  
    Integrates with JTA (Java Transaction API) and Spring to manage transactions reliably.
    
7. **Lazy Loading & Fetching Strategies:**  
    Loads only the data needed, improving performance.
    
---
### Example Flow

- Define a Java class `Student` with fields `id`, `name`, `marks`.
- Map it to a database table `student`.
- Instead of writing `INSERT INTO student ...`, you just do:

```java
Student s = new Student(1, "Jack", 90);
session.save(s);
```

# 🌿 Hibernate Caching

---

## 🔹 What is Caching?
Caching means **storing data temporarily in memory** so that if you need the same data again, Hibernate doesn’t have to go to the database (which is slower).

---

## 🔹 Levels of Cache in Hibernate

### 1️⃣ First-Level Cache (Session Cache)
- Built-in and enabled **by default** ✅  
- Works at the **`Session` object** level  
- If you load the same entity twice in one session, Hibernate fetches it from **memory**, not the DB  

**Example:**
```java
Session session = factory.openSession();

Student s1 = session.get(Student.class, 1); // Query to DB
Student s2 = session.get(Student.class, 1); // Comes from cache, no DB hit
```

### 2️⃣ Second-Level Cache (SessionFactory Cache)

- **Optional** → needs configuration (Ehcache, Infinispan, etc.)
    
- Shared across **multiple sessions**
    
- Useful when many users request the **same data repeatedly**
    
💡 Example: A list of courses accessed by many users can be cached to avoid repeated DB queries.

---
## 🔹 Why is Caching Useful?

- 🚀 **Performance boost** → fewer DB calls
    
- 📉 **Reduced load** on the database
    
- ⚡ **Faster response** → data from memory instead of DB
    
---
## 📝 Summary

- **First-level cache** → per-session (automatic)
    
- **Second-level cache** → across sessions (manual configuration)