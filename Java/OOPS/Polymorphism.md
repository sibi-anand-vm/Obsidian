Polymorphism in OOP means "many forms." It allows methods to behave differently based on the parameters passed or the object calling them.

1. **Compile-Time Polymorphism (Method Overloading)**:
    
    - Methods with the same name but different parameters (type, number, or both).
    - The decision of which method to execute is made during compilation.
    - Example: One `add` method for integers and another for floats.
2. **Run-Time Polymorphism (Method Overriding)**:
    
    - A subclass overrides a method in the superclass.
    - The decision of which method to execute is made during runtime based on the object type.

Here's a sample code demonstrating **both types of Polymorphism** in Java:
- **Compile-time Polymorphism** (Method Overloading)
- **Run-time Polymorphism** (Method Overriding)

```
// Parent Class
class Animal {
    // Method to demonstrate Runtime Polymorphism
    public void sound() {
        System.out.println("Animals make sounds");
    }
}

// Child Class
class Dog extends Animal {
    // Overriding the sound method
    @Override
    public void sound() {
        System.out.println("Dogs bark");
    }
}

// Demonstrating Compile-time Polymorphism
class Calculator {
    // Method Overloading: Adding two integers
    public int add(int a, int b) {
        return a + b;
    }

    // Method Overloading: Adding three integers
    public int add(int a, int b, int c) {
        return a + b + c;
    }

    // Method Overloading: Adding two floats
    public float add(float a, float b) {
        return a + b;
    }
}

// Main Class
public class PolymorphismExample {
    public static void main(String[] args) {
        // Runtime Polymorphism
        Animal myAnimal = new Animal();
        Animal myDog = new Dog(); // Reference of Animal, object of Dog

        myAnimal.sound(); // Calls Animal's sound method
        myDog.sound();    // Calls Dog's overridden sound method

        // Compile-time Polymorphism
        Calculator calc = new Calculator();
        System.out.println("Sum of two integers: " + calc.add(5, 10));
        System.out.println("Sum of three integers: " + calc.add(5, 10, 15));
        System.out.println("Sum of two floats: " + calc.add(2.5f, 3.5f));
    }
}
```
This code demonstrates:
1. **Compile-time Polymorphism** using method overloading in the `Calculator` class.
2. **Run-time Polymorphism** using method overriding between `Animal` and `Dog`.