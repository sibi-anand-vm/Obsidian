### <mark style="background: #FF5582A6;">Variables and Data Types in Java</mark>

1. **Variables**: Containers for storing temporary values during program execution.
2. **Data Types**: Define the type of data a variable can store.
![[Pasted image 20241225184301.png]]

<mark style="background: #FFB86CA6;">Types of Data Types</mark>

1. **Primitive Data Types**:
    
    - **Integer Types**:
        - `byte` (1 byte): Stores values from -128 to 127.
        - `short` (2 bytes): Stores values from -32,768 to 32,767.
        - `int` (4 bytes): Default integer type, stores values from -2³¹ to 2³¹-1.
        - `long` (8 bytes): For large integers. Must end with `L`.
    - **Floating-Point Types**:
        - `float` (4 bytes): Stores decimal values, ends with `f`.
        - `double` (8 bytes): Default for decimal values, higher precision.
    - **Character Type**:
        - `char` (2 bytes): Stores a single character within single quotes (`'a'`).
    - **Boolean Type**:
        - `boolean` (1 bit): Stores `true` or `false`.
![[Pasted image 20241225184344.png]]
See the example code:
```
class DataTypesExample {
    public static void main(String[] args) {
        // Integer types
        byte b = 100;
        short s = 30000;
        int i = 123456;
        long l = 123456789L;

        // Floating-point types
        float f = 12.34f;
        double d = 123.456789;

        // Character type
        char c = 'A';

        // Boolean type
        boolean isJavaFun = true;

        // Print values
        System.out.println("Byte: " + b);
        System.out.println("Short: " + s);
        System.out.println("Int: " + i);
        System.out.println("Long: " + l);
        System.out.println("Float: " + f);
        System.out.println("Double: " + d
    
```
![[Pasted image 20241225184423.png]]

## <mark style="background: #FFB86CA6;">Binary and Hexadecimal values</mark>
Here’s a sample code showcasing how to store and use binary and hexadecimal values in Java:
```
class BinaryHexExample {
    public static void main(String[] args) {
        // Storing a binary value (prefix 0b)
        int binaryValue = 0b1010; // Binary for decimal 10
        System.out.println("Binary Value (0b1010): " + binaryValue);

        // Storing a hexadecimal value (prefix 0x)
        int hexValue = 0x1F; // Hexadecimal for decimal 31
        System.out.println("Hexadecimal Value (0x1F): " + hexValue);

        // Using binary and hexadecimal in calculations
        int sum = binaryValue + hexValue;
        System.out.println("Sum of Binary and Hexadecimal: " + sum);
    }
}

```
### Explanation:

1. **Binary Values**: Use the prefix `0b` followed by the binary digits (0 or 1).
2. **Hexadecimal Values**: Use the prefix `0x` followed by hexadecimal digits (0-9, A-F).

## <mark style="background: #FFB86CA6;">Incrementing Char</mark>

In Java, you can increment a `char` value because `char` is internally represented as a numeric value (its Unicode value). When you increment a `char`, its Unicode value increases, resulting in the next character in the Unicode sequence.

```
class CharIncrementExample {
    public static void main(String[] args) {
        char letter = 'A'; // Initial character
        System.out.println("Initial char: " + letter);

        // Increment the char
        letter++;
        System.out.println("After increment: " + letter);

        // Increment multiple times
        letter += 3;
        System.out.println("After incrementing by 3: " + letter);
    }
}

```
**OUTPUT:**
```
Initial char: A  
After increment: B  
After incrementing by 3: E
```
