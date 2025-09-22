# Collections in Java

The **Collection in Java** is a framework that provides an architecture to store and manipulate the group of objects.

Java Collections can achieve all the operations that you perform on a data such as searching, sorting, insertion, manipulation, and deletion.

Java Collection means a single unit of objects. Java Collection framework provides many interfaces (Set, List, Queue, Deque) and classes ([ArrayList](https://www.javatpoint.com/java-arraylist), Vector, [LinkedList](https://www.javatpoint.com/java-linkedlist), [PriorityQueue](https://www.javatpoint.com/java-priorityqueue), HashSet, LinkedHashSet, TreeSet).
![[Pasted image 20250821164140.png]]
![[Pasted image 20241230224027.png]]
**ArrayList Example**
```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<String> names = new ArrayList<>();
        names.add("Alice");
        names.add("Bob");
        names.add("Charlie");

        System.out.println("ArrayList contents: " + names);
    }
}

```
**HashSet Example**
```java
import java.util.HashSet;

public class HashSetExample {
    public static void main(String[] args) {
        HashSet<Integer> numbers = new HashSet<>();
        numbers.add(10);
        numbers.add(20);
        numbers.add(20); // Duplicate value, won't be added

        System.out.println("HashSet contents: " + numbers);
    }
}

```
**LinkedList Example**
```java
import java.util.LinkedList;

public class LinkedListExample {
    public static void main(String[] args) {
        LinkedList<String> tasks = new LinkedList<>();
        tasks.add("Task 1");
        tasks.add("Task 2");
        tasks.addFirst("Urgent Task");

        System.out.println("LinkedList contents: " + tasks);
    }
}

```
**HashMap Example**
```java
import java.util.HashMap;

public class HashMapExample {
    public static void main(String[] args) {
        HashMap<Integer, String> map = new HashMap<>();
        map.put(1, "Apple");
        map.put(2, "Banana");
        map.put(3, "Cherry");

        System.out.println("HashMap contents: " + map);
    }
}

```
## Comparison of Map Implementations

|Map Class|Null Key Support|Null Value Support|Notes|
|---|---|---|---|
|**HashMap**|✅ 1 null key allowed|✅ Multiple null values allowed|Most commonly used general-purpose map|
|**LinkedHashMap**|✅ 1 null key allowed|✅ Multiple null values allowed|Preserves insertion order|
|**TreeMap**|❌ Not allowed|✅ Multiple null values allowed|Sorted by keys, comparator required for custom ordering|
|**Hashtable**|❌ Not allowed|❌ Not allowed|Legacy class, synchronized (slower than ConcurrentHashMap)|
|**ConcurrentHashMap**|❌ Not allowed|❌ Not allowed|Thread-safe, high-performance concurrency|
|**ConcurrentSkipListMap**|❌ Not allowed|❌ Not allowed|Concurrent + sorted map, based on skip list|

---

### 🔑 Quick Interview Takeaways

- **HashMap & LinkedHashMap** → **one null key**, **multiple null values**.
    
- **TreeMap** → **no null key**, but **multiple null values**.
    
- **Hashtable & Concurrent Maps** → **no null keys, no null values**.
## <font color="#f79646">Essential methods</font>
```java
import java.util.*;

public class CollectionsExample {
    public static void main(String[] args) {
        // 1. List Example
        List<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Banana");
        list.add("Cherry");
        list.add(1, "Blueberry");
        System.out.println("List: " + list);

        list.remove("Banana");
        System.out.println("After removal: " + list);

        System.out.println("Element at index 1: " + list.get(1));
        System.out.println("List contains 'Apple': " + list.contains("Apple"));

        // 2. Set Example
        Set<Integer> set = new HashSet<>();
        set.add(10);
        set.add(20);
        set.add(30);
        set.add(20); // Duplicate, won't be added
        System.out.println("\nSet: " + set);

        set.remove(10);
        System.out.println("After removal: " + set);
        System.out.println("Set contains 30: " + set.contains(30));

        // 3. Map Example
        Map<Integer, String> map = new HashMap<>();
        map.put(1, "John");
        map.put(2, "Jane");
        map.put(3, "Jack");
        System.out.println("\nMap: " + map);

        map.remove(2);
        System.out.println("After removal: " + map);

        System.out.println("Value for key 1: " + map.get(1));
        System.out.println("Map contains key 3: " + map.containsKey(3));
        System.out.println("Map contains value 'Jack': " + map.containsValue("Jack"));

        // 4. Queue Example
        Queue<String> queue = new LinkedList<>();
        queue.offer("Task1");
        queue.offer("Task2");
        queue.offer("Task3");
        System.out.println("\nQueue: " + queue);

        System.out.println("Polled element: " + queue.poll());
        System.out.println("Queue after poll: " + queue);

        System.out.println("Peek element: " + queue.peek());

        // 5. Collections Utility Methods
        Collections.sort(list);
        System.out.println("\nSorted List: " + list);

        Collections.reverse(list);
        System.out.println("Reversed List: " + list);

        System.out.println("Frequency of 'Apple': " + Collections.frequency(list, "Apple"));
        System.out.println("Max element in Set: " + Collections.max(set));
    }
}
```