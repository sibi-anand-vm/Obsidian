**For loop** is used when the number of iterations is known in advance. It includes initialization, condition check, and increment/decrement.
- **While loop** is used when the number of iterations is not known in advance, but you need to check the condition before executing the loop.
- **Do while loop** is similar to the while loop, but it guarantees at least one execution of the loop, as the condition is checked after executing the loop.

Here’s an example demonstrating all three types of loops:
```
public class Loops {
    public static void main(String[] args) {
        // For loop example
        System.out.println("For loop:");
        for (int i = 1; i <= 5; i++) {
            System.out.println("Iteration: " + i);
        }

        // While loop example
        System.out.println("\nWhile loop:");
        int j = 1;
        while (j <= 5) {
            System.out.println("Iteration: " + j);
            j++;
        }

        // Do while loop example
        System.out.println("\nDo while loop:");
        int k = 1;
        do {
            System.out.println("Iteration: " + k);
            k++;
        } while (k <= 5);
    }
}

```