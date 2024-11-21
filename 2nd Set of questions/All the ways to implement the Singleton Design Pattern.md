# All the ways to implement the Singleton Design Pattern

Here are all the ways to implement the Singleton Design Pattern in Java, each with its own trade-offs in terms of thread-safety, lazy initialization, and performance:

### 1. Eager Initialization Singleton
In this approach, the instance is created at the time of class loading. This is a straightforward and thread-safe method, but it does not allow for lazy initialization.

#### Example:
```java

public class EagerSingleton {
    // Create instance at the time of class loading
    private static final EagerSingleton instance = new EagerSingleton();

    private EagerSingleton() {}

    public static EagerSingleton getInstance() {
        return instance;
    }
}
```
- **Pros:** Simple and thread-safe.
- **Cons:** The instance is created even if it is never used, which could waste resources.
---
### 2. Lazy Initialization Singleton
This approach delays the creation of the singleton instance until it is needed (lazy initialization). However, this is not thread-safe unless additional synchronization is added.

#### Example:
```java

public class LazySingleton {
    private static LazySingleton instance;

    private LazySingleton() {}

    public static LazySingleton getInstance() {
        if (instance == null) {
            instance = new LazySingleton();
        }
        return instance;
    }
}
```
- **Pros:** Instance is created only when needed.
- **Cons:** Not thread-safe.
---
### 3. Thread-Safe Singleton with Synchronized Method
In this method, synchronization is added to ensure that the singleton instance is created safely in a multithreaded environment. This approach ensures thread-safety but reduces performance because every call to getInstance() is synchronized.

#### Example:
```java

public class SynchronizedSingleton {
    private static SynchronizedSingleton instance;

    private SynchronizedSingleton() {}

    public static synchronized SynchronizedSingleton getInstance() {
        if (instance == null) {
            instance = new SynchronizedSingleton();
        }
        return instance;
    }
}
```
- **Pros:** Thread-safe.
- **Cons:** Reduced performance due to synchronization overhead on each call.
---
### 4. Thread-Safe Singleton Using Double-Checked Locking
This approach optimizes the synchronized method by using double-checked locking. The instance is only synchronized the first time it is created, avoiding performance degradation after initialization.

#### Example:
```java

public class DoubleCheckedLockingSingleton {
    private static volatile DoubleCheckedLockingSingleton instance;

    private DoubleCheckedLockingSingleton() {}

    public static DoubleCheckedLockingSingleton getInstance() {
        if (instance == null) {
            synchronized (DoubleCheckedLockingSingleton.class) {
                if (instance == null) {
                    instance = new DoubleCheckedLockingSingleton();
                }
            }
        }
        return instance;
    }
}
```
- **Pros:** Thread-safe, with good performance after the instance is created.
- **Cons:** Slightly more complex.
---
### 5. Bill Pugh Singleton (Lazy Initialization with Static Inner Class)
This is one of the most efficient ways to implement a thread-safe singleton. The static inner class (SingletonHelper) holds the singleton instance, and it is only loaded when the getInstance() method is called.

#### Example:
```java

public class BillPughSingleton {
    private BillPughSingleton() {}

    // Inner static class responsible for holding Singleton instance
    private static class SingletonHelper {
        private static final BillPughSingleton INSTANCE = new BillPughSingleton();
    }

    public static BillPughSingleton getInstance() {
        return SingletonHelper.INSTANCE;
    }
}
```
- **Pros:** Thread-safe, lazy-loaded, and no synchronization overhead.
- **Cons:** None.
---
### 6. Enum Singleton
Using an enum is the most straightforward and effective way to create a singleton in Java. It is inherently thread-safe, prevents serialization issues, and is immune to reflection and cloning.

#### Example:
```java
Copy code
public enum EnumSingleton {
    INSTANCE;

    public void someMethod() {
        // Business logic
    }
}
```
- **Pros:** Thread-safe, protects against serialization, cloning, and reflection.
- **Cons:** Not flexible in certain cases (e.g., if you need to lazy-load resources).
