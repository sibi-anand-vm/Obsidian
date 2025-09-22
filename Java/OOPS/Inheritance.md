Inheritance is a mechanism in object-oriented programming where one class (child class or subclass) can derive properties and methods from another class (parent class or superclass). It helps in code reusability and establishing a relationship between classes.

- **Single-Level Inheritance**: A class (B) extends only one base class (A). Example: `Class B extends Class A`.
    
- **Multi-Level Inheritance**: A class (C) extends another derived class (B), and that class (B) extends a base class (A). Here, class C inherits properties of both A and B. Example: `Class C extends Class B`, and `Class B extends Class A`.
    
- **Multiple Inheritance**: A class tries to extend more than one class (A and B), which is not allowed in Java due to ambiguity (which method to call). Java does not support multiple inheritance with classes. Example: `Class C extends Class A, Class B` (This is not allowed in Java).
    
- **Hybrid Inheritance**: This is a combination of multiple types of inheritance (e.g., a mix of multiple inheritance and other forms). Since Java does not support multiple inheritance with classes, hybrid inheritance is not possible in Java.
    
- **Hierarchical Inheritance**: Multiple classes (B, C) extend a single base class (A), sharing the base class's properties. Example: `Class B extends Class A` and `Class C extends Class A`.

```
// Single-level Inheritance: Class B extends Class A
class A {
    public void displayA() {
        System.out.println("This is Class A - Single-level Inheritance");
    }
}

class B extends A {
    public void displayB() {
        System.out.println("This is Class B - Single-level Inheritance");
    }
}

// Multi-level Inheritance: Class C extends Class B, which extends Class A
class C extends B {
    public void displayC() {
        System.out.println("This is Class C - Multi-level Inheritance");
    }
}

// Hierarchical Inheritance: Multiple classes extending the same parent class
class D extends A {
    public void displayD() {
        System.out.println("This is Class D - Hierarchical Inheritance");
    }
}

class E extends A {
    public void displayE() {
        System.out.println("This is Class E - Hierarchical Inheritance");
    }
}

public class InheritanceExample {
    public static void main(String[] args) {
        // Single-level Inheritance
        B objB = new B();
        objB.displayA();
        objB.displayB();

        System.out.println();

        // Multi-level Inheritance
        C objC = new C();
        objC.displayA();
        objC.displayB();
        objC.displayC();

        System.out.println();

        // Hierarchical Inheritance
        D objD = new D();
        objD.displayA();
        objD.displayD();

        E objE = new E();
        objE.displayA();
        objE.displayE();
    }
}

```
Java designers (James Gosling & team) avoided it mainly because of the **Diamond Problem**.

### 🔹 Java’s Approach

To avoid this confusion:
- **Classes** in Java support **single inheritance only**.
- But **Interfaces** can be inherited from **multiple sources**.
### 🔹 Multiple Inheritance with Interfaces (Safe)
```
interface A {
    default void show() { System.out.println("From A"); }
}

interface B {
    default void show() { System.out.println("From B"); }
}

class C implements A, B {
    // Must resolve conflict manually
    public void show() {
        A.super.show(); // explicitly calling A's show
        B.super.show(); // explicitly calling B's show
    }
}

public class Test {
    public static void main(String[] args) {
        C obj = new C();
        obj.show();
    }
}
```

### 🔑 Summary

- **No multiple inheritance for classes** → to avoid ambiguity, complexity, and simplify design.
    
- **Yes for interfaces** → Java allows multiple inheritance of interfaces, and ambiguity must be resolved explicitly.