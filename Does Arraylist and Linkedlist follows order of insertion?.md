# Does Arraylist and Linkedlist follows order of insertion?

# Maintaining Order of Insertion in Java

Yes, both `ArrayList` and `LinkedList` in Java maintain the order of insertion. This means that the elements are stored and retrieved in the same order in which they were added.

## ArrayList
`ArrayList` is a resizable array implementation of the `List` interface. It maintains the insertion order of elements. Here’s a quick example:

```java
import java.util.ArrayList;
import java.util.List;

public class ArrayListExample {
    public static void main(String[] args) {
        List<String> arrayList = new ArrayList<>();
        arrayList.add("A");
        arrayList.add("B");
        arrayList.add("C");

        System.out.println(arrayList); // Output: [A, B, C]
    }
}
```
In the example above, the elements "A", "B", and "C" are added to the `ArrayList` in that order, and they are stored and retrieved in the same order.

## LinkedList
`LinkedList` is a doubly linked list implementation of the `List` and `Deque` interfaces. It also maintains the insertion order of elements. Here’s an example:

```java
import java.util.LinkedList;
import java.util.List;

public class LinkedListExample {
    public static void main(String[] args) {
        List<String> linkedList = new LinkedList<>();
        linkedList.add("X");
        linkedList.add("Y");
        linkedList.add("Z");

        System.out.println(linkedList); // Output: [X, Y, Z]
    }
}
```

In the example above, the elements "X", "Y", and "Z" are added to the `LinkedList` in that order, and they are stored and retrieved in the same order.

## Comparison of ArrayList and LinkedList
While both `ArrayList` and `LinkedList` maintain the order of insertion, they have different performance characteristics:

### ArrayList:
- **Access Time**: O(1) for get operations because it uses an array internally.
- **Insertion Time**: O(n) in the worst case for add operations (when resizing the array).
- **Memory**: Less memory overhead compared to `LinkedList`.

### LinkedList:
- **Access Time**: O(n) for get operations because it requires traversal from the head of the list.
- **Insertion Time**: O(1) for add operations at the beginning or end of the list.
- **Memory**: More memory overhead due to storage of pointers for the next and previous elements.

## Conclusion
Both `ArrayList` and `LinkedList` maintain the order of insertion. The choice between them should be based on the specific performance needs of your application, such as whether you require fast access times (favoring `ArrayList`) or frequent insertions and deletions (favoring `LinkedList`).
