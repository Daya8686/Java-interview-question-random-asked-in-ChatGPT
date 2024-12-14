## poll() and remove() methods in Java

In Java, the `poll()` and `remove()` methods are commonly used in the context of collections like `Queue`. Both methods are used to retrieve and remove the head of the queue, but they differ in how they handle empty collections.

### poll()

- Retrieves and removes the head of the queue.
- If the queue is empty, it returns `null` instead of throwing an exception.

Example:

```java
Queue<Integer> queue = new LinkedList<>();
Integer head = queue.poll(); // returns null if the queue is empty
```

### remove()

- Retrieves and removes the head of the queue.
- If the queue is empty, it throws a `NoSuchElementException`.

Example:

```java
Queue<Integer> queue = new LinkedList<>();
Integer head = queue.remove(); // throws NoSuchElementException if the queue is empty
```
