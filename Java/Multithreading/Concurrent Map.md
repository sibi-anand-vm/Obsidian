# 🧵 Concurrent Map in Java

## 🔹 Overview

`ConcurrentMap` is a **thread-safe map** that allows concurrent access and modification without requiring external synchronization.

- Synchronization is handled automatically by Java.
    
- Useful in multithreaded environments where multiple threads read/write data.
    

### Implementations

- `ConcurrentHashMap`
    
- `ConcurrentSkipListMap`
    
- `ConcurrentListHashMap`
    
- `ConcurrentNavigableHashMap`
    

---

## 🔹 Internal Working

### 1. Adding an element

1. **Hashing & segment determination**: The key is hashed to find the target segment.
    
2. **Lock acquisition**: Only one thread can access the segment at a time.
    
3. **Insertion**: The element is inserted into the determined segment.
    
4. **Lock release**: Segment is unlocked for other threads.
    

### 2. Fetching an element

1. **Hashing & segment determination**: Key is hashed to locate the segment.
    
2. **Lock acquisition**: Segment is locked to ensure thread-safe read.
    
3. **Read operation**: Element is retrieved from the segment.
    
4. **Lock release**: Segment is unlocked, allowing other threads to access it.
    

---

## 💻 Example Code

```java
import java.util.concurrent.ConcurrentHashMap;
import java.util.concurrent.ConcurrentMap;

public class ConcurrentMapExample {
    public static void main(String[] args) throws InterruptedException {
        ConcurrentMap<Integer, String> map = new ConcurrentHashMap<>();

        // Thread 1: Adding elements
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                map.put(i, "Value-" + i);
                System.out.println("Thread 1 added: " + i);
            }
        });

        // Thread 2: Reading elements
        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                String value = map.get(i);
                System.out.println("Thread 2 read: " + i + " -> " + value);
            }
        });

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println("Final map: " + map);
    }
}
```

---

## ✅ Key Points

- Concurrency is achieved at **segment level**, not the whole map.
    
- Multiple threads can read/write **different segments simultaneously**.
    
- Only threads accessing the same segment are synchronized.
    
- Provides **high-performance thread-safe operations** without locking the entire map.
    

---

## 🧩 Takeaways

- Prefer `ConcurrentHashMap` for high-concurrency scenarios.
    
- Segment-level locking improves throughput compared to full-map synchronization.
    
- Always use concurrent collections in multithreaded environments instead of synchronized wrappers.