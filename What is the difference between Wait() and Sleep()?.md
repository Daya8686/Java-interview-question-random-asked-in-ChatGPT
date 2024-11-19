# What is the difference between Wait() and Sleep()?

# wait() Method in Java

The `wait()` method is used in Java for thread synchronization, specifically for inter-thread communication. A thread that calls `wait()` goes into a waiting state until another thread calls `notify()` or `notifyAll()` on the same object.

## Key Points about `wait()` Method:
- **Purpose**: Used for inter-thread communication. A thread that calls `wait()` goes into a waiting state until another thread calls `notify()` or `notifyAll()` on the same object.
- **Synchronization Requirement**: `wait()` must be called from within a synchronized block or method. This ensures that the thread calling `wait()` holds the object's lock before releasing it. When `wait()` is called, the thread releases the lock and goes into a waiting state until it is notified.

### Example of `wait()`:
```java
class SharedResource {
    synchronized void waitForSignal() {
        try {
            System.out.println(Thread.currentThread().getName() + " is waiting...");
            wait(); // Releases the lock and waits
            System.out.println(Thread.currentThread().getName() + " is resumed.");
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
            System.out.println("Thread interrupted");
        }
    }

    synchronized void sendSignal() {
        System.out.println(Thread.currentThread().getName() + " is sending signal...");
        notify(); // Notifies one waiting thread to resume
    }
}

public class WaitExample {
    public static void main(String[] args) {
        SharedResource resource = new SharedResource();

        Thread t1 = new Thread(() -> resource.waitForSignal(), "Thread 1");
        Thread t2 = new Thread(() -> resource.sendSignal(), "Thread 2");

        t1.start();
        try {
            Thread.sleep(1000); // Ensures that Thread 1 waits before Thread 2 sends the signal
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
        t2.start();
    }
}
```
Output:
```java
Thread 1 is waiting...
Thread 2 is sending signal...
Thread 1 is resumed.
```

### Explanation:
- **Thread 1** calls `waitForSignal()` and enters the synchronized method. It then calls `wait()`, releasing the lock on the `SharedResource` object and waiting to be notified.
- **Thread 2** enters the synchronized `sendSignal()` method, where it calls `notify()`. This notifies `Thread 1` to resume execution, which reacquires the lock and continues.

# sleep() Method
### Purpose:
The `sleep()` method is used to pause the execution of the current thread for a specified period. It simply makes the thread sleep for a given duration.

### Synchronization Requirement:
`sleep()` does not require the thread to hold any lock, and it can be called from anywhere, even outside a synchronized block.

Example of sleep():
```java

class SleepExample {
    void simulateWork() {
        System.out.println(Thread.currentThread().getName() + " is going to sleep...");
        try {
            Thread.sleep(2000); // Sleeps for 2 seconds
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
        System.out.println(Thread.currentThread().getName() + " has woken up.");
    }
}

public class SleepDemo {
    public static void main(String[] args) {
        SleepExample example = new SleepExample();

        Thread t1 = new Thread(() -> example.simulateWork(), "Thread 1");
        Thread t2 = new Thread(() -> example.simulateWork(), "Thread 2");

        t1.start();
        t2.start();
    }
}

```
Output:
```java
Thread 1 is going to sleep...
Thread 2 is going to sleep...
Thread 1 has woken up.
Thread 2 has woken up.
```
# Key Differences Between `wait()` and `sleep()` in Java

## Explanation:
Both `Thread 1` and `Thread 2` call the `simulateWork()` method, which includes a call to `Thread.sleep(2000)`. This pauses each thread's execution for 2 seconds, after which the threads resume execution.

### Key Differences:

#### `wait()`
- **Synchronization Requirement**: Must be called from within a synchronized block/method.
- **Lock Management**: Releases the lock on the object it is waiting on.
- **Thread State**: The thread enters the waiting state until it is notified.
- **Purpose**: Typically used for inter-thread communication.

#### `sleep()`
- **Synchronization Requirement**: Can be called from anywhere, without needing synchronization.
- **Lock Management**: Does not release any locks or interact with synchronization mechanisms.
- **Thread State**: Pauses the thread for a specified duration, after which the thread resumes.
- **Purpose**: Typically used for pausing execution or simulating delays.

## Summary
- **`wait()`**: A powerful tool for managing thread coordination and communication within synchronized blocks.
- **`sleep()`**: A simple way to introduce a delay in thread execution.
