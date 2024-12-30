****Lambda expressions in Java****, introduced in Java SE 8, represent instances of functional interfaces (interfaces with a single abstract method). They provide a concise way to express instances of single-method interfaces using a block of code.
## Functionalities of Lambda Expression in Java
Lambda Expressions implement the only abstract function and therefore implement functional interfaces lambda expressions are added in Java 8 and provide the below functionalities.
- ****Functional Interfaces****: Lambda expressions implement single abstract methods of functional interfaces.
- ****Code as Data****: Treat functionality as a method argument.
- ****Class Independence****: Create functions without defining a class.
- ****Pass and Execute****: Pass lambda expressions as objects and execute on demand.

Lambda expressions allow for cleaner and more efficient code, especially in functional programming. 
## Lambda Expression Syntax
```
lambda operator -> body
```
### Lambda Expression Parameters
There are three Lambda Expression Parameters are mentioned below:
1. Zero Parameter
2. Single Parameter
3. Multiple Parameters
![[Pasted image 20241230003346.png]]
### Java Lambda Expression Example
****Functional Interface Example****:
```
// Java program to demonstrate lambda expressions
// to implement a user defined functional interface.

// A sample functional interface (An interface with
// single abstract method
interface FuncInterface
{
    // An abstract function
    void abstractFun(int x);

    // A non-abstract (or default) function
    default void normalFun()
    {
       System.out.println("Hello");
    }
}

class Test
{
    public static void main(String args[])
    {
        // lambda expression to implement above
        // functional interface. This interface
        // by default implements abstractFun()
        FuncInterface fobj = (int x)->System.out.println(2*x);

        // This calls above lambda expression and prints 10.
        fobj.abstractFun(5);
    }
}
```