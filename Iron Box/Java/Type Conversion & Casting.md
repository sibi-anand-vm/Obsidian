### <mark style="background: #FFB86CA6;">Type Conversion, Casting, and Type Promotion</mark>

1. **Type Conversion**: Automatically converting a smaller data type to a larger data type (widening conversion).
    - Example: A `byte` value can be automatically converted to `int`.
```
byte smallValue = 12;
int largerValue = smallValue; // Widening (automatic conversion)
System.out.println("Converted byte to int: " + largerValue);   
```

2. **Casting**: Forcefully converting a larger data type to a smaller data type (narrowing conversion). It requires explicit casting and can result in data loss.
    - Example: Converting an `int` to a `byte`.
```
int largeValue = 257;
byte smallValue = (byte) largeValue; // Narrowing (explicit casting)
System.out.println("Converted int to byte: " + smallValue); // Output: 1
```
3. **Type Promotion**: When performing operations between smaller data types, Java automatically promotes the result to a larger data type (usually `int`) to avoid overflow.
     Example: Multiplying two `byte` values results in an `int`, and the result is then cast back to `byte`.
```
byte a = 10, b = 30;
byte result = (byte) (a * b); // Promotion to int and then casting back to byte
System.out.println("Result of multiplication: " + result); // Output: 44     
```
### <mark style="background: #FFB86CA6;">Complete Code Example:</mark>

```
public class TypeConversionExample {
    public static void main(String[] args) {
        // Type Conversion (widening)
        byte smallValue = 12;
        int largerValue = smallValue; // Automatic conversion
        System.out.println("Converted byte to int: " + largerValue);

        // Casting (narrowing)
        int largeValue = 257;
        byte smallValueFromInt = (byte) largeValue; // Explicit cast
        System.out.println("Converted int to byte: " + smallValueFromInt); // Output: 1

        // Type Promotion
        byte a = 10, b = 30;
        byte result = (byte) (a * b); // Promotion to int and then back to byte
        System.out.println("Result of multiplication: " + result); // Output: 44
    }
}
```