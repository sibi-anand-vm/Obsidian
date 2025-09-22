- **Functional Interfaces**: Introduced in Java 8, functional interfaces are interfaces with exactly one abstract method. They enable the use of lambda expressions. The `@FunctionalInterface` annotation can be used to enforce this constraint.
    
- **Marker Interfaces**: These are interfaces with no methods, used to convey metadata or a specific capability to the JVM (e.g., `Serializable` or `Cloneable`).

### Key Features of Functional Interfaces:

1. **Single Abstract Method**: They are also known as Single Abstract Method (SAM) interfaces.
2. **`@FunctionalInterface` Annotation**: This is optional but recommended. It marks an interface as a functional interface and ensures compile-time errors if the interface doesn't adhere to functional interface rules.
3. **Default and Static Methods**: Functional interfaces can also have default or static methods, but they don't affect the single abstract method requirement.

### Examples of Built-in Functional Interfaces:

1. **Runnable**: Contains a single `run()` method.
2. **Callable**: Contains a single `call()` method.
3. **Predicate**: Contains a single `test()` method for evaluating conditions.
4. **Function**: Contains a single `apply()` method for transforming data.
### Sample Code:
#### Custom Functional Interface
```
@FunctionalInterface
interface Calculator {
    int calculate(int a, int b); // Single abstract method
}
public class FunctionalInterfaceExample {
    public static void main(String[] args) {
        // Using a lambda expression
        Calculator addition = (a, b) -> a + b;
        Calculator multiplication = (a, b) -> a * b;

        System.out.println("Addition: " + addition.calculate(5, 3)); // Output: 8
        System.out.println("Multiplication: " + multiplication.calculate(5, 3)); // Output: 15
    }
}
```
**Built-in Functional Interface** 
**Example**
```
import java.util.function.Function;

public class BuiltInFunctionalInterface {
    public static void main(String[] args) {
        // Using Function interface
        Function<String, Integer> stringLength = str -> str.length();

        System.out.println("Length of 'Functional': " + stringLength.apply("Functional")); // Output: 10
    }
}

```
### Benefits of Functional Interfaces:
1. **Supports Lambda Expressions**: Enables functional programming in Java.
2. **Readability**: Simplifies code by reducing boilerplate.
3. **Reusability**: Predefined functional interfaces in `java.util.function` can be reused for various tasks.

## 🔹 What is a Marker Interface?

A **marker interface** is an interface with **no methods or fields** inside it.  
It is simply used to **mark** or **tag** a class with metadata, so the JVM or frameworks can treat those classes differently.

👉 In short: **It gives a "label" to a class without forcing it to implement any method.**

---

## 🔹 Examples of Marker Interfaces in Java

1. **`Serializable`** → tells JVM that this class’s objects can be serialized (converted into byte stream).
    
2. **`Cloneable`** → tells JVM that this class allows cloning via `.clone()`.
    
3. **`Remote`** (in RMI) → marks classes that can be used remotely.

## 🔹 Marker Interfaces vs Annotations

- Before **Java 5**, marker interfaces were widely used.
    
- Now, we mostly use **annotations** (`@Override`, `@FunctionalInterface`, `@Entity`) as they are **more powerful**.
    

---

👉 So, a **marker interface = empty interface used to tag classes for JVM/framework behavior.**

## 🔹 Are annotations MANDATORY?
mandatory?

👉 **No, they are not mandatory.**  
They are optional, but **highly recommended** because they help the compiler catch mistakes.