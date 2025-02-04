## What are Java Exceptions?

****In Java, Exception**** is an unwanted or unexpected event, which occurs during the execution of a program, i.e. at run time, that disrupts the normal flow of the program’s instructions. Exceptions can be caught and handled by the program. When an exception occurs within a method, it creates an object. This object is called the exception object. It contains information about the exception, such as the name and description of the exception and the state of the program when the exception occurred.
### ****Major reasons why an exception Occurs****

- Invalid user input
- Device failure
- Loss of network connection
- Physical limitations (out-of-disk memory)
- Code errors
- Out of bound
- Null reference
- Type mismatch
- Opening an unavailable file
- Database errors
- Arithmetic errors

****Errors**** represent irrecoverable conditions such as Java virtual machine (JVM) running out of memory, memory leaks, stack overflow errors, library incompatibility, infinite recursion, etc. Errors are usually beyond the control of the programmer, and we should not try to handle errors.
### Difference between Error and Exception
Let us discuss the most important part which is the ****differences between Error and Exception**** that is as follows: 
- ****Error:**** An Error indicates a serious problem that a reasonable application should not try to catch.
- ****Exception:**** Exception indicates conditions that a reasonable application might try to catch.
### Exception Hierarchy

All exception and error types are subclasses of the class ****Throwable****, which is the base class of the hierarchy. One branch is headed by ****Exception****. This class is used for exceptional conditions that user programs should catch. NullPointerException is an example of such an exception. Another branch, ****Error**** is used by the Java run-time system([JVM](https://www.geeksforgeeks.org/jvm-works-jvm-architecture/)) to indicate errors having to do with the run-time environment itself(JRE). StackOverflowError is an example of such an error.
![[Pasted image 20241230152331.png]]
## Types of Exceptions
Java defines several types of exceptions that relate to its various class libraries. Java also allows users to define their own exceptions.

![Types of Exceptions in Java](https://media.geeksforgeeks.org/wp-content/uploads/20240730174225/Exceptions-in-Java-1-768.webp)

****Exceptions can be categorized in two ways:****

1. ****Built-in Exceptions****  
    - Checked Exception
    - Unchecked Exception 
2. ****User-Defined Exceptions****
### ****1. Built-in Exceptions****

Built-in exceptions are the exceptions that are available in Java libraries. These exceptions are suitable to explain certain error situations.

- ****Checked Exceptions:**** Checked exceptions are called compile-time exceptions because these exceptions are checked at compile-time by the compiler.  
     
- ****Unchecked Exceptions:**** The unchecked exceptions are just opposite to the checked exceptions. The compiler will not check these exceptions at compile time. In simple words, if a program throws an unchecked exception, and even if we didn’t handle or declare it, the program would not give a compilation error.
### ****2. User-Defined Exceptions:****
Sometimes, the built-in exceptions in Java are not able to describe a certain situation. In such cases, users can also create exceptions, which are called ‘user-defined Exceptions’. 
The _****advantages of Exception Handling in Java****_ are as follows:
1. Provision to Complete Program Execution
2. Easy Identification of Program Code and Error-Handling Code
3. Propagation of Errors
4. Meaningful Error Reporting
5. Identifying Error Types

****Methods to print the Exception information:****
#### ****1. printStackTrace()****
This method prints exception information in the format of the Name of the exception: description of the exception, stack trace.
#### 2.****getMessage()**** 
The getMessage() method prints only the description of the exception.

## Here’s a summary of the five topics you’ve covered
1. **Exception Handling Basics:**  
    Exceptions are unexpected events during runtime that disrupt normal program flow. The `try` block contains code that might throw exceptions, `catch` handles specific exceptions, and `finally` ensures certain statements execute regardless of exceptions. Types of exceptions include runtime and logical exceptions (e.g., `ArithmeticException`, `IOException`).
    
2. **BufferedReader and Scanner Classes:**  
    `BufferedReader` (with `InputStreamReader`) is an older way to read user input, requiring conversion for numeric types. The `Scanner` class is simpler, with methods like `nextInt()` or `nextLine()` to read inputs directly.
    
3. **`throws` and `throw`:**
    
    - `throw` is used to explicitly throw an exception in a method, often based on a condition.
    - `throws` is used to declare that a method might throw exceptions, allowing the calling method to handle them.
4. **Custom Exceptions:**  
    Developers can create custom exceptions by extending `Exception` or `RuntimeException`. This allows handling specific cases not covered by standard exceptions.
    
5. **Exceptions in Inheritance:**  
    When overriding methods in a subclass, the exceptions thrown must either match or be subclasses of the parent method's exceptions. This maintains compatibility in the inheritance hierarchy.

Some of sample code for reference
**1.Try catch finally blocks**
```
public class ExceptionExample {
    public static void main(String[] args) {
        try {
            int result = 10 / 0; // This will throw an ArithmeticException
        } catch (ArithmeticException e) {
            System.out.println("Caught an ArithmeticException: " + e.getMessage());
        } finally {
            System.out.println("Finally block always executes.");
        }
    }
}

```
**2.Throw and Throws keyword**
```
class CustomException extends Exception {
    public CustomException(String message) {
        super(message);
    }
}

public class ThrowsThrowExample {
    public static void validateAge(int age) throws CustomException {
        if (age < 18) {
            throw new CustomException("Age must be 18 or above.");
        }
        System.out.println("Valid age!");
    }

    public static void main(String[] args) {
        try {
            validateAge(16);
        } catch (CustomException e) {
            System.out.println("Caught exception: " + e.getMessage());
        }
    }
}

```
**3.BufferedReader and Scanner**
```
import java.io.*;
import java.util.Scanner;

public class InputExample {
    public static void main(String[] args) throws IOException {
        // Using BufferedReader
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        System.out.println("Enter a number using BufferedReader:");
        int num1 = Integer.parseInt(br.readLine());
        System.out.println("You entered: " + num1);

        // Using Scanner
        Scanner scanner = new Scanner(System.in);
        System.out.println("Enter another number using Scanner:");
        int num2 = scanner.nextInt();
        System.out.println("You entered: " + num2);

        scanner.close();
    }
}

```
4. **Exceptions in Inheritance:**
```
class ParentClass {
    public void display() throws IOException {
        System.out.println("Parent class method.");
    }
}

class ChildClass extends ParentClass {
    @Override
    public void display() throws FileNotFoundException { // Subclass of IOException
        System.out.println("Child class method.");
    }
}

public class InheritanceExceptionExample {
    public static void main(String[] args) {
        ParentClass obj = new ChildClass();
        try {
            obj.display();
        } catch (IOException e) {
            System.out.println("Caught exception: " + e.getMessage());
        }
    }
}
```