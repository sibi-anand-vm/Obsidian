# Spring Dependency Injection (DI)

Spring uses **Inversion of Control (IoC)** with **Dependency Injection (DI)** to manage objects (beans).  
Instead of manually creating objects with `new`, Spring automatically creates and wires them.

---

## 🔹 3 Common Types of Dependency Injection

### 1. Constructor Injection

- Dependencies are passed through the **class constructor**.
    
- Recommended in **modern Spring Boot apps**.
    
- Enforces that dependencies must be present at object creation.
    

#### Example
```java
@Service
public class OrderService {

    private final PaymentService paymentService;

    // Spring injects PaymentService here
    public OrderService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}
```

✅ Pros
- Mandatory dependencies are enforced at object creation.
- Encourages **immutability** (fields can be `final`).
- Great for **unit testing**.
❌ Cons
- Constructor becomes **bloated** if there are too many dependencies.
---
### 2. Setter Injection

- Dependencies are injected via **setter methods**.
**Example**:
```java
@Service
public class OrderService {

    private PaymentService paymentService;

    @Autowired
    public void setPaymentService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}
```

✅ Pros
- Good for **optional dependencies**.
- Dependency can be changed after object creation.
❌ Cons
- Object may be in an **incomplete state** if setter not called.
- More **boilerplate code** (getters/setters).
---
### 3. Field Injection

- Dependencies are injected **directly into fields** using `@Autowired`.
```java
@Service
public class OrderService {

    @Autowired
    private PaymentService paymentService;
}

```

| Injection Type  | Pros 🚀                                          | Cons ⚠️                                    | Best Use Case              |
| --------------- | ------------------------------------------------ | ------------------------------------------ | -------------------------- |
| **Constructor** | Immutable, test-friendly, required deps enforced | Large constructors if too many deps        | ✅ Preferred in Spring Boot |
| **Setter**      | Flexible, good for optional deps                 | Object may be incomplete, more code        | Optional dependencies      |
| **Field**       | Simple, less code                                | Hidden deps, hard to test, no immutability | Quick prototypes/POCs      |
|                 |                                                  |                                            |                            |

## 🏆 Recommendation

- Use **Constructor Injection** for most cases.
- Use **Setter Injection** for optional dependencies.
- Avoid **Field Injection** in production code.