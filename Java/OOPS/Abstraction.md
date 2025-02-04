### ==**Abstract Keyword**==

The `abstract` keyword is used to define a class or method that must be implemented in its subclass.

- **Abstract Class**: Cannot be instantiated.
- **Abstract Method**: Declared without a body.

**Example**:
```
abstract class A {
    abstract void display();

    void show() {
        System.out.println("Non-abstract method in abstract class");
    }
}

class B extends A {
    @Override
    void display() {
        System.out.println("Display method in Class B");
    }
}

public class Main {
    public static void main(String[] args) {
        B obj = new B();
        obj.display();
        obj.show();
    }
}

```