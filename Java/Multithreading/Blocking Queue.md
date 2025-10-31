# 🧵 BlockingQueue in Java

## 🔹 Overview

`BlockingQueue` is a **thread-safe (synchronized)** or **concurrent** collection used to handle producer-consumer type problems. It ensures safe communication between multiple threads by blocking operations when needed.

There are **two main implementations**:

1. **BlockingDeque** — a double-ended blocking queue.
    
2. **TransferQueue** — allows direct handoff between producer and consumer.
    

---

## 🔹 How BlockingDeque Works

- When adding an element:
    
    - ✅ If space is available → element is added.
        
    - ⛔ If queue is **full** → the thread **waits (blocks)** until space becomes available.
        
- When taking an element:
    
    - ✅ If elements exist → removes and returns one.
        
    - ⛔ If queue is **empty** → the thread **waits (blocks)** until an element is available.
        

---

## 🔹 How TransferQueue Works

- If a **consumer** tries to take from an **empty queue**, it will **block** until a producer provides an element.
    
- A **producer** can directly **transfer** an element to a waiting consumer instead of putting it into the queue.
    

✅ So, if the producer is ready with an element, the consumer can immediately receive it — no need to store it in the queue.

---

## 🔹 Major Implementations

- `ArrayBlockingQueue`
    
- `LinkedBlockingQueue`
    
- `PriorityBlockingQueue`
    
- `DelayQueue`
    
- `SynchronousQueue`
    

---

## 🔹 BlockingQueue Operations

|Operation|Behavior|
|---|---|
|**put(E e)**|Adds an element if space is available; blocks if full.|
|**take()**|Removes and returns the head element; blocks if empty.|
|**add(E e)**|Adds an element, throws exception if full.|
|**poll()**|Retrieves and removes head element; returns `null` if empty.|
|**peek()**|Retrieves (but doesn’t remove) head element; returns `null` if empty.|

---


# 🧵 BlockingQueue Implementation in Java

- **put()** → blocks if queue is full
    
- **take()** → blocks if queue is empty
    
- Eliminates manual `synchronized`, `wait()`, and `notify()` calls.
    

---

## 💻 Example Code

```java
package com.jocata.ConcurrentCollection;

import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.BlockingQueue;

public class BlockingQueueImpl {

    static BlockingQueue<Integer> blockingQueue = new ArrayBlockingQueue<>(5);

    public static void main(String[] args) throws InterruptedException {

        Thread producer = new Thread(() -> {
            for (int i = 0; i < 20; i++) {
                try {
                    System.out.println("Producer producing: " + i);
                    blockingQueue.put(i);
                    System.out.println("Producer produced: " + i);
                    Thread.sleep(100);
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }
            }
        });

        Runnable consumerTask = () -> {
            try {
                for (int i = 0; i < 10; i++) {
                    Integer value = blockingQueue.take();
                    System.out.println(Thread.currentThread().getName() + " consuming: " + value);
                    Thread.sleep(150);
                    System.out.println(Thread.currentThread().getName() + " consumed: " + value);
                }
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        };

        Thread consumerOne = new Thread(consumerTask, "Consumer-1");
        Thread consumerTwo = new Thread(consumerTask, "Consumer-2");

        producer.start();
        consumerOne.start();
        consumerTwo.start();

        producer.join();
        consumerOne.join();
        consumerTwo.join();
    }
}
```

---

## 🔹 Explanation

- **ArrayBlockingQueue<>(5)** → capacity of 5 elements.
    
- **Producer Thread** → produces 20 items, blocks if queue full.
    
- **Consumer Threads** → consume items, block if queue empty.
    
- **Graceful interrupt handling** → `Thread.currentThread().interrupt()` restores interrupt flag.
    
- **Thread.join()** ensures main thread waits for all threads to finish.
    

---

## ✅ Advantages

- Thread-safe by design.
    
- Proper producer-consumer coordination.
    
- Avoids race conditions.
    
- Scalable: easy to add more producers or consumers.
    
- Clear output due to thread naming.
    

---

## 🧩 Key Takeaways

- `BlockingQueue` simplifies concurrent programming.
    
- Supports multiple implementations: `ArrayBlockingQueue`, `LinkedBlockingQueue`, `PriorityBlockingQueue`, `DelayQueue`, `SynchronousQueue`.
    
- Automatically blocks threads when needed, avoiding busy-waiting.
    
- Ideal for producer-consumer patterns and thread-pool tasks.
## 🧠 Summary

- `BlockingQueue` helps manage **producer-consumer coordination**.
    
- Ensures **thread-safe** queue access.
    
- Provides **blocking behavior** to prevent race conditions.
    
- For high concurrency and performance, prefer `LinkedBlockingQueue` or `SynchronousQueue` depending on your use case.