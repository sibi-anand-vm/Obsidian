```java
class VarargsExample {
    // ✅ Varargs Rules:
    // 1. Varargs (int... scores) must be the LAST parameter.
    // 2. Only one varargs parameter allowed per method.
    // 3. Internally, varargs are treated as arrays.

    // Example 1: Extra int before varargs
    static void printDetails(String name, int n, int... scores) {
        System.out.println("Name: " + name);
        System.out.println("Number: " + n);

        for (int s : scores) {
            System.out.print(s + " ");
        }
        System.out.println();
    }

    // Example 2: Only varargs, use scores.length to count
    static void printScores(String name, int... scores) {
        System.out.println("Name: " + name);
        System.out.println("Count of scores: " + scores.length);
    }

    // ❌ Invalid Example (will cause compilation error):
    // static void wrongExample(String name, int... scores, int n) {}
    // Reason: varargs must be the last parameter.

    public static void main(String[] args) {
        // Call with extra int before varargs
        printDetails("Captain", 5, 90, 85, 80);

        // Call with only varargs
        printScores("Captain", 90, 85, 80);
    }
} ```