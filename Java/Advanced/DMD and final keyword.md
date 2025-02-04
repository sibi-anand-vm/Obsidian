### **Dynamic Method Dispatch**

Dynamic Method Dispatch refers to the process by which a call to an overridden method is resolved at runtime rather than compile time. This mechanism is fundamental to achieving **runtime polymorphism** in Java.

- **How it works**:
    - A superclass reference variable can refer to a subclass object.
    - When a method is called using the reference, the version of the method that corresponds to the object (not the reference) is invoked.
```
class A {
    void display() {
        System.out.println("Display method of Class A");
    }
}

class B extends A {
    @Override
    void display() {
        System.out.println("Display method of Class B");
    }
}

public class Main {
    public static void main(String[] args) {
        A obj = new B(); // Superclass reference, subclass object
        obj.display();   // Calls the display method of Class B
    }
}
```
**Explanation**:

- The reference type (`A`) determines what methods can be accessed at compile time.
- The actual object type (`B`) determines which version of the method is executed at runtime.

---

### **Final Keyword**

The `final` keyword is a modifier in Java that can be applied to variables, methods, and classes.

1. **Final Variable**:
    
    - When a variable is declared `final`, its value cannot be changed once assigned.
    - It is essentially a constant.
    
    **Example**:
```
class A {
    final int MAX_VALUE = 100;

    void display() {
        System.out.println("Max Value: " + MAX_VALUE);
    }
}
```
2.**Final Method**:
- A `final` method cannot be overridden by a subclass.
**Example**:
```
class A {
    final void display() {
        System.out.println("Final Method in Class A");
    }
}

class B extends A {
    // void display() { } // Error: Cannot override the final method
}
```
3.**Final Class**:
- A `final` class cannot be extended (i.e., no subclasses can be created).
**Example**:
```
final class A {
    void display() {
        System.out.println("Final Class");
    }
}

// class B extends A { } // Error: Cannot subclass a final class

```