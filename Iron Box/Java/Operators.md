### <mark style="background: #FFB86CA6;">Types of Operators:</mark>

1. **Arithmetic Operators**: Used for basic mathematical operations.
    
    - `+` (Addition)
    - `-` (Subtraction)
    - `*` (Multiplication)
    - `/` (Division)
    - `%` (Modulus)
2. **Assignment Operators**: Used to assign values to variables with operations.
    
    - `=` (Assignment)
    - `+=` (Add and assign)
    - `-=` (Subtract and assign)
    - `*=` (Multiply and assign)
    - `/=` (Divide and assign)
3. **Relational Operators**: Used to compare two values.
    
    - `==` (Equal to)
    - `!=` (Not equal to)
    - `>` (Greater than)
    - `<` (Less than)
    - `>=` (Greater than or equal to)
    - `<=` (Less than or equal to)
4. **Logical Operators**: Used to perform logical operations.
    
    - `&&` (Logical AND)
    - `||` (Logical OR)
    - `!` (Logical NOT)
```
public class OperatorExample {
    public static void main(String[] args) {
        int a = 10, b = 20, c = 30;

        // Arithmetic Operators
        int sum = a + b; // Addition
        int diff = b - a; // Subtraction
        int prod = a * b; // Multiplication
        int div = c / a; // Division
        int mod = b % a; // Modulus

        // Assignment Operators
        a += 5; // a = a + 5
        b -= 2; // b = b - 2
        c *= 2; // c = c * 2
        a /= 3; // a = a / 3

        // Relational Operators
        boolean isEqual = (a == b); // Equal to
        boolean isNotEqual = (b != c); // Not equal to
        boolean isGreaterThan = (c > a); // Greater than
        boolean isLessThan = (a < b); // Less than
        boolean isGreaterEqual = (b >= a); // Greater than or equal to
        boolean isLessEqual = (a <= c); // Less than or equal to

        // Logical Operators
        boolean logicalAnd = (a > 5 && b > 10); // AND
        boolean logicalOr = (a > 5 || b < 10); // OR
        boolean logicalNot = !(a == b); // NOT

        // Display results
        System.out.println("Arithmetic Operations:");
        System.out.println("a + b = " + sum);
        System.out.println("b - a = " + diff);
        System.out.println("a * b = " + prod);
        System.out.println("c / a = " + div);
        System.out.println("b % a = " + mod);

        System.out.println("\nAssignment Operations:");
        System.out.println("a += 5, a = " + a);
        System.out.println("b -= 2, b = " + b);
        System.out.println("c *= 2, c = " + c);
        System.out.println("a /= 3, a = " + a);

        System.out.println("\nRelational Operations:");
        System.out.println("a == b: " + isEqual);
        System.out.println("b != c: " + isNotEqual);
        System.out.println("c > a: " + isGreaterThan);
        System.out.println("a < b: " + isLessThan);
        System.out.println("b >= a: " + isGreaterEqual);
        System.out.println("a <= c: " + isLessEqual);

        System.out.println("\nLogical Operations:");
        System.out.println("a > 5 && b > 10: " + logicalAnd);
        System.out.println("a > 5 || b < 10: " + logicalOr);
        System.out.println("!(a == b): " + logicalNot);
    }
}

```
## <mark style="background: #FFB86CA6;">Ternary Operator</mark>

It comes in form of ?:
Example:
```
n=20
boolean result= n%2==0? true :false;
System.out.println("!(a == b): " + logicalNot);
```
**OUTPUT:**
```
true
```

