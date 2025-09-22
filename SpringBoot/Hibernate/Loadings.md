## 🚌 Analogy: Bus Ticket Example

1. **`get()` → Buy and Check Immediately**
    - You go to the counter and **ask for ticket #1**.
    - The clerk **immediately checks the system**:
        - If ticket exists → you get it.
        - If not → clerk says **“not available”** (`null`).
            
2. **`load()` → Take a Placeholder Ticket**
    - You go to the counter and ask for ticket #2.        
    - The clerk **gives you a blank placeholder ticket** (proxy).
    - Only **when you actually try to sit on the bus** → the system checks if ticket exists.
        - If ticket exists → you get real details.    
        - If not → **clerk throws an error** (`ObjectNotFoundException`).
            

## 🔎 In Hibernate

### Using `get()`
```java
Student s1 = ss.get(Student.class, 1);  // hits DB immediately
if (s1 != null) {
    System.out.println(s1.getAname());  // data already there
} else {
    System.out.println("No student with id=1");
}
```
👉 DB is queried **immediately**. If record doesn’t exist → `s1 == null`.

#### Using `load()`
```java
Student s2 = ss.load(Student.class, 1); // NO DB query yet!
System.out.println("Proxy created...");

// Now we touch a field
System.out.println(s2.getAname());  // DB query happens NOW
```
👉 DB query happens **only when you use it**.  
If record doesn’t exist → `ObjectNotFoundException`.

**Key Features**

| Feature               | `get()` ✅                     | `load()` ⚡                       |
| --------------------- | ----------------------------- | -------------------------------- |
| Query executed        | Immediately                   | Delayed until field accessed     |
| Missing record result | Returns `null`                | Throws `ObjectNotFoundException` |
| Performance           | Slower if you don’t need data | Faster if you might not use data |
| Proxy object          | No                            | Yes                              |
