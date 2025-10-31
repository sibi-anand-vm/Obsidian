# 🧩 CyclicBarrier in Java — Example & Notes

## 🔹 Concept

`CyclicBarrier` is a synchronization aid in Java that allows a **fixed number of threads** to wait for each other at a common barrier point.  
Once all threads reach the barrier, an optional **barrier action** is executed, and then the barrier resets for reuse.

---

## 🧠 Key Points

- Belongs to: `java.util.concurrent`
    
- Used when **multiple threads must meet at a checkpoint** before proceeding.
    
- Once all threads call `await()`, the barrier is released and optionally runs a specified action.
    
- The barrier **automatically resets** after being released, hence the name _cyclic_.
    

---

## 🔧 Example Code

```java
package com.jocata.Synchronization;

import java.util.concurrent.BrokenBarrierException;
import java.util.concurrent.CyclicBarrier;

public class CyclicBarrierExample {

    private static final int numOfTourists = 5;
    private static final int numOfStages = 3;

    private static final CyclicBarrier cyclicBarrier = new CyclicBarrier(numOfTourists, () -> {
        System.out.println("Guide is speaking\n");
    });

    public static void main(String[] args) {
        for (int i = 0; i < numOfTourists; i++) {
            new Thread(new Tourist(i)).start();
        }
    }

    public static class Tourist implements Runnable {

        private final int touristId;

        public Tourist(int i) {
            this.touristId = i;
        }

        @Override
        public void run() {
            try {
                for (int i = 1; i <= numOfStages; i++) {
                    Thread.sleep((long) (Math.random() * 2000)); // random delay
                    System.out.println("Tourist " + touristId + " arrived at stage " + i);

                    // Wait for others to arrive before moving to next stage
                    cyclicBarrier.await();
                }
            } catch (InterruptedException | BrokenBarrierException e) {
                e.printStackTrace();
            }
        }
    }
}
```

---

## 🔊 How It Works

1. Each tourist represents a separate thread.
    
2. All tourists must reach a stage (checkpoint).
    
3. When the last tourist calls `await()`, the barrier action (`Guide is speaking`) executes.
    
4. After the barrier releases, it resets for the next stage.
    

---

## 💨 Output Example

```
Tourist 2 arrived at stage 1
Tourist 0 arrived at stage 1
Tourist 1 arrived at stage 1
Tourist 3 arrived at stage 1
Tourist 4 arrived at stage 1
Guide is speaking

Tourist 1 arrived at stage 2
Tourist 2 arrived at stage 2
Tourist 3 arrived at stage 2
Tourist 0 arrived at stage 2
Tourist 4 arrived at stage 2
Guide is speaking
```

---

## 🔗 Related Classes

- `CountDownLatch` → One-time synchronization, cannot be reset.
    
- `Phaser` → More flexible version for variable parties.
    

---

## 💡 Real-Life Analogy

Think of tourists at checkpoints:  
They can’t proceed to the next point until **everyone arrives**. Once all are ready, the **guide speaks**, and they move together to the next stage.

---

## 🔄 Summary

| Feature              | Description                        |
| -------------------- | ---------------------------------- |
| Package              | `java.util.concurrent`             |
| Synchronization Type | Barrier Point                      |
| Resettable           | Yes (Cyclic)                       |
| Common Use           | Coordinating multi-threaded phases |
| Key Method           | `await()`                          |
| Exception            | `BrokenBarrierException`           |