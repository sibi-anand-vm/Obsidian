# 🧥 Thread Synchronization in Java

### ⚠️ Problem

When multiple threads access the same resource at the same time, it can lead to **data inconsistency** or **race conditions**.

---

### 🛠 Solution: Synchronization

Java provides the `synchronized` keyword to **control access to shared resources**.

---

### 🔹 1. Method-Level Synchronization

- Locks the **entire method** (monitor lock on `this` object).
    
- Other threads cannot access any synchronized method of the same object until the lock is released.
    
- Can reduce concurrency if multiple threads need access.
    

```java
public synchronized void increment() {
    count++;
}
```

---

### 🔹 2. Block-Level Synchronization (Recommended)

- Locks **only the critical section** of code.
    
- Other threads can still execute non-synchronized parts of the method.
    
- Improves concurrency and efficiency.
    

```java
public void increment() {
    synchronized(this) {
        count++;
    }
}
```

---

### 🔹 3. `this` vs Separate Lock Object

#### Using `this`

- Locks the **current instance**.
    
- Only one thread can enter any synchronized block or method of this object at a time.
    
- Threads on other instances are not blocked.
    

```java
synchronized(this) {
    // critical section
}
```

#### Using a Separate Lock Object

- Locks only this specific lock object.
    
- Safer and more flexible; allows multiple locks in one object.
    
- External code cannot accidentally acquire the lock.
    

```java
private final Object lock = new Object();

synchronized(lock) {
    // critical section
}
```

---

### ✅ Rule of Thumb

- Use `this` when locking the **entire instance** is sufficient.
    
- Use a **private lock object** when you want **more control** and **better concurrency**.

## Example
### 🛠 Solution: Synchronization with a Lock Object

Use a shared lock object with `synchronized` to ensure **only one thread at a time** can access the critical section.

---

### 🔹 Example Code

```java
package com.jocata.Synchronization;

public class SynchronizationKeyword {

    static int counter = 0;
    static final Object lock = new Object(); 

    public static void increment() {
        synchronized (lock) {
            counter++;
        }
    }

    public static void main(String[] args) throws InterruptedException {

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) increment();
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) increment();
        });

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println("Counter: " + counter); // Always 2000
    }
}
```

---

### 🔹 Explanation

1. **Shared Counter:** `counter` is shared by both threads.
    
2. **Lock Object:** `lock` is a static final object used for synchronization.
    
3. **Synchronized Increment:** The `increment()` method uses `synchronized(lock)` to prevent race conditions.
    
4. **Threads:** Two threads increment the counter 1000 times each.
    
5. **Joining Threads:** `t1.join()` and `t2.join()` ensure the main thread waits for both threads to finish.
    
6. **Output:** Always prints `2000` due to proper synchronization.
    

---

### 🔹 Key Points

- Block-level synchronization with a **shared lock object** is safer and more efficient than synchronizing the whole method.
    
- Always use the **same lock object** for threads that access shared resources.
    
- Prevents lost updates and ensures thread-safe operations.