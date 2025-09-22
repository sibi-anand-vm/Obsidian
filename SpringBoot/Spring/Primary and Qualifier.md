## 1️⃣ Solution – `@Primary`

- Marks a bean as the **default choice** when multiple candidates exist.
```java
@Component
@Primary
public class Laptop implements Computer {
    public void compile() {
        System.out.println("Laptop compiling...");
    }
}
```

```java
@Component
public class Developer {
    @Autowired
    private Computer com; // ✅ Laptop will be injected by default
}
```
## 2️⃣ Solution – `@Qualifier`

- Used to **specify exactly which bean** to inject.
- Works at **field, constructor, or setter** level.

```java
@Component
public class Developer {

    @Autowired
    @Qualifier("desktop")  // bean name = class name with lowercase first letter
    private Computer com;

    public void build() {
        com.compile();
        System.out.println("Hi guys. I am developer");
    }
}

```