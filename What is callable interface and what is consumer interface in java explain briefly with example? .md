

### 1. What is callable interface and what is consumer interface in java explain briefly with example?


  
  ### Callable interface

The **`Callable`**  interface is part of the **`java.util.concurrent`** package and represents a task that can be executed by a thread. It is similar to the **`Runnable`** interface but has a few key differences:
1. **Return Value:** A `Callable` can return a result after it completes its execution.
2. **Exception Handling:**  A `Callable` can throw checked exceptions.

#### Key Method
* `V call() throws Exception:` This method, when implemented, contains the task's logic and returns a result of type `V`.
### Example of Callable

``` java 

import java.util.concurrent.Callable;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

public class CallableExample {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newSingleThreadExecutor();
        
        Callable<Integer> callableTask = () -> {
            // Task logic here
            Thread.sleep(1000);
            return 42;
        };
        
        Future<Integer> future = executor.submit(callableTask);
        
        try {
            Integer result = future.get(); // Get the result of the callable task
            System.out.println("Result: " + result);
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            executor.shutdown();
        }
    }
}
```

# Consumer Interface

The Consumer interface is part of the `java.util.function` package and represents an operation that accepts a single input argument and returns no result. It is typically used for operations that process or consume an input argument.

## Key Method
`void accept(T t):` This method, when implemented, performs the operation on the given argument `t`.
### Example of Consumer
```java
import java.util.function.Consumer;

public class ConsumerExample {
    public static void main(String[] args) {
        Consumer<String> greeter = (name) -> System.out.println("Hello, " + name + "!");
        
        greeter.accept("Alice");
        greeter.accept("Bob");
    }
}

```
# Summary

## Callable:
- **Returns a result.**
- **Can throw checked exceptions.**
- **Useful for tasks that need to return a value or throw an exception.**

## Consumer:
- **Does not return a result.**
- **Does not throw checked exceptions.**
- **Useful for operations that consume an input and perform some action with it.**

Both interfaces are used to define tasks and operations in a clear and concise manner, leveraging Java's functional programming capabilities.

---
