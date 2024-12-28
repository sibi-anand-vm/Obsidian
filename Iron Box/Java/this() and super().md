- **`this` keyword**: It refers to the current instance of the class. If used in a constructor or method, it refers to the current object of that class. In the constructor, if you use `this()`, it calls the current class's constructor. It’s often used to differentiate between instance variables and parameters when they have the same name.
    
- **`super` keyword**: It is used to refer to the superclass of the current class. If used in a constructor, `super()` calls the superclass constructor. You can also use `super` to access methods and variables from the superclass.
    

Here’s a **sample code** to demonstrate both `this` and `super`:
```
class A {
    A() {
        System.out.println("Constructor of A");
    }

    void display() {
        System.out.println("Display method in class A");
    }
}

class B extends A {
    int num;

    // Constructor of class B
    B() {
        super();  // Calls constructor of A (superclass)
        System.out.println("Constructor of B");
    }

    // Constructor with a parameter
    B(int num) {
        this();  // Calls the constructor of B
        this.num = num;  // Sets the value of the instance variable
    }

    // Method overriding display method of A
    @Override
    void display() {
        super.display();  // Calls display method of A
        System.out.println("Display method in class B");
    }
}

public class Main {
    public static void main(String[] args) {
        B b = new B(10);  // Calls the constructor of class B with parameter
        b.display();  // Calls the overridden display method in class B
    }
}
```
### Explanation:

- **`super()`** in `B` calls the constructor of class `A`.
- **`this()`** in `B(int num)` calls the default constructor of class `B` before assigning the value to the instance variable `num`.
- **`super.display()`** in class `B` calls the `display()` method of class `A` before executing the `display()` method in class `B`.