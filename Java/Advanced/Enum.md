A Java enumeration is a [class](https://www.geeksforgeeks.org/object-oriented-programming-in-python-set-1-class-and-its-members/) type. Although we don’t need to instantiate an enum using ****new,**** it has the same capabilities as other classes. This fact makes Java enumeration a very powerful tool. Just like classes, you can give them [constructors,](https://www.geeksforgeeks.org/constructors-c/) add instance variables and methods, and even implement interfaces.
## <mark style="background: #FFB86CA6;"> Declaration of enum in Java</mark>
Enum declaration can be done outside a class or inside a class but not inside a method.
### 1. Declaration outside the class
```
// A simple enum example where enum is declared
// outside any class (Note enum keyword instead of
// class keyword)
enum Color {
    RED,
    GREEN,
    BLUE;
}

public class Test {
    // Driver method
    public static void main(String[] args) {
        Color c1 = Color.RED;
        System.out.println(c1);
    }
}
```
**OUTPUT**
```
RED
```
## Properties of Enum in Java

There are certain properties followed by Enum as mentioned below:

- ****Class Type:**** Every enum is internally implemented using the `Class` type.
- ****Enum Constants:**** Each enum constant represents an object of type enum.
- ****Switch Statements:**** Enum types can be used in switch statements.
- ****Implicit Modifiers:**** Every enum constant is implicitly `public static final`. Since it is static, it can be accessed using the enum name. Since it is final, enums cannot be extended.
- ****Main Method:**** Enums can declare a `main()` method, allowing direct invocation from the command line.
****Below is the implementation of the above properties:****
```
// A Java program to demonstrate working on enum
// in a switch case (Filename Test.java)

import java.util.Scanner;

// An Enum class
enum Day {
    SUNDAY,
    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY;
}

// Driver class that contains an object of "day" and
// main().
public class Test {
    Day day;

    // Constructor
    public Test(Day day) {
        this.day = day;
    }

    // Prints a line about Day using switch
    public void dayIsLike() {
        switch (day) {
        case MONDAY:
            System.out.println("Mondays are bad.");
            break;
        case FRIDAY:
            System.out.println("Fridays are better.");
            break;
        case SATURDAY:
        case SUNDAY:
            System.out.println("Weekends are best.");
            break;
        default:
            System.out.println("Midweek days are so-so.");
            break;
        }
    }

    // Driver method
    public static void main(String[] args) {
        String str = "MONDAY";
        Test t1 = new Test(Day.valueOf(str));
        t1.dayIsLike();
    }
}
```
**OUTPUT**
```
Mondays are bad.
```
