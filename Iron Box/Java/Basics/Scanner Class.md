1. The `Scanner` class does indeed belong to the `java.util` package, and it is used for reading inputs like integers, floats, strings, etc., from various input sources such as `System.in` (keyboard), files, or streams.
    
2. `nextLine` reads the entire line of input as a string, while methods like `nextInt`, `nextFloat`, etc., only read the next token (separated by whitespace).
    
3. For reading a matrix as input, you can loop through rows (outer loop) and use an inner loop to parse values for each column.

```
package Basics;  
import java.util.*;  
import static java.lang.Integer.parseInt;  
class Scannerclass{  
    public static void  main(String[] args){  
        int a,b;  
        Scanner sc=new Scanner(System.in);  
        a=sc.nextInt();  
        b=sc.nextByte();  
        System.out.println("First val:"+a);  
        System.out.println("Sec val:"+b);  
        sc.nextLine();  
        String line[]=sc.nextLine().split(" ");  
        for(String s:line){  
            System.out.print(parseInt(s)+" ");  
        }  
        int[][] mat = new int[a][b];  
  
        System.out.println("Enter the matrix elements row by row (space-separated): ");  
        for (int i = 0; i < a; i++) {  
            String[] l = sc.nextLine().split(" ");  
            for (int j = 0; j < b; j++) {  
                mat[i][j] = parseInt(l[j]);  
            }  
        }  
  
        // Print the matrix  
        System.out.println("The matrix is:");  
        for (int i = 0; i < a; i++) {  
            for (int j = 0; j < b; j++) {  
                System.out.print(mat[i][j] + " ");  
            }  
            System.out.println();  
        }  
    }  
}
```
