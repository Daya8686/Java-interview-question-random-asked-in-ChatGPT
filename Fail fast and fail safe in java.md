### 3. Fail fast and fail safe in java

# Fail-Fast and Fail-Safe in Java

In Java, the terms "fail-fast" and "fail-safe" are used to describe the behavior of iterators or collection views when the underlying collection is modified while being iterated over. These behaviors are particularly relevant in concurrent or multi-threaded environments.

## Fail-Fast
Fail-fast iterators and collection views throw a `ConcurrentModificationException` if they detect that the collection has been modified after the iterator was created. This behavior helps to quickly detect concurrent modification issues, ensuring that such problems are not silently ignored, which could lead to unpredictable behavior.

## Fail-Fast Iterators

Fail-fast iterators immediately throw an exception if the collection is structurally modified during iteration (except through the iterator's own methods like `remove()`).

## Key Points
- **Modification Detection**: Fail-fast iterators detect any structural modification (like `add()`, `remove()`, `clear()`) to the collection after the iterator is created.
- **Exception Thrown**: If modification is detected, they throw a `ConcurrentModificationException`.
- **Examples**: Iterators returned by collections like `ArrayList`, `HashMap`, `HashSet`, etc.
- **Usage**: They are generally used in single-threaded environments, as modifications during iteration are often unintended.



### Example of Fail-Fast
Most of the collection classes in `java.util` package (like `ArrayList`, `HashMap`, `HashSet`, etc.) provide fail-fast iterators.

```java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class FailFastExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("one");
        list.add("two");
        list.add("three");

        Iterator<String> iterator = list.iterator();
        while (iterator.hasNext()) {
            String element = iterator.next();
            System.out.println(element);
            // Modifying the list while iterating
            if ("two".equals(element)) {
                list.add("four");
            }
        }
    }
}
```
* This code will throw a `ConcurrentModificationException` when it tries to add "four" to the list while iterating over it.

## Fail-Safe
Fail-safe iterators and collection views do not throw a `ConcurrentModificationException` if the collection is modified during iteration. Instead, they work on a copy of the collection, ensuring that the original collection can be safely modified without affecting the iteration. This behavior is typically implemented in collections that are designed for concurrent access.

## Fail-Safe Iterators

Fail-safe iterators allow modifications to the collection during iteration without throwing exceptions. They work on a copy of the collection's data, not on the original collection.

## Key Points
- **No Exception**: Fail-safe iterators do not throw `ConcurrentModificationException` when the collection is modified during iteration.
- **Work on a Copy**: They operate on a cloned or a snapshot copy of the collection, so structural modifications do not affect the iteration process.
- **Examples**: Iterators returned by collections like `CopyOnWriteArrayList`, `ConcurrentHashMap`, etc.
- **Usage**: Commonly used in concurrent or multi-threaded environments where the collection may be modified by multiple threads.


### Example of Fail-Safe
Classes from the `java.util.concurrent` package (like `CopyOnWriteArrayList`, `ConcurrentHashMap`, etc.) provide fail-safe iterators.

```java
import java.util.Iterator;
import java.util.concurrent.CopyOnWriteArrayList;

public class FailSafeExample {
    public static void main(String[] args) {
        CopyOnWriteArrayList<String> list = new CopyOnWriteArrayList<>();
        list.add("one");
        list.add("two");
        list.add("three");

        Iterator<String> iterator = list.iterator();
        while (iterator.hasNext()) {
            String element = iterator.next();
            System.out.println(element);
            // Modifying the list while iterating
            if ("two".equals(element)) {
                list.add("four");
            }
        }

        // Print the final list
        System.out.println("Final list: " + list);
    }
}
```
