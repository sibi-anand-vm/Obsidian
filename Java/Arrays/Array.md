## ==One dim,2-dim,N-Dimensional array==
- Arrays are continuous memory blocks used to store elements of the same data type.
- They allow element access using index numbers, which always start from zero.
- The size of an array must be specified during declaration and cannot be changed later.
- Arrays are objects in Java and can be declared using curly braces or the `new` keyword.
- You can traverse arrays using loops like `for`, `while`, `do-while`, and the enhanced `for-each` loop.
- Arrays can only store elements of a single data type, which is a key limitation.
- For storing elements of different data types, other Java collections like `ArrayList` or `HashMap` are recommended.
- Arrays are fundamental but lack the flexibility of dynamic
```
package Arrays;  
import java.util.Scanner;  
  
import static java.lang.Integer.parseInt;  
  
class OneandTwoDimArray{  
    public static void  main(String[] args){  
        Scanner sc=new Scanner(System.in);  
        int[] a=new int[5];  
        int m,n;  
        for(int i=0;i<a.length;i++){  
            a[i]=(int)(Math.random()*10);  
            System.out.print(a[i]+" ");  
        }  
  
        m=sc.nextInt();  
        n=sc.nextInt();  
        sc.nextLine();  
int mat[][]=new int[m][n];  
        for(int i=0;i<mat.length;i++){  
            String[] line=sc.nextLine().split(" ");  
            for (int j=0;j<mat[i].length;j++){  
                mat[i][j]=parseInt(line[j]);  
            }  
        }  
        for(int i[]:mat){  
            for(int j:i){  
                System.out.print(j+" ");  
            }  
            System.out.println();  
        }  
    }  
}
```
## ==Jagged array==
- Jagged arrays allow rows to have different lengths, unlike regular multidimensional arrays.
- In a jagged array, one row can have a different number of elements than another.
- This flexibility makes them ideal for scenarios where data varies in size across rows.
- They are often implemented as an array of arrays, enabling dynamic row sizes.
- Jagged arrays break the uniform size rule of normal multidimensional arrays.
```
package Arrays;  
import static java.lang.Integer.parseInt;  
import java.util.*;  
class JaggedArray {  
    public static void main(String[] args) {  
        Scanner sc = new Scanner(System.in);  
        int m = sc.nextInt();  
        sc.nextLine();  
        int mat[][] = new int[m][];  
for(int i=0;i< mat.length;i++){  
    String[] l=sc.nextLine().split(" ");  
    mat[i]=new int[l.length];  
    for (int j=0;j<mat[i].length;j++){  
        mat[i][j]=(parseInt(l[j]));  
    }  
}  
        for(int i[]:mat){  
            for(int j:i){  
                System.out.print(j+" ");  
            }  
            System.out.println();  
        }  
    }  
}
```