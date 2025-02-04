## ==Variables in Interface==
- Variables in interfaces are defaultly final and static.It need to there initialised there itself  and cannot be overridden.
## ==Methods in Interfaces:==

- **Definition**: Interfaces in Java allow achieving 100% abstraction. They contain method declarations without implementations.
- **Implementation**: A class implementing an interface must provide implementations for all its methods.
- **Usage**:
    - Define method declarations in an interface.
    - Implement these methods in a class using the `implements` keyword.
    - Access methods via a reference to the interface but instantiated using the implementing class.
- **Inheritance**:
    - Classes use `extends` to inherit other classes but use `implements` to adopt interfaces.
    - Multiple inheritance is supported by implementing multiple interfaces simultaneously.
    - The implementing class must provide implementations for all methods of all inherited interfaces.
- **Example**:
    - If `class C` implements `interface A` and `interface B`, it must define methods for both `A` and `B`.
    - References to interfaces restrict access to methods specific to that interface.
```
// Define Interface A
interface A {
    void methodA();
}

// Define Interface B
interface B {
    void methodB();
}

// Class C implements both Interface A and Interface B
class C implements A, B {
    // Implement method from Interface A
    public void methodA() {
        System.out.println("Method A from Interface A is implemented.");
    }

    // Implement method from Interface B
    public void methodB() {
        System.out.println("Method B from Interface B is implemented.");
    }
}

// Main class
public class InterfaceExample {
    public static void main(String[] args) {
        // Create an object of Class C
        C obj = new C();

        // Use Interface A's reference to call methodA
        A aRef = obj;
        aRef.methodA();

        // Use Interface B's reference to call methodB
        B bRef = obj;
        bRef.methodB();
    }
}

```