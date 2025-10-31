==Here Arrays class provides several static methods that can be used to perform these tasks directly without the use of loops, hence forth making our code super short and optimized.==
- **asList()**: Converts an array into a list.
- **binarySearch()**: Searches for a key in the array using binary search.
- **compare()**: Compares two arrays and returns the index of the first mismatch.
- **copyOf()**: Copies an array into a new array with a specified length.
- **copyOfRange()**: Copies a range of elements from an array.
- **equals()**: Compares two arrays for equality.
- **fill()**: Fills an array with a specified value.
- **sort()**: Sorts an array in ascending order.
- **sort(fromIndex, toIndex)**: Sorts a specified portion of an array.
- **toString()**: Converts an array to a string representation.
- 
```java
import java.util.*;

public class ArrayMethodsExample {
    public static void main(String[] args) {
        
        // 1. asList() - Convert an array to a list
        Integer[] arr1 = {5, 3, 8, 1};
        List<Integer> list = Arrays.asList(arr1);
        System.out.println("asList(): " + list);
        
        // 2. binarySearch() - Perform binary search in a sorted array
        int[] arr2 = {1, 3, 5, 8};
        int index = Arrays.binarySearch(arr2, 3);
        System.out.println("binarySearch() - Index of 3: " + index);
        
        // 3. compare() - Compare two arrays
        int[] arr3 = {1, 2, 3};
        int[] arr4 = {1, 2, 3};
        int compareResult = Arrays.compare(arr3, arr4);
        System.out.println("compare() - Comparison result: " + compareResult);
        
        // 4. copyOf() - Copy an array with a new length
        int[] arr5 = {1, 2, 3};
        int[] newArr = Arrays.copyOf(arr5, 5);
        System.out.println("copyOf() - New array: " + Arrays.toString(newArr));
        
        // 5. copyOfRange() - Copy a specific range of an array
        int[] arr6 = {1, 2, 3, 4, 5};
        int[] copiedRange = Arrays.copyOfRange(arr6, 1, 4);  // Copies elements from index 1 to 3
        System.out.println("copyOfRange() - Copied range: " + Arrays.toString(copiedRange));
        
        // 6. equals() - Compare two arrays for equality
        boolean areEqual = Arrays.equals(arr3, arr4);
        System.out.println("equals() - Arrays are equal: " + areEqual);
        
        // 7. fill() - Fill an array with a specific value
        int[] arr7 = new int[5];
        Arrays.fill(arr7, 7);
        System.out.println("fill() - Filled array: " + Arrays.toString(arr7));
        
        // 8. sort() - Sort the array
        int[] arr8 = {5, 2, 9, 1, 3};
        Arrays.sort(arr8);
        System.out.println("sort() - Sorted array: " + Arrays.toString(arr8));
        
        // 9. sort() with range - Sort a specific range of the array
        int[] arr9 = {5, 3, 8, 6, 1, 2};
        Arrays.sort(arr9, 2, 5); // Sort elements from index 2 to 4
        System.out.println("sort() with range - Sorted range: " + Arrays.toString(arr9));
        
    }
}

```