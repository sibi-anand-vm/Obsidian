# 📘 Java Generics – Methods, Classes & Bounds

Generics in Java allow **type-safe** code that works with different data types without repeating the same logic.

---

## 1️⃣ Generic Class

A class that can hold or operate on any type.

```java
// Generic Class
class Box<T> {
    private T value;

    public void set(T value) {
        this.value = value;
    }

    public T get() {
        return value;
    }
}

public class GenericClassExample {
    public static void main(String[] args) {
        Box<Integer> intBox = new Box<>();
        intBox.set(100);
        System.out.println("Integer Box: " + intBox.get());

        Box<String> strBox = new Box<>();
        strBox.set("Hello Generics");
        System.out.println("String Box: " + strBox.get());
    }
}
```

✅ Output
```
Integer Box: 100
String Box: Hello Generics
```

---

## 2️⃣ Generic Method

A method that can accept any type as a parameter.

```java
class GenericMethodExample {
    // Generic Method
    public static <T> void printArray(T[] arr) {
        for (T element : arr) {
            System.out.print(element + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Integer[] intArr = {1, 2, 3};
        String[] strArr = {"A", "B", "C"};

        printArray(intArr); // prints: 1 2 3
        printArray(strArr); // prints: A B C
    }
}
```

✅ Output
```
1 2 3 
A B C
```

---

## 3️⃣ Bounded Generics

Restricts the type parameter to a specific class or its subclasses.

```java
// Only accepts Number or its subclasses
class Calculator<T extends Number> {
    private T num;

    public Calculator(T num) {
        this.num = num;
    }

    public double square() {
        return num.doubleValue() * num.doubleValue();
    }
}

public class BoundedGenericsExample {
    public static void main(String[] args) {
        Calculator<Integer> intCalc = new Calculator<>(5);
        System.out.println("Square of 5: " + intCalc.square()); // 25.0

        Calculator<Double> doubleCalc = new Calculator<>(3.5);
        System.out.println("Square of 3.5: " + doubleCalc.square()); // 12.25

        // ❌ Not allowed: String is not a subclass of Number
        // Calculator<String> strCalc = new Calculator<>("Hi");
    }
}
```

✅ Output
```
Square of 5: 25.0
Square of 3.5: 12.25
```

---

## ⚡ Summary

- **Generic Class** → `class Box<T> { ... }`  
- **Generic Method** → `<T> void methodName(T param)`  
- **Bounded Generics** → `<T extends Number>` restricts to Numbers only  

✔️ Helps write **reusable, flexible, and type-safe** code.
    
