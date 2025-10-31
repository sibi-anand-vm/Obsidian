# 🧵 ExecutorService in Java

ExecutorService is a framework in Java that **manages a pool of threads** efficiently, instead of creating threads manually. It automates **thread creation, task assignment, and shutdown**.

---

## 1️⃣ SingleThreadExecutor

- Executes **all tasks sequentially** with a single thread.
    
- Tasks are **queued** and executed **in order**.
    

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class SingleThreadExecutor {
    public static void main(String[] args) {
        try (ExecutorService service = Executors.newSingleThreadExecutor()) {
            for (int i = 0; i < 5; i++) {
                service.execute(new Task(i));
            }
        }
    }

    static class Task implements Runnable {
        private int taskId;
        Task(int taskId) { this.taskId = taskId; }
        @Override
        public void run() {
            System.out.println("Task:" + taskId + " executed by thread " + Thread.currentThread().getName());
        }
    }
}
```

---

## 2️⃣ FixedThreadPoolExecutor

- Executes tasks using a **fixed number of threads**.
    
- Tasks are queued if all threads are busy.
    

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class FixedThreadPoolExecutor {
    public static void main(String[] args) {
        try (ExecutorService service = Executors.newFixedThreadPool(2)) {
            for (int i = 0; i < 5; i++) {
                service.execute(new Task(i));
            }
        }
    }

    static class Task implements Runnable {
        private int taskId;
        Task(int taskId) { this.taskId = taskId; }
        @Override
        public void run() {
            System.out.println("Task:" + taskId + " executed by thread " + Thread.currentThread().getName());
        }
    }
}
```

---

## 3️⃣ CachedThreadPoolExecutor

- Dynamically creates threads as needed and **reuses idle threads**.
    
- Idle threads are removed if free for 60 seconds.
    

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class CachedThreadPoolExecutor {
    public static void main(String[] args) {
        try (ExecutorService service = Executors.newCachedThreadPool()) {
            for (int i = 0; i < 1000; i++) {
                service.execute(new Task(i));
            }
        }
    }

    static class Task implements Runnable {
        private int taskId;
        Task(int taskId) { this.taskId = taskId; }
        @Override
        public void run() {
            System.out.println("Task:" + taskId + " executed by thread " + Thread.currentThread().getName());
        }
    }
}
```

---

## 4️⃣ ScheduledThreadPoolExecutor

- Executes tasks **after a delay** or **at fixed intervals**.
    

```java
import java.util.concurrent.Executors;
import java.util.concurrent.ScheduledExecutorService;
import java.util.concurrent.TimeUnit;

public class ScheduledThreadPoolExecutorExample {
    public static void main(String[] args) {
    
        ScheduledExecutorService service = Executors.newScheduledThreadPool(1);

        service.scheduleAtFixedRate(new Task(), 1000, 2000, TimeUnit.MILLISECONDS);

        try {
            if (!service.awaitTermination(5000, TimeUnit.MILLISECONDS))
                service.shutdown();
        } catch (InterruptedException e) {
            service.shutdown();
        }
    }

    static class Task implements Runnable {
        @Override
        public void run() {
            System.out.println("Task executed by thread " + Thread.currentThread().getName());
        }
    }
}
```

---

## 5️⃣ Ideal Thread Pool Size

- **Depends on CPU cores, task type, and system load.**
    

### Guidelines:

- **CPU-Intensive Tasks**: Pool size ≈ number of CPU cores.
    
- **IO-Intensive Tasks**: Pool size > number of cores (threads can wait while IO completes).
    
- Avoid creating **too many threads**, which causes context-switching overhead.
    

```java
int cores = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(cores);
```

### Notes:

- CPU cores should **not be fully consumed** — leave some cores for OS and background processes.
    
- More threads than cores is fine for **IO-intensive tasks**.
    
- Fewer threads than cores for **CPU-intensive tasks** is generally better.
    

---

✅ **Summary Table**

| Executor Type        | Threads | Task Handling                              | Use Case               |
| -------------------- | ------- | ------------------------------------------ | ---------------------- |
| SingleThreadExecutor | 1       | Sequential                                 | Maintain task order    |
| FixedThreadPool      | Fixed n | Queued tasks executed in parallel          | Limited parallelism    |
| CachedThreadPool     | Dynamic | Reuses idle threads, creates new if needed | Many short-lived tasks |
| ScheduledThreadPool  | Fixed n | Executes delayed or periodic tasks         | Timed/background tasks |

# 🧵 CPU-Intensive vs IO-Intensive Tasks with ExecutorService

ExecutorService thread pool size should depend on **task type**: CPU-intensive or IO-intensive.

---

## 1️⃣ CPU-Intensive Tasks

**Characteristics:**

- Heavy computations (image processing, math calculations, etc.)
    
- Threads continuously use the CPU
    
- Pool size ≈ number of CPU cores to minimize context switching
    

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class CpuIntensiveExample {
    public static void main(String[] args) {
        int cores = Runtime.getRuntime().availableProcessors();
        ExecutorService executor = Executors.newFixedThreadPool(cores);

        for (int i = 0; i < cores; i++) {
            executor.submit(() -> {
                long sum = 0;
                for (long j = 0; j < 1_000_000_000; j++) {
                    sum += j;
                }
                System.out.println("Sum calculated by " + Thread.currentThread().getName());
            });
        }
        executor.shutdown();
    }
}
```

✅ **Key Point:**

- Avoid creating more threads than CPU cores.
    

---

## 2️⃣ IO-Intensive Tasks

**Characteristics:**

- Waiting for network, file, or database operations
    
- Threads often idle while waiting for I/O
    
- Pool size can be larger than CPU cores to keep CPU busy
    

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class IoIntensiveExample {
    public static void main(String[] args) {
        int cores = Runtime.getRuntime().availableProcessors();
        ExecutorService executor = Executors.newFixedThreadPool(cores * 2); // larger pool for I/O

        for (int i = 0; i < 10; i++) {
            executor.submit(() -> {
                try {
                    System.out.println("Thread " + Thread.currentThread().getName() + " performing I/O");
                    Thread.sleep(2000); // simulating I/O wait
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }
            });
        }
        executor.shutdown();
    }
}
```

✅ **Key Point:**

- More threads than cores is okay because many threads will be idle during I/O.
    

---

## 🧭 Summary Table

|Task Type|Pool Size Recommendation|Reason|
|---|---|---|
|CPU-Intensive|≈ # of CPU cores|Avoid too many threads; maximize CPU usage|
|IO-Intensive|> # of CPU cores (e.g., cores × 2)|Threads spend time waiting; more threads keep CPU busy|
