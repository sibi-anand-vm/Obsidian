
Java supports different **types of classes** based on their definition, purpose, and usage.

---
## 1. Concrete Class
- A normal class with fully defined methods.
- You can create objects of it.

```java
class Car {
    void drive() {
        System.out.println("Car is driving...");
    }
}

public class Test {
    public static void main(String[] args) {
        Car c = new Car();  // ✅ object creation allowed
        c.drive();
    }
}
```

---

## 2. Abstract Class
- Declared with `abstract` keyword.
- May contain **abstract methods** (without body).
- Cannot be instantiated directly.
- Used for **partial abstraction**.

```java
abstract class Shape {
    abstract void draw(); // abstract method
    void info() { // concrete method
        System.out.println("This is a shape.");
    }
}

class Circle extends Shape {
    void draw() {
        System.out.println("Drawing Circle...");
    }
}

public class Test {
    public static void main(String[] args) {
        Shape s = new Circle(); // upcasting
        s.draw();
        s.info();
    }
}
```

---

## 3. Final Class
- Declared with `final` keyword.
- Cannot be **inherited**.
- Used for **security and immutability**.

```java
final class Bank {
    void display() {
        System.out.println("Secure Bank");
    }
}

// ❌ class MyBank extends Bank { }  // Error: cannot subclass final class
```

---

## 4. Static Nested Class
- A **class inside another class** marked as `static`.
- Can only access **static members** of the outer class.
- Does **not** require an outer class object.

```java
class Outer {
    static class Inner {
        void show() {
            System.out.println("Inside static nested class");
        }
    }

    public static void main(String[] args) {
        Outer.Inner obj = new Outer.Inner(); // no outer object needed
        obj.show();
    }
}
```

---

## 5. Inner Class (Non-static Nested Class)
- Defined inside another class.
- Can access **all members** of the outer class.
- Requires an **outer class object** to create an instance.

```java
class Outer {
    class Inner {
        void show() {
            System.out.println("Inside inner class");
        }
    }

    public static void main(String[] args) {
        Outer outer = new Outer();
        Outer.Inner inner = outer.new Inner();
        inner.show();
    }
}
```

---

## 6. Local Inner Class
- Defined inside a **method** or block.
- Scope limited to that method.
- Can access **final or effectively final** variables of the method.

```java
class Outer {
    void display() {
        int x = 10; // effectively final
        class Local {
            void msg() {
                System.out.println("Local inner class value: " + x);
            }
        }
        Local obj = new Local();
        obj.msg();
    }

    public static void main(String[] args) {
        Outer outer = new Outer();
        outer.display();
    }
}
```

---

## 7. Anonymous Inner Class
- Class **without a name**.
- Used for **one-time implementation** of abstract classes or interfaces.

```java
abstract class Animal {
    abstract void sound();
}

public class Test {
    public static void main(String[] args) {
        Animal dog = new Animal() { // anonymous inner class
            void sound() {
                System.out.println("Woof Woof!");
            }
        };
        dog.sound();
    }
}
```

---

## 8. POJO Class (Plain Old Java Object)
- Simple class with **fields, getters, setters, constructors**.
- No business logic.
- Often used in frameworks like Hibernate, Spring.

```java
class Student {
    private String name;
    private int age;

    // Constructor
    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Getters
    public String getName() { return name; }
    public int getAge() { return age; }
}
```

---

## 9. Singleton Class
- A class that allows **only one object** to be created.
- Useful for **resources like DB connection, config classes**.

```java
class Singleton {
    private static Singleton instance;

    private Singleton() {} // private constructor

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}

public class Test {
    public static void main(String[] args) {
        Singleton s1 = Singleton.getInstance();
        Singleton s2 = Singleton.getInstance();
        System.out.println(s1 == s2); // true ✅
    }
}
```

---

## 🔑 Summary Table

| Class Type             | Key Point                                      |
|------------------------|-----------------------------------------------|
| Concrete               | Normal class (can create objects)             |
| Abstract               | Partial abstraction, cannot instantiate       |
| Final                  | Cannot be inherited                            |
| Static Nested          | Nested with `static` keyword                  |
| Inner (Non-static)     | Access outer class members                     |
| Local Inner            | Defined inside a method                        |
| Anonymous Inner        | One-time class without name                    |
| POJO                   | Simple data container                          |
| Singleton              | Only one instance allowed                       |
