In **Java**, a **Bean** is a reusable software component that follows specific conventions. The term is widely used in **JavaBeans** and **Spring Beans**.

---
### 1️⃣ **JavaBean**

A **JavaBean** is a simple Java class that follows these rules: ✔️ Has a **public no-argument constructor**  
✔️ Provides **getter and setter** methods to access private fields  
✔️ Implements **Serializable** (optional but recommended)

### 2️⃣ **Spring Bean**

In the **Spring Framework**, a **Bean** is an object managed by the Spring **IoC (Inversion of Control) Container**.  
It is typically defined using **@Component, @Service, @Repository**, or **@Bean** annotations.

### **Key Differences:**

| Feature       | JavaBean                                | Spring Bean                                     |
| ------------- | --------------------------------------- | ----------------------------------------------- |
| Purpose       | Reusable component with getters/setters | Managed object in Spring framework              |
| Constructor   | No-argument required                    | No strict requirement                           |
| Instantiation | Manually via `new`                      | Spring manages it                               |
| Configuration | No framework needed                     | Configured via XML, Annotations, or Java Config |

---

### **Summary**

- **JavaBean** = Simple, reusable Java class with getters/setters
- **Spring Bean** = Object managed by the Spring container