# 🧩 CountDownLatch in Java

## 🔹 Concept Overview

**CountDownLatch** is a synchronization aid in Java that allows one or more threads to wait until a set of operations being performed by other threads completes.

Think of it like a **checkpoint system**:

- You (the main thread or tech lead) assign several subtasks to your team (worker threads).
    
- The main task (you) can proceed **only after** all subtasks are finished.
    
- The **checkpoint** that tracks whether all subtasks are done is the **latch**.
    

---

## 🔹 How It Works

- `CountDownLatch` is initialized with a **count** — the number of threads (or subtasks) to wait for.
    
- Each time a thread finishes its task, it calls `latch.countDown()`, which decreases the count by 1.
    
- The main thread calls `latch.await()`, which **blocks** until the count reaches zero.
    
- Once the count becomes 0, all waiting threads are released and execution proceeds.
    

---

## 🔹 Example Analogy

> 👨‍💻 You’re a tech lead with 3 assistants.  
> Each assistant has a subtask to complete.  
> The project (main thread) can only proceed once all 3 assistants have reported completion.

---

## 🔹 Code Example

```java
import java.util.concurrent.CountDownLatch;

public class CountDownLatchDemo {

    public static void main(String[] args) throws InterruptedException {
        CountDownLatch latch = new CountDownLatch(3);

        // Three worker threads
        for (int i = 1; i <= 3; i++) {
            new Thread(new Worker(latch, "Worker-" + i)).start();
        }

        // Main thread waits for workers to finish
        latch.await();
        System.out.println("✅ All workers completed. Main thread proceeds.");
    }

    static class Worker implements Runnable {
        private final CountDownLatch latch;
        private final String name;

        Worker(CountDownLatch latch, String name) {
            this.latch = latch;
            this.name = name;
        }

        @Override
        public void run() {
            System.out.println(name + " started task...");
            try {
                Thread.sleep(1000); // Simulate work
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println(name + " finished task.");
            latch.countDown(); // Decrement latch count
        }
    }
}
```

---

## 🔹 Difference from `Thread.join()`

|Feature|`Thread.join()`|`CountDownLatch`|
|---|---|---|
|Waiting mechanism|Waits for **one specific thread** to finish|Waits for **multiple threads or tasks**|
|Flexibility|Must call `join()` for each thread individually|One latch can handle multiple threads together|
|Reusability|Can be reused by restarting threads|**Cannot be reused** once count reaches 0|

---

## 🔹 Summary

✅ **Use CountDownLatch** when:

- You have multiple parallel tasks and need to wait for all to finish before proceeding.
    
- You want a clean, centralized waiting mechanism instead of multiple `.join()` calls.
    

🧠 Think of it as:

> “Wait until everyone’s done, then move to the next phase.”