## Safely Removing Entries from a Collection While Iterating in Java

To safely remove an entry from a collection while iterating over it in Java, you should use an iterator instead of a regular for loop or foreach loop. This is because directly modifying a collection during iteration can result in a `ConcurrentModificationException`.

### Steps:

1. Obtain an `Iterator` from the collection.
2. Use the `hasNext()` method to loop through the collection.
3. Inside the loop, call `next()` to get the next element.
4. Use the `remove()` method of the `Iterator` to remove the current element safely.

### Example:

```java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class RemoveWhileIterating {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Banana");
        list.add("Orange");
        list.add("Mango");

        // Using an iterator to remove elements
        Iterator<String> iterator = list.iterator();
        while (iterator.hasNext()) {
            String fruit = iterator.next();
            if ("Banana".equals(fruit)) {
                iterator.remove(); // Safely remove "Banana" from the list
            }
        }

        // Print the remaining elements
        System.out.println(list); // Output: [Apple, Orange, Mango]
    }
}
```

## Key Points

- **iterator.remove():** This method removes the current element that was returned by `next()`. It ensures safe removal without throwing `ConcurrentModificationException`.
- **Do not modify the collection directly inside a for-each loop or a regular for loop,** as it may cause runtime exceptions due to concurrent modification.

### Using ListIterator (for List collections)

If you're working with a `List` and need bidirectional iteration, you can use `ListIterator`, which provides additional functionality such as adding, replacing, and traversing in reverse.

Example:

```java
ListIterator<String> listIterator = list.listIterator();
while (listIterator.hasNext()) {
    String fruit = listIterator.next();
    if ("Orange".equals(fruit)) {
        listIterator.remove(); // Safely remove "Orange"
    }
}
```
## Reverse Traversal Example

After a forward traversal, you can use the `ListIterator` to iterate in reverse by using the `hasPrevious()` and `previous()` methods.

### Example:

```java
import java.util.ArrayList;
import java.util.List;
import java.util.ListIterator;

public class ListIteratorExample {
    public static void main(String[] args) {
        List<String> rivers = new ArrayList<>();
        rivers.add("Nile");
        rivers.add("Amazon");
        rivers.add("Yangtze");
        rivers.add("Ganges");

        // Create a ListIterator to iterate through the list
        ListIterator<String> iterator = rivers.listIterator(rivers.size()); // Start at the end

        System.out.println("Reverse traversal:");
        while (iterator.hasPrevious()) {
            // Move backward through the list
            String river = iterator.previous();
            System.out.println(river);
        }
    }
}
```
## Key Methods of ListIterator -
 **next():** Returns the next element and moves the cursor forward.
 - **hasNext():** Returns `true` if there are more elements to traverse forward.
 - **previous():** Returns the previous element and moves the cursor backward.
 - **hasPrevious():** Returns `true` if there are elements to traverse backward. -
 -  **remove():** Removes the last element returned by either `next()` or `previous()`.
 - **add(E e):** Inserts the specified element into the list (can be used while traversing).
 - **set(E e):** Replaces the last element returned by `next()` or `previous()` with the specified element.
