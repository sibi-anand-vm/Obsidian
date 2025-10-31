# 🧩 Singleton Pattern — Why Constructor is Private

## 🎯 Goal
Ensure that **only one instance** of a class exists in the entire application and provide a **global access point** to it.

---

## 🚫 Why the Constructor is NOT Public
If the constructor were **public**, anyone could create new objects:

```java
DatabaseConnection db1 = new DatabaseConnection();
DatabaseConnection db2 = new DatabaseConnection();
```

➡️ This breaks the **Singleton rule** — multiple instances would exist.

---

## ✅ Why the Constructor is **Private**
When we write:

```java
private DatabaseConnection() { }
```

It means:
> Only this class itself can create an object of it.

No other class can use the `new` keyword.

Thus, the object can only be created **inside** the class, usually via a static method like `getInstance()`.

---

## 🧱 Full Example
```java
public class DatabaseConnection {
    private static DatabaseConnection instance;

    // Private constructor prevents external instantiation
    private DatabaseConnection() { }

    // Static method to control object creation
    public static DatabaseConnection getInstance() {
        if (instance == null) {
            instance = new DatabaseConnection(); // Create only once
        }
        return instance;
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        DatabaseConnection db1 = DatabaseConnection.getInstance();
        DatabaseConnection db2 = DatabaseConnection.getInstance();

        System.out.println(db1 == db2); // true ✅ same object
    }
}
```

---

## 🧠 Summary

| Access Modifier | Who Can Call `new`? | Effect in Singleton |
|------------------|---------------------|----------------------|
| **public** | Everyone | ❌ Multiple objects created |
| **private** | Only inside the class | ✅ Only one object created |
| **protected** | Same package or subclass | ⚠️ Still unsafe |
| **default** | Same package only | ⚠️ Still unsafe |

---

## ⚙️ In Short
> **Constructor is private** → prevents direct object creation → enforces one instance → **core rule of Singleton**.
