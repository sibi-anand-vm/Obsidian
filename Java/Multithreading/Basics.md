![[Pasted image 20251017102653.png]]

## <font color="#ff0000">Thread</font>

A **thread** is the smallest unit of execution within a process. It represents a single sequence of programmed instructions that can run independently and, often, simultaneously with other threads in the same program.

## What a Thread Does

A thread performs a specific part of a program’s work. Each thread runs its own sequence of instructions, maintains its **program counter** (current instruction), **stack** (local variables), and **registers** (temporary data), but shares memory and resources with other threads in the same process.

![[Pasted image 20251017104245.png]]

- The **kernel** is a core part of the operating system responsible for managing threads and CPU resources.
    
- It **creates**, **tracks**, and **schedules** kernel-level threads.
    
- The **thread scheduler** inside the kernel decides which thread runs next on available CPU cores.
    
- Scheduling decisions are based on factors like **thread priority**, **scheduling policy**, and CPU availability.
    
- **User-level threads** depend on kernel threads for actual execution, but scheduling and resource allocation are controlled by the kernel.
    
- The **scheduling policy** defines rules for thread execution order, priority, and time slices to ensure fairness and performance.
    
- Common scheduling policies include:
    
    - **First-Come, First-Served (FCFS):** Threads run in order of arrival.
        
    - **Round Robin (RR):** Threads share CPU time equally in turns.
        
    - **First In, First Out (FIFO):** Real-time threads run until they block or yield.
        
    - **Priority Scheduling:** Threads with higher priority run first.
        
    - **Deadline-based (EDF):** Tasks scheduled by earliest deadlines.
### 🧩<font color="#ff0000"> **Concurrency vs Parallelism (Simplified Explanation)**</font>

**Concurrency**

> Concurrency means _dealing with multiple tasks at once_.  
> It’s about _managing_ multiple threads or processes so they make progress together — not necessarily _executing simultaneously_.  
> Threads may start and finish at different times, and the CPU **interleaves** their execution (e.g., switching between them quickly).

✅ Example:  
Single-core CPU running multiple threads by time-slicing — gives the _illusion_ of parallel execution.

![[Pasted image 20251017104352.png]]

**Parallelism**

> Parallelism means _doing multiple tasks at the same exact time_.  
> It requires multiple CPU cores (or processors).  
> Each thread runs **simultaneously** and often starts and finishes around the same time — actual _simultaneous execution_.

✅ Example:  
Multi-core CPU running 4 threads at the same time — one per core.

![[Pasted image 20251017104421.png]]

![[Pasted image 20251017104508.png]]

### <font color="#ff0000">Thread Lifecycle</font>

- **New State:** Thread is created, not started. It stays here until `start()` is called.[](https://uncodemy.com/blog/thread-life-cycle-in-java)​

- **Runnable State:** The thread can run but is waiting for CPU time. This means it might be running or just waiting for a core.
    
- **Running State:** Actively executing on a CPU core.

- **Waiting State:** Entered when a thread calls `join()` on another thread or `wait()` on an object. The thread will stay here until notified, interrupted, or the other thread completes and allows it to resume.[](https://blog.ycrash.io/java-suspended-thread-states-blocked-waiting-timed_waiting/)​
    
	Example:** If thread A calls `threadB.join()`, thread A will be in the waiting state until thread B finishes its work.

- **Terminated State:** After the thread finishes its execution (completes the run method or encounters an error), it moves to this state.

![[Pasted image 20251017105454.png]]

### <font color="#ff0000">Threads Methods</font>

| Method          | Description                        |
| --------------- | ---------------------------------- |
| `start()`       | Starts thread                      |
| `run()`         | Thread logic                       |
| `sleep(ms)`     | Pause current thread               |
| `join()`        | Wait until another thread finishes |
| `interrupt()`   | Interrupts thread                  |
| `isAlive()`     | Checks if thread still running     |
| `setPriority()` | Change priority (1–10)             |
