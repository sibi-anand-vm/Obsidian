### ==The `static` Keyword in Java==

The `static` keyword in Java is used for memory management and applies to variables, methods, blocks, and nested classes. Static members belong to the **class** rather than any specific instance of the class. This means you can access them without creating an object of the class.

### <mark style="background: #ADCCFFA6;">Key Points:</mark>

1. **Static Variable**:
    
    - Shared among all instances of a class.
    - Memory is allocated once at the class level.
2. **Static Method**:
    
    - Can be called without creating an instance of the class.
    - Cannot access non-static variables or methods directly.
3. **Static Block**:
    
    - Used to initialize static variables.
    - Executed when the class is loaded into memory.
4. **Static Nested Class**:
    
    - A nested class declared static.
    - Does not require an instance of the outer class to be instantiated.
### ==Key Takeaways:==

1. **Static methods cannot directly access non-static members.**
2. **Non-static methods can access both static and non-static members.**
3. To use non-static members inside a static method, you must create an object.

```
class StaticExample {
    // Static variable
    static int staticCounter = 0;

    // Instance variable
    int instanceCounter = 0;

    // Static block
    static {
        System.out.println("Static block executed.");
        staticCounter = 100; // Initializing static variable
    }

    // Static method
    static void staticMethod() {
        System.out.println("Static method called. StaticCounter: " + staticCounter);
        // System.out.println(instanceCounter); // Error: Cannot access non-static variable
    }

    // Instance method
    void instanceMethod() {
        instanceCounter++;
        staticCounter++;
        System.out.println("Instance method called. InstanceCounter: " + instanceCounter + ", StaticCounter: " + staticCounter);
    }

    // Static nested class
    static class NestedStaticClass {
        void display() {
            System.out.println("Inside static nested class. StaticCounter: " + staticCounter);
        }
    }
}

public class StaticKeywordDemo {
    public static void main(String[] args) {
        // Access static method and variable without creating an instance
        StaticExample.staticMethod();
        System.out.println("StaticCounter from main: " + StaticExample.staticCounter);

        // Creating instances
        StaticExample obj1 = new StaticExample();
        StaticExample obj2 = new StaticExample();

        obj1.instanceMethod();
        obj2.instanceMethod();

        // Accessing static nested class
        StaticExample.NestedStaticClass nestedObj = new StaticExample.NestedStaticClass();
        nestedObj.display();
    }
}

```
Static blocks will get executed only if class if loaded and executed only once in a program irrespective of how many blocks created.
### When Does a Class Get Loaded?

1. **When an Instance is Created**:  
    If you create an object of the class:
```
	 MyClass obj = new MyClass();
```    
2. **When a Static Member is Accessed**:  
    Accessing a static variable or method of the class:    
``` 
	MyClass.staticMethod(); System.out.println(MyClass.staticVariable);
```
3. **When the Class is Explicitly Referenced**:  
    Using reflection or calling `Class.forName()`:
```
	Class<?> clazz = Class.forName("MyClass");
```
4. **When It’s the Main Class**:  
    If the class contains the `main` method and is the entry point of the program:
```
	public static void main(String[] args) {     // Class is loaded here }
```