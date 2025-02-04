A **race condition** occurs in a multi-threaded or concurrent environment when two or more threads or processes access shared resources (like variables, files, or databases) simultaneously, and the outcome of the execution depends on the timing or sequence of their execution.
### Key Points:

1. **Unpredictable Behavior**: The program behaves unpredictably because the execution order is not deterministic.
2. **Shared Resources**: Happens when threads or processes share resources and at least one thread modifies the resource.
3. **Concurrency Issue**: Arises in concurrent programming when proper synchronization is not implemented.
### Example:

Consider two threads trying to increment a shared variable:
```
class Counter {
    int count = 0;

    void increment() {
        count++;
    }
}
public class RaceConditionExample {
    public static void main(String[] args) {
        Counter counter = new Counter();

        Runnable task = () -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        };

        Thread thread1 = new Thread(task);
        Thread thread2 = new Thread(task);

        thread1.start();
        thread2.start();

        try {
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Final count: " + counter.count);
    }
}
```