# 🧵 Multithreading in Java

## 🔹 1. Introduction

**Multithreading** = executing multiple threads _concurrently_ to improve performance and responsiveness.

A **thread** is the smallest unit of execution within a process. It represents a single sequence of programmed instructions that can run independently and, often, simultaneously with other threads in the same program.

## What a Thread Does

A thread performs a specific part of a program’s work. Each thread runs its own sequence of instructions, maintains its **program counter** (current instruction), **stack** (local variables), and **registers** (temporary data), but shares memory and resources with other threads in the same process.
    
- **Process** → program in execution (can have multiple threads)
    

✅ Java supports multithreading via `java.lang.Thread` and the `java.util.concurrent` package.

---

## 🔹 2. Creating Threads

### ✅ Way 1: Extend `Thread` class

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running: " + Thread.currentThread().getName());
    }
}

public class Demo {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        t1.start(); // starts new thread
    }
}
```

---

### ✅ Way 2: Implement `Runnable`

```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Runnable thread: " + Thread.currentThread().getName());
    }
}

public class Demo {
    public static void main(String[] args) {
        Thread t = new Thread(new MyRunnable());
        t.start();
    }
}
```

> 🧠 Prefer `Runnable` — allows extending another class.

---

### ✅ Way 3: Lambda Expression

```java
public class LambdaThread {
    public static void main(String[] args) {
        Thread t = new Thread(() -> System.out.println("Lambda thread running"));
        t.start();
    }
}
```

---

## 🔹 3. Thread Lifecycle

|State|Description|
|---|---|
|**New**|Thread created but not started|
|**Runnable**|Ready to run or running|
|**Blocked/Waiting**|Waiting for monitor lock or signal|
|**Timed Waiting**|Waiting for a specific time|
|**Terminated**|Finished execution|

---

## 🔹 4. Thread Methods

| Method          | Description                        |
| --------------- | ---------------------------------- |
| `start()`       | Starts thread                      |
| `run()`         | Thread logic                       |
| `sleep(ms)`     | Pause current thread               |
| `join()`        | Wait until another thread finishes |
| `interrupt()`   | Interrupts thread                  |
| `isAlive()`     | Checks if thread still running     |
| `setPriority()` | Change priority (1–10)             |

---

## 🔹 5. Synchronization

Prevents **race conditions** (multiple threads accessing shared data simultaneously).

```java
class Counter {
    private int count = 0;

    public synchronized void increment() {
        count++;
    }

    public int getCount() { return count; }
}

public class SyncDemo {
    public static void main(String[] args) throws InterruptedException {
        Counter c = new Counter();

        Thread t1 = new Thread(() -> { for(int i=0;i<1000;i++) c.increment(); });
        Thread t2 = new Thread(() -> { for(int i=0;i<1000;i++) c.increment(); });

        t1.start();
        t2.start();
        t1.join();
        t2.join();

        System.out.println("Count: " + c.getCount());
    }
}
```

---

## 🔹 6. Thread Coordination: `yield()`, `join()`, and `sleep()`

### ⚙️ `yield()`

- Suggests the scheduler to give up the CPU so that other threads can run.
    
- Does **not guarantee** that the thread will pause.
    

```java
Thread.yield();
```

### ⚙️ `join()`

- Makes the current thread wait until another thread completes.
    

```java
t1.join(); // main waits until t1 finishes
```

### ⚙️ `sleep()`

- Suspends the thread for the specified time.
    

```java
Thread.sleep(1000); // 1 sec pause
```

---

## 🔹 7. Advanced Java Concurrency (Executors)

Instead of manually creating threads, use **Executor Framework** (from `java.util.concurrent`).

```java
import java.util.concurrent.*;

public class ExecutorDemo {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(3);

        for (int i = 0; i < 5; i++) {
            executor.execute(() -> System.out.println(Thread.currentThread().getName()));
        }

        executor.shutdown();
    }
}
```

### 🔸 Thread Pools

- `newFixedThreadPool(n)` → fixed number of threads
    
- `newCachedThreadPool()` → creates threads as needed
    
- `newSingleThreadExecutor()` → single thread execution
    

---

## 🔹 8. Real-World Usage (Banking Example)

**Scenario:** Banking microservice

| Operation            | Thread Usage                          |
| -------------------- | ------------------------------------- |
| Deposit/Withdraw     | Parallel transactions per user        |
| Balance Update       | Synchronized section (atomic updates) |
| Notification Service | Runs in separate async thread         |
| Audit Logging        | Uses Executor pool or async service   |
|                      |                                       |

```java
@Async
public void sendTransactionAlert(User user) {
    emailService.send(user.getEmail(), "Transaction Completed");
}
```

> `@Async` in Spring Boot uses a background thread pool (`TaskExecutor`) for parallel execution.

---

## 🔹 9. Thread Safety Tips

- Use `synchronized` or `ReentrantLock` for shared resources.
    
- Use **Concurrent Collections** (`ConcurrentHashMap`, `CopyOnWriteArrayList`).
    
- Avoid mutable shared state.
    
- Prefer `ExecutorService` over manual thread management.
    

---

## 🔹 10. Summary Table

| Concept           | Description                           |
| ----------------- | ------------------------------------- |
| `Thread`          | Represents a single thread            |
| `Runnable`        | Functional interface for thread logic |
| `ExecutorService` | Manages a pool of threads             |
| `@Async` (Spring) | Executes methods asynchronously       |
| `join()`          | Waits for thread completion           |
| `yield()`         | Suggests giving up CPU                |
| `sleep()`         | Suspends execution temporarily        |
| `synchronized`    | Ensures thread-safe access            |

---

**Next Level:** Learn `CompletableFuture`, `ForkJoinPool`, and Reactive Streams for non-blocking async systems.