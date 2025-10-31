# 🏭 Factory Pattern — Overview

## 🎯 Goal
Define an **interface for creating objects**, but let subclasses decide which class to instantiate.  
Decouples object creation from the client.

---

## 🔹 Why Use Factory
- When you have a **superclass with multiple subclasses**.  
- You want to **decide at runtime** which subclass to create.  
- Centralizes creation logic, reducing code duplication.

---

## 🧱 Example
```java
// Interface
interface Shape {
    void draw();
}

// Concrete classes
class Circle implements Shape {
    public void draw() { System.out.println("Drawing Circle"); }
}
class Square implements Shape {
    public void draw() { System.out.println("Drawing Square"); }
}

// Factory class
class ShapeFactory {
    public Shape getShape(String type) {
        if (type == null) return null;
        if (type.equalsIgnoreCase("CIRCLE")) return new Circle();
        else if (type.equalsIgnoreCase("SQUARE")) return new Square();
        return null;
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        ShapeFactory factory = new ShapeFactory();
        Shape shape1 = factory.getShape("CIRCLE");
        shape1.draw(); // Drawing Circle
    }
}
```

---

## ⚙️ Summary
| Feature | Factory Pattern |
|---------|----------------|
| Purpose | Encapsulate object creation |
| Client code | Decoupled from concrete classes |
| Use cases | DAO creation, Shape/Widget factories |

---
