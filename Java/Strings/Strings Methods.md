1. **String**:
    - A sequence of characters (letters, numbers, symbols) enclosed in double quotes.
    - Indexing starts at 0, and the last index is the length minus 1.
    - **Immutable**: If you try to modify a string, a new object is created, and the old object is discarded. The memory address in the stack will be replaced by the new string.
2. **StringBuffer**:
    - Similar to `String`, but allows modifications without creating new objects.
    - **Has a default capacity of 16 extra characters**: This extra capacity helps avoid memory reallocation when the string grows, improving performance.
    - **Thread-Safe**: Provides synchronization for safe multi-threaded modifications.
    - Key methods: `insert()`, `append()`, `delete()`, `reverse()`.
3. **StringBuilder**:
    - Similar to `StringBuffer` but **not thread-safe**, making it faster when thread safety is not required.
    - Like `StringBuffer`, it also has extra capacity for performance optimization.
    - Key methods: `insert()`, `append()`, `delete()`, `reverse()`.

The key difference between **StringBuffer** and **StringBuilder** is thread safety. `StringBuffer` ensures thread safety by synchronizing operations, while `StringBuilder` does not.

```
public class StringExample {
    public static void main(String[] args) {
        // String Example
        String str = "Hello";
        System.out.println("Original String: " + str);

        // Methods in String
        System.out.println("Length: " + str.length());
        System.out.println("Uppercase: " + str.toUpperCase());
        System.out.println("Lowercase: " + str.toLowerCase());
        System.out.println("Contains 'll': " + str.contains("ll"));
        System.out.println("Substring (1, 4): " + str.substring(1, 4));

        // StringBuilder Example
        StringBuilder sb = new StringBuilder("Hello");
        System.out.println("\nOriginal StringBuilder: " + sb);

        // Methods in StringBuilder
        sb.append(" World"); // Append
        System.out.println("After Append: " + sb);
        sb.insert(6, "Beautiful "); // Insert
        System.out.println("After Insert: " + sb);
        sb.delete(6, 16); // Delete
        System.out.println("After Delete: " + sb);
        sb.reverse(); // Reverse
        System.out.println("After Reverse: " + sb);

        // StringBuffer Example
        StringBuffer sbf = new StringBuffer("Hello");
        System.out.println("\nOriginal StringBuffer: " + sbf);

        // Methods in StringBuffer
        sbf.append(" Java"); // Append
        System.out.println("After Append: " + sbf);
        sbf.insert(6, "Cool "); // Insert
        System.out.println("After Insert: " + sbf);
        sbf.delete(6, 11); // Delete
        System.out.println("After Delete: " + sbf);
        sbf.reverse(); // Reverse
        System.out.println("After Reverse: " + sbf);
    }
}

```

## <font color="#f79646">Essential String Methods</font>

```
public class StringMethodsDemo {
    public static void main(String[] args) {
        String str = "  Hello, Java World!  ";

        // Trim leading and trailing spaces
        String trimmedStr = str.trim();
        System.out.println("Trimmed: " + trimmedStr);

        // Convert to lowercase and uppercase
        System.out.println("Lowercase: " + trimmedStr.toLowerCase());
        System.out.println("Uppercase: " + trimmedStr.toUpperCase());

        // Find the length
        System.out.println("Length: " + trimmedStr.length());

        // Access character at specific index
        System.out.println("Character at index 7: " + trimmedStr.charAt(7));

        // Check if the string contains a substring
        System.out.println("Contains 'Java': " + trimmedStr.contains("Java"));

        // Replace characters
        String replacedStr = trimmedStr.replace('o', '0');
        System.out.println("Replaced 'o' with '0': " + replacedStr);

        // Extract a substring
        System.out.println("Substring (7, 11): " + trimmedStr.substring(7, 11));

        // Split the string
        String[] words = trimmedStr.split(" ");
        System.out.println("Words:");
        for (String word : words) {
            System.out.println(word);
        }

        // Check equality
        String anotherStr = "HELLO, JAVA WORLD!";
        System.out.println("Equals: " + trimmedStr.equals(anotherStr)); // Case-sensitive
        System.out.println("EqualsIgnoreCase: " + trimmedStr.equalsIgnoreCase(anotherStr));

        // Find index of a character
        System.out.println("Index of 'J': " + trimmedStr.indexOf('J'));
        System.out.println("Last index of 'o': " + trimmedStr.lastIndexOf('o'));
    }
}

```