## What are the different stages of thread explain in a brief with points in Java?

## Stages of a Thread in Java (Thread Life Cycle)

A thread in Java goes through various stages during its life cycle:

- **New:** When a thread is created but not yet started. It’s in the new state.
Example:
```Java
Thread t = new Thread();

```
- **Runnable:** After calling the `start()` method, the thread is in the runnable state. It may be running or waiting for CPU time.
Example:
```Java
t.start();

```
- **Blocked/Waiting:** The thread is not currently runnable but might be runnable again in the future. It is waiting for a monitor lock or for a signal from another thread.
Example:
```Java
synchronized (object) {
    object.wait(); // Thread enters waiting state
}

```
- **Timed Waiting:** A thread is in a timed waiting state when it calls methods like `sleep()` or `wait()` with a timeout.
Example:
```Java
Thread.sleep(1000); // Timed waiting for 1 second

```
- **Terminated:** When the thread has completed execution, it reaches the terminated state.

Example:
```Java
public void run() {
    System.out.println("Thread finished execution");
}

```
