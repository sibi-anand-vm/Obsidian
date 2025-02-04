Constructors are special methods in Java used to initialize objects of a class.
- The constructor name must match the class name.
- They do not have a return type.
- They are called automatically when an object of the class is created.
- Constructor overloading allows multiple constructors with different parameter lists in the same class.
### ==Sample Code:==
```
class Person {
    String name;
    int age;

    // Default constructor
    Person() {
        name = "Unknown";
        age = 0;
    }

    // Parameterized constructor
    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    void displayInfo() {
        System.out.println("Name: " + name + ", Age: " + age);
    }
}

public class ConstructorExample {
    public static void main(String[] args) {
        // Using default constructor
        Person person1 = new Person();
        person1.displayInfo();

        // Using parameterized constructor
        Person person2 = new Person("Alice", 25);
        person2.displayInfo();
    }
}

```