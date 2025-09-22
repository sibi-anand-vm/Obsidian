# Spring Boot Notes – Dependency Injection with Interface

---

## 🌱 Key Concepts

1. **Interface-based DI**
   - We code to an **interface** (`Computer`), not to a specific implementation (`Laptop` / `Desktop`).
   - This makes the code **loosely coupled** and **flexible**.

2. **@Autowired**
   - Spring automatically **injects a bean** of type `Computer` into `Developer`.
   - Since `Laptop` is annotated with `@Component`, Spring will use it by default.

3. **Multiple Implementations**
   - If multiple beans implement the same interface (e.g., `Laptop` and `Desktop`), Spring needs clarification.
   - This can be handled using:
     - `@Primary` → default bean.
     - `@Qualifier` → specify which bean to inject.

---

## 🚀 Code Recap

### `Computer.java` (Interface)
```java
public interface Computer {
    void compile();
}
```

Laptop.java
```java
@Component
public class Laptop implements Computer {
    public void compile() {
        System.out.println("Compiling");
    }
}

```

Desktop.java
```java
public class Desktop implements Computer {
    public void compile() {
        System.out.println("Compiling");
    }
}
```

Developer.java
```
@Component
public class Developer {

    @Autowired
    private Computer com; // IoC container injects Laptop (default bean)

    public void build() {
        com.compile();
        System.out.println("Hi guys. I am developer");
    }
}

```

## 🔑 Flow of Execution

1. Spring Boot app starts → IoC container (`ApplicationContext`) is created.
2. Spring scans for `@Component` beans.
    
    - Finds `Laptop` and `Developer`.
    - Creates beans for them.
        
3. In `Developer`, Spring sees `@Autowired private Computer com;`
    
    - `Laptop` implements `Computer` → injected automatically.
        
4. When `Developer.build()` is called:
    
    - `Laptop.compile()` runs → prints `"Compiling"`.
    - Then prints `"Hi guys. I am developer"`.