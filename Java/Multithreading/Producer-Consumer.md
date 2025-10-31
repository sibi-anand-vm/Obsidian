# 🧵 Producer–Consumer Pattern in Java (Using wait() and notify())

## 🧠 1. Introduction

The **Producer–Consumer problem** is a classic example of thread synchronization where:

- One thread (**Producer**) generates data or items.
    
- Another thread (**Consumer**) processes or consumes those items.
    
- Both share a **common buffer (container)**.
    

To prevent issues like overfilling or consuming from an empty buffer, Java provides `wait()` and `notify()` methods for coordination.

---

## ⚙️ 2. How It Works

- The **Producer** adds elements to the buffer until it reaches a maximum size.
    
- If the buffer is **full**, the producer thread calls `wait()` and releases the lock.
    
- The **Consumer** removes elements from the buffer.
    
- If the buffer is **empty**, the consumer thread calls `wait()`.
    
- Whenever an item is added or removed, the active thread calls `notify()` to wake up the other waiting thread.
    

---

## 🧩 3. Rules

1. Both `wait()` and `notify()` must be called **inside a synchronized block**.
    
2. The thread must **own the monitor lock** of the object it calls `wait()` or `notify()` on.
    
3. `wait()` temporarily **releases the lock**, allowing other threads to acquire it.
    

---

## 💻 4. Example Code

```java
package com.jocata.Synchronization;

import java.util.LinkedList;
import java.util.List;

public class ProducerConsumer {
    public static void main(String[] args) {

        Worker worker = new Worker();

        Thread producer = new Thread(() -> {
            try {
                worker.produce();
            } catch (InterruptedException e) {
                System.out.println(e.getMessage());
            }
        });

        Thread consumer = new Thread(() -> {
            try {
                worker.consume();
            } catch (InterruptedException e) {
                System.out.println(e.getMessage());
            }
        });

        producer.start();
        consumer.start();
    }

    static class Worker {

        private final int TOP = 5;
        private final int BOTTOM = 0;
        private int sequenceNo = 0;

        private final List<Integer> container = new LinkedList<>();
        private final Object lock = new Object();

        void produce() throws InterruptedException {
            synchronized (lock) {
                while (true) {
                    if (container.size() == TOP) {
                        System.out.println("Container is full. Producer waiting...");
                        lock.wait();
                    } else {
                        System.out.println("Adding " + sequenceNo + " to container.");
                        container.add(sequenceNo++);
                        lock.notify();
                    }
                    Thread.sleep(500);
                }
            }
        }

        void consume() throws InterruptedException {
            synchronized (lock) {
                while (true) {
                    if (container.size() == BOTTOM) {
                        System.out.println("Container is empty. Consumer waiting...");
                        lock.wait();
                    } else {
                        System.out.println("Removing " + container.removeFirst() + " from container.");
                        lock.notify();
                    }
                    Thread.sleep(500);
                }
            }
        }
    }
}
```

### For parallel Adding and remove items version
```java
package com.jocata.Synchronization;  
  
import java.util.LinkedList;  
import java.util.List;  
  
public class ProducerConsumer {  
    public static void main(String[] args) {  
  
        Worker worker = new Worker();  
  
        Thread producer = new Thread(() -> {  
            try {  
                worker.produce();  
            } catch (InterruptedException e) {  
                System.out.println(e.getMessage());  
            }  
        });  
  
        Thread consumer = new Thread(() -> {  
            try {  
                worker.consume();  
            } catch (InterruptedException e) {  
                System.out.println(e.getMessage());  
            }  
        });  
  
        producer.start();  
        consumer.start();  
    }  
  
    static class Worker {  
  
        private final int TOP = 5;  
        private final int BOTTOM = 0;  
        private int sequenceNo = 0;  
  
        private final List<Integer> container = new LinkedList<>();  
        private final Object lock = new Object();  
  
        void produce() throws InterruptedException {  
            while (true) {  
                synchronized (lock) {  
                    while (container.size() == TOP) {  
                        System.out.println("Container is full. Producer waiting...");  
                        lock.wait();  
                    }  
                    System.out.println("Adding " + sequenceNo + " to container.");  
                    container.add(sequenceNo++);  
                    lock.notify();  
                }  
                Thread.sleep(500);  
            }  
        }  
  
        void consume() throws InterruptedException {  
            while (true) {  
                synchronized (lock) {  
                    while (container.size() == BOTTOM) {  
                        System.out.println("Container is empty. Consumer waiting...");  
                        lock.wait();  
                    }  
                    int removed = container.remove(0);  
                    System.out.println("Removing " + removed + " from container.");  
                    lock.notify();  
                }  
                Thread.sleep(1000);  
            }  
        }  
    }  
}
```
---

## 🧠 5. Explanation

- The **Producer** thread keeps adding items to the container until it reaches the `TOP` limit.
    
- The **Consumer** thread removes items from the container until it’s empty.
    
- When the container is full, the producer waits.
    
- When the container is empty, the consumer waits.
    
- Both alternate their execution through `wait()` and `notify()` calls.
    

---

## ⚖️ 6. Why This Works

- The `while(true)` loop is placed **inside the synchronized block**.
    
- Each time `wait()` is called, it **releases the lock** so the other thread can enter.
    
- `notify()` wakes up the other waiting thread, which reacquires the lock and continues.
    
- The use of `LinkedList` allows easy use of `removeFirst()` and acts like a queue.
    

---

## 💡 7. Real-World Uses

|Context|Producer|Consumer|
|---|---|---|
|Web Server|Request Handler|Worker Thread|
|Data Pipeline|Data Source|Processor Thread|
|Messaging Systems|Message Publisher|Subscriber|
|Video Processing|Frame Decoder|Renderer|

---

## 🧭 8. Summary

- `wait()` → releases lock and pauses thread.
    
- `notify()` → wakes one waiting thread.
    
- `notifyAll()` → wakes all waiting threads.
    
- Used to coordinate threads sharing a common buffer.
    

✅ **The Producer–Consumer pattern enables smooth communication between threads without busy waiting!**