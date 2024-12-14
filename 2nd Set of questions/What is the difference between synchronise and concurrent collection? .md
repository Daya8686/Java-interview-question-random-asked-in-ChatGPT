### What is the difference between synchronise and concurrent collection?
## Difference Between Synchronized and Concurrent Collections

### Synchronized Collections

- **Thread Safety:** These collections ensure thread safety by synchronizing the entire collection. Only one thread can access the collection at a time.
- **Examples:** `Collections.synchronizedList()`, `Vector`, `Hashtable`.
- **Drawback:** Performance can degrade as it locks the entire collection, causing contention between threads.

Example:

```java
List<String> synchronizedList = Collections.synchronizedList(new ArrayList<>());
```
### Concurrent Collections

- **Thread Safety:** These collections are specifically designed for concurrent access without locking the entire collection, allowing better performance in multi-threaded environments.
- **Examples:** `ConcurrentHashMap`, `CopyOnWriteArrayList`, `ConcurrentLinkedQueue`.
- **Advantage:** More fine-grained locking or lock-free mechanisms provide better concurrency performance.

Example:

```java
ConcurrentMap<String, String> map = new ConcurrentHashMap<>();
```
