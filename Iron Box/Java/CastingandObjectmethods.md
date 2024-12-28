### ==**Upcasting and Downcasting**==

- **Upcasting**: Casting a subclass reference to a superclass type.
- **Downcasting**: Casting a superclass reference to a subclass type.

**Example**:
```
class A {
    void display() {
        System.out.println("Display method of Class A");
    }
}

class B extends A {
    void show() {
        System.out.println("Show method of Class B");
    }
}

public class Main {
    public static void main(String[] args) {
        A obj = new B();  // Upcasting
        obj.display();

        B obj2 = (B) obj;  // Downcasting
        obj2.show();
    }
}
```
### **Object Class Methods**

The `Object` class in Java is the root of the class hierarchy. Every class in Java is a subclass of `Object`. Key methods:

1. **equals()**: Compares two objects for equality.
2. **toString()**: Returns a string representation of the object.
3. **hashCode()**: Returns the hash code value of the object.
```
class A {
    int x;

    A(int x) {
        this.x = x;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        A a = (A) obj;
        return x == a.x;
    }
    public String toString() {
        return "A{x=" + x + "}";
    }
}

public class Main {
    public static void main(String[] args) {
        A obj1 = new A(10);
        A obj2 = new A(10);

        System.out.println(obj1.equals(obj2)); // true
        System.out.println(obj1.toString());  // A{x=10}
    }
}

```