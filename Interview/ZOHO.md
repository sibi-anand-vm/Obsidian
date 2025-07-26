1.Linked List Cycle
https://leetcode.com/problems/linked-list-cycle/submissions/

2.Linked List Cycle
https://leetcode.com/problems/linked-list-cycle-ii/submissions/

3.GCD
```
public class Solution {
	public static int hcf(int a, int b) {
		while(b>0){
		int temp=b;
		b=a%b;
		a=temp;
}
return a;
}
}
```

```
LCM=(a*b)/GCD
```

LCM
```
import java.util.Scanner;
public class LCMByPrimeFactorLogic {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        System.out.print("Enter first number: ");
        int a = sc.nextInt();

        System.out.print("Enter second number: ");
        int b = sc.nextInt();

        int lcm = 1;
        int i = 2;

        while (a > 1 || b > 1) {
            if (a % i == 0 || b % i == 0) {
                lcm *= i;
                if (a % i == 0) a /= i;
                if (b % i == 0) b /= i;
            } else {
                i++;
            }
        }
        System.out.println("LCM is: " + lcm);
    }
}
```

4.Middle-of-the-Linked-List
https://leetcode.com/problems/middle-of-the-linked-list/submissions

5.Find the Index of the First Occurrence in a String
```
public class StrStrManual {
    public static int strStr(String haystack, String needle) {
        int hLen = haystack.length();
        int nLen = needle.length();
        
        if (nLen == 0) return 0;

        for (int i = 0; i <= hLen - nLen; i++) {
            int j = 0;
            // Compare characters manually
            while (j < nLen && haystack.charAt(i + j) == needle.charAt(j)) {
                j++;
            }
            // If full match found
            if (j == nLen) return i;
        }

        return -1;
    }

    public static void main(String[] args) {
        String haystack = "sadbutsad";
        String needle = "but";

        int index = strStr(haystack, needle);
        System.out.println("Index: " + index);  // Output: 3
    }
}

```

6.Counting Sort
```
public class CountingSortString {
    public static String sortString(String str) {
        int[] count = new int[26];  // Only for lowercase a-z

        // Count frequency of each character
        for (char c : str.toCharArray()) {
            count[c - 'a']++;
        }

        // Rebuild sorted string
        StringBuilder sorted = new StringBuilder();
        for (int i = 0; i < 26; i++) {
            while (count[i]-- > 0) {
                sorted.append((char) (i + 'a'));
            }
        }

        return sorted.toString();
    }

    public static void main(String[] args) {
        String input = "desab";
        String sorted = sortString(input);

        System.out.println("Sorted string: " + sorted); // Output: abdes
    }
}
```

7.**Nth node from the end** of a Singly Linked List
```
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

public class LinkedListNthFromEnd {
    // Function to get nth node from the end
    public static int getNthFromEnd(Node head, int n) {
        Node first = head;
        Node second = head;

        // Move first pointer n steps ahead
        for (int i = 0; i < n; i++) {
            if (first == null) return -1; // n is greater than length
            first = first.next;
        }

        // Move both pointers until first reaches the end
        while (first != null) {
            first = first.next;
            second = second.next;
        }

        return second.data;
    }

    public static void main(String[] args) {
        // Example LL: 1 -> 2 -> 3 -> 4 -> 5
        Node head = new Node(1);
        head.next = new Node(2);
        head.next.next = new Node(3);
        head.next.next.next = new Node(4);
        head.next.next.next.next = new Node(5);

        int n = 2; // 2nd node from end is 4
        int result = getNthFromEnd(head, n);
        System.out.println("Nth node from end: " + result);
    }
}

```

8.Print Matrix in Snake pattern 
![[Pasted image 20250715212656.png]]

9.Leaders in a array
![[Pasted image 20250715213341.png]]

10.Second max
```
public class SecondMax {
    public static void main(String[] args) {
        int[] arr = {5, 1, 8, 3, 9, 9, 7};

        int firstMax = Integer.MIN_VALUE;
        int secondMax = Integer.MIN_VALUE;

        for (int num : arr) {
            if (num > firstMax) {
                secondMax = firstMax;
                firstMax = num;
            } else if (num > secondMax && num != firstMax) {
                secondMax = num;
            }
        }

        if (secondMax == Integer.MIN_VALUE) {
            System.out.println("No second maximum (all elements same or only one unique)");
        } else {
            System.out.println("Second maximum: " + secondMax);
        }
    }
}

```

11.Kth Maximum
```
import java.util.*;

public class KthDistinctMax {
    public static void main(String[] args) {
        int[] arr = {10, 8, 20, 4, 15, 8}; // duplicates exist
        int k = 3;

        // Use TreeSet to store unique elements in descending order
        TreeSet<Integer> set = new TreeSet<>(Collections.reverseOrder());
        for (int num : arr) set.add(num);

        if (set.size() < k) {
            System.out.println("Not enough distinct elements");
        } else {
            Iterator<Integer> it = set.iterator();
            int count = 1;
            while (it.hasNext()) {
                int val = it.next();
                if (count == k) {
                    System.out.println("K-th distinct max: " + val);
                    break;
                }
                count++;
            }
        }
    }
}

```

12.Push All Zeros to End (Stable Order)
```
import java.util.Arrays;

public class PushZeroes {
    public static void pushZeroesToEnd(int[] arr) {
        int index = 0; // position to place next non-zero

        // Step 1: Move non-zero elements forward
        for (int num : arr) {
            if (num != 0) {
                arr[index++] = num;
            }
        }

        // Step 2: Fill remaining positions with 0
        while (index < arr.length) {
            arr[index++] = 0;
        }
    }

    public static void main(String[] args) {
        int[] arr = {0, 3, 0, 5, 0, 9, 2};

        pushZeroesToEnd(arr);

        System.out.println("After pushing zeros: " + Arrays.toString(arr));
    }
}

```
![[Pasted image 20250715215537.png]]

13.Remove Duplicates from an Integer Array
```
import java.util.*;

public class RemoveDuplicatesFromArray {
    public static int[] removeDuplicates(int[] arr) {
        LinkedHashSet<Integer> set = new LinkedHashSet<>();
        for (int num : arr) {
            set.add(num); // Keeps only unique elements in insertion order
        }

        // Convert set back to array
        int[] result = new int[set.size()];
        int i = 0;
        for (int num : set) {
            result[i++] = num;
        }
        return result;
    }

    public static void main(String[] args) {
        int[] arr = {1, 3, 2, 3, 1, 5, 2};
        int[] unique = removeDuplicates(arr);
        System.out.println(Arrays.toString(unique)); // Output: [1, 3, 2, 5]
    }
}

```
![[Pasted image 20250716070118.png]]

14.Two Sum
```
public class TwoSumArrayAsMap {
    public static int[] twoSum(int[] nums, int target) {
        int max = 10000; // assume values are in range 0 to 10^4
        int[] indexMap = new int[max + 1]; // stores index + 1

        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];

            if (complement >= 0 && complement <= max && indexMap[complement] > 0) {
                return new int[] { indexMap[complement] - 1, i };
            }

            indexMap[nums[i]] = i + 1; // store index + 1 to avoid default 0
        }

        return new int[] {}; // no solution
    }

    public static void main(String[] args) {
        int[] nums = {2, 7, 11, 15};
        int target = 9;

        int[] result = twoSum(nums, target);
        System.out.println("Indices: [" + result[0] + ", " + result[1] + "]");
    }
}

```

15.Remove chars
```
public class RemoveUsing26Array {
    public static void main(String[] args) {
        String str1 = "banana";
        String str2 = "an";

        // Step 1: Mark presence of characters in str2
        boolean[] hash = new boolean[26]; // Only for lowercase a-z

        for (char c : str2.toCharArray()) {
            hash[c - 'a'] = true;
        }

        // Step 2: Build the result string
        StringBuilder result = new StringBuilder();
        for (char c : str1.toCharArray()) {
            if (!hash[c - 'a']) {
                result.append(c);
            }
        }

        System.out.println("After removal: " + result); // Output: b
    }
}

```

16.Replace 0's with 1's
![[Pasted image 20250716073901.png]]

17.Multiply 2 polynomial

![[Pasted image 20250716074625.png]]

18.Geek-Onanci

![[Pasted image 20250716080138.png]]

19.Square root of a number
![[Pasted image 20250716082026.png]]

20.Anagram

```
import java.util.HashMap;

public class AnagramChecker {
    public static boolean areAnagrams(String a, String b) {
        if(a.length() != b.length()) return false;

        HashMap<Character, Integer> countMap = new HashMap<>();
        for(char c : a.toCharArray()) {
            countMap.put(c, countMap.getOrDefault(c, 0) + 1);
        }
        for(char c : b.toCharArray()) {
            if(!countMap.containsKey(c) || countMap.get(c) == 0) return false;
            countMap.put(c, countMap.get(c) - 1);
        }
        return true;
    }
}
```

21.Gap Sum

![[Pasted image 20250716084838.png]]

22.1A0B1

![[Pasted image 20250716102057.png]]

23.Run Encoding

![[Pasted image 20250716104557.png]]

24.First Non repeating Character

![[Pasted image 20250716105306.png]]

25.Rope cutting

![[Pasted image 20250716115113.png]]

```
double value = 3.14159265358979;

// Using printf
System.out.printf("%.7f\n", value);  // Output: 3.1415927

// Or using format()
String formatted = String.format("%.7f", value);
System.out.println(formatted);
```

26.Geek forgot the code
![[Pasted image 20250716125623.png]]

27.ReciprocalString

![[Pasted image 20250716140413.png]]

28.Bracket number

![[Pasted image 20250716141654.png]]

29.Remove duplicates in LL

![[Pasted image 20250716141959.png]]

30.Maximum sum of a subarray of size `k`

```
public class MaxSubarraySumK {
    public static int maxSubarraySum(int[] arr, int k) {
        int n = arr.length;
        if (n < k) return -1;

        // Compute sum of first window of size k
        int windowSum = 0;
        for (int i = 0; i < k; i++) {
            windowSum += arr[i];
        }

        int maxSum = windowSum;

        // Slide the window
        for (int i = k; i < n; i++) {
            windowSum += arr[i] - arr[i - k]; // Add new, remove old
            maxSum = Math.max(maxSum, windowSum);
        }

        return maxSum;
    }

    public static void main(String[] args) {
        int[] arr = {2, 1, 5, 1, 3, 2};
        int k = 3;
        System.out.println("Max sum of subarray of size " + k + ": " + maxSubarraySum(arr, k));
    }
}
```

31.Evaluate String
```
import java.util.*;

public class EvaluateExpressionWithStack {

    // Step 1: Convert infix to postfix
    public static List<String> infixToPostfix(String expr) {
        List<String> output = new ArrayList<>();
        Stack<Character> operators = new Stack<>();

        int n = expr.length();
        for (int i = 0; i < n; i++) {
            char ch = expr.charAt(i);

            if (Character.isDigit(ch)) {
                // Handle multi-digit numbers
                StringBuilder num = new StringBuilder();
                while (i < n && Character.isDigit(expr.charAt(i))) {
                    num.append(expr.charAt(i++));
                }
                i--; // step back
                output.add(num.toString());

            } else if (ch == '(') {
                operators.push(ch);

            } else if (ch == ')') {
                while (!operators.isEmpty() && operators.peek() != '(') {
                    output.add(operators.pop().toString());
                }
                operators.pop(); // pop '('

            } else if (isOperator(ch)) {
                while (!operators.isEmpty() && precedence(operators.peek()) >= precedence(ch)) {
                    output.add(operators.pop().toString());
                }
                operators.push(ch);
            }
        }

        while (!operators.isEmpty()) {
            output.add(operators.pop().toString());
        }

        return output;
    }

    // Step 2: Evaluate postfix expression
    public static int evaluatePostfix(List<String> postfix) {
        Stack<Integer> stack = new Stack<>();

        for (String token : postfix) {
            if (isNumeric(token)) {
                stack.push(Integer.parseInt(token));
            } else {
                int b = stack.pop();
                int a = stack.pop();
                int res = applyOp(a, b, token.charAt(0));
                stack.push(res);
            }
        }

        return stack.pop();
    }

    // Helpers
    public static boolean isOperator(char ch) {
        return ch == '+' || ch == '-' || ch == '*' || ch == '/';
    }

    public static int precedence(char op) {
        if (op == '+' || op == '-') return 1;
        if (op == '*' || op == '/') return 2;
        return 0;
    }

    public static int applyOp(int a, int b, char op) {
        switch (op) {
            case '+': return a + b;
            case '-': return a - b;
            case '*': return a * b;
            case '/': return a / b; // assume b != 0
            default: return 0;
        }
    }

    public static boolean isNumeric(String str) {
        return str.matches("\\d+");
    }

    public static void main(String[] args) {
        String expr = "8*(4+2)/2";

        List<String> postfix = infixToPostfix(expr);
        System.out.println("Postfix: " + postfix); // Debug

        int result = evaluatePostfix(postfix);
        System.out.println("Evaluated Result: " + result); // Output: 24
    }
}

```