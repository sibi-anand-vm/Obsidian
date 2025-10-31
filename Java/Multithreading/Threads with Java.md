### 🧠 <font color="#ff0000">**Concurrency and Thread Management in Java**</font>

In Java, when we create and start threads using the `Thread` class or the `ExecutorService`, **the JVM handles thread creation and scheduling at the user level**, but **actual execution is managed by the operating system (kernel level)**.

✅ **Breakdown:**

1. **User-Level (JVM Side)**
    
    - The JVM provides the **abstraction** for threads (`java.lang.Thread`, `Runnable`, `Callable`, etc.).
        
    - It manages thread lifecycle — creation, start, run, sleep, wait, notify, etc.
        
    - But the JVM itself **does not schedule threads directly** on the CPU.
        
2. **Kernel-Level (OS Side)**
    
    - The JVM internally maps each Java thread to a **native OS thread** (known as a _1:1 threading model_).
        
    - The **OS kernel’s scheduler** decides when and on which CPU core each thread runs.
        
    - So actual context switching, time-slicing, and CPU allocation are handled by the **operating system**, not the JVM.
        

---

### ⚙️ **In Summary**

|Layer|Role|Example|
|---|---|---|
|**JVM (User Level)**|Creates and manages Java thread objects|`new Thread(() -> {...}).start()`|
|**OS Kernel**|Schedules and executes native threads on CPU|Context switching, load balancing|
|**CPU**|Executes machine instructions of threads|Parallel or time-sliced|
```java
package com.jocata;  
  
import com.jocata.ThreadImpl.RunnableInterface.Thread1;  
import com.jocata.ThreadImpl.ThreadClass.Thread2;  
  
public class Main {  
    public static void main(String[] args) {  
  
        Thread t1=new Thread(new Thread1());  
        Thread t2=new Thread2();  
  
        t1.start();  
        t2.start();  
  
    }  
}
```

✅ **Both threads run concurrently** (independent of each other).  
Each will execute its `run()` method in parallel.

---

### 🧩 What Happens Behind the Scenes

|Thread|How it’s created|How it runs|
|---|---|---|
|`t1`|Wraps a `Runnable` (`Thread1`) inside a `Thread` object|JVM calls `Thread1.run()`|
|`t2`|Directly a subclass of `Thread`|JVM calls `Thread2.run()`|

So internally, both lead to a `run()` method being executed in separate threads.

### <font color="#ff0000">Join Method</font>

![[Pasted image 20251017135913.png]]
Yes, the usage of the `join()` method in this code makes the main thread wait until both threads `one` and `two` complete their execution before proceeding to execute further statements.

- `one.join();` causes the main thread to wait for thread `one` to finish.
    
- `two.join();` causes the main thread to wait for thread `two` to finish.
    
- **Only after** both threads have finished, the main thread resumes and prints `"Done executing the threads!"`.

This ensures that the main thread does not proceed past the `join()` lines until both `one` and `two` have completed their tasks.

![[Pasted image 20251017140246.png]]

### <font color="#ff0000">Daemon Threads</font>
![[Pasted image 20251017141245.png]]
### 🧠 **Daemon Threads — Explained Clearly**

> **Daemon threads** are **background service threads** that provide support to **user threads**.

---

### ⚙️ **Key Properties**

1. 🟢 **Runs in background:**  
    Daemon threads run in the background performing tasks like garbage collection, cleanup, or monitoring.
    
2. ⚪ **Low priority (usually):**  
    They often have lower priority — but this isn’t enforced by the JVM automatically.  
    You _can_ change it manually using `setPriority()`, but it’s not required.
    
3. 🔴 **JVM termination rule:**  
    👉 When **all user (non-daemon) threads finish**,  
    the **JVM automatically terminates**, even if daemon threads are still running.
    
    This means daemon threads **do not prevent the JVM from shutting down**.
    
4. 🧩 **Created by marking a thread as daemon:**
    
```js
Thread t = new Thread(...);
 t.setDaemon(true); 
 t.start();
```
    
    > ⚠️ You must call `setDaemon(true)` **before** calling `start()`.
    

---

### ✅ Example

```java
public class DaemonExample {
    public static void main(String[] args) {
        Thread daemon = new Thread(() -> {
            while (true) {
                System.out.println("Daemon thread running...");
                try { Thread.sleep(500); } catch (InterruptedException e) {}
            }
        });

        daemon.setDaemon(true);
        daemon.start();

        // User thread
        for (int i = 0; i < 3; i++) {
            System.out.println("User thread working...");
            try { Thread.sleep(1000); } catch (InterruptedException e) {}
        }

        System.out.println("User thread finished → JVM ends, daemon stops!");
    }
}

```

🧩 **Output (example):**

```
Daemon thread running...
User thread working...
Daemon thread running...
User thread working...
User thread finished → JVM ends, daemon stops!
```

👉 JVM exits even though daemon thread is still looping.

---

### 🧾 In short:

> “Daemon threads run in the background (usually low priority).  
> When all user threads finish, JVM terminates immediately,  
> even if daemon threads haven’t completed.”

### <font color="#ff0000">Thread Priority</font>
## 🧵 Main Thread and Thread Priority in Java (In Short)

- **Main Thread:** Automatically created by JVM to run `main()`. Always starts first.
    
- **Thread Creation:** Other threads begin **only after `.start()`** is called in the main thread. Priority does not affect this.
    
- **Thread Priority:** Ranges from 1–10; only hints the OS scheduler **after threads start**. Higher priority may get more CPU time, but main always executes first.

- Every thread has a **priority** (integer value 1–10).
    
- **Default:** `Thread.NORM_PRIORITY = 5`
    
- **Min:** `Thread.MIN_PRIORITY = 1`
    
- **Max:** `Thread.MAX_PRIORITY = 10`

### Summary

| Concept                    | Description                                  |
| -------------------------- | -------------------------------------------- |
| **Main Thread**            | Automatically created by JVM to run `main()` |
| **Start Order**            | Main always starts first                     |
| **New Threads**            | Begin only after `.start()` is called        |
| **Priority Range**         | 1 (MIN) → 5 (NORM, default) → 10 (MAX)       |
| **Effect of Priority**     | Hint to scheduler, not a guarantee           |
| **Main Thread’s Priority** | Usually `Thread.NORM_PRIORITY` (5)           |

```js

public class PriorityExample {
    public static void main(String[] args) {
    
        Thread high = new Thread(() -> System.out.println("High priority thread"));
        high.setPriority(Thread.MAX_PRIORITY);

        Thread low = new Thread(() -> System.out.println("Low priority thread"));
        low.setPriority(Thread.MIN_PRIORITY);

        System.out.println("Main thread starts first!");
        high.start();
        low.start();
    }
}

```

🧩 **Output (typical):**
```
Main thread starts first!
High priority thread
Low priority thread
```