# 🧵 Callable and Future in Java

Callable tasks allow **returning a result** from a thread asynchronously.  
Future objects act as **placeholders** for the result of a Callable task.

---

## Example: Callable + Future

```java
import java.util.concurrent.*;

public class CallableFuture {
    public static void main(String[] args) {

        try (ExecutorService service = Executors.newFixedThreadPool(3)) {

            Future<Integer> result = service.submit(new Task());

            System.out.println(result.get());

        } catch (ExecutionException | InterruptedException e) {
            throw new RuntimeException(e);
        }
    }

    // Callable task that returns a value
    static class Task implements Callable<Integer> {
        @Override
        public Integer call() throws Exception {
            return 7;
        }
    }
}
```

---
![[Pasted image 20251020132322.png]]

## 🧵 Asynchronous Execution Flow

1. **Submit the Task**
    
    - Main Thread calls `executorService.submit(callableTask)`.
        
    - Thread Pool accepts the task and begins executing it asynchronously.
        
2. **Receive the Future**
    
    - Immediately after submission, a `Future<Integer>` is returned.
        
    - The Future acts as a **placeholder** for the result.
        
3. **Retrieve the Result (Blocking)**
    
    - Calling `future.get()` blocks the main thread.
        
    - Main Thread waits until the task completes and the result is available.
        
4. **Resume Execution**
    
    - Once the task finishes, `future.get()` returns the result.
        
    - Main Thread continues executing the rest of the code.
        

---

### ✅ Key Points

- `.submit()` returns a `Future` **immediately**, task may not have started yet.
    
- `.get()` is a **blocking call**, main thread waits for the result.
    
- Callable tasks are useful for **returning results from asynchronous computations**.
    
- Exceptions in Callable are propagated via **ExecutionException** when calling `.get()`.