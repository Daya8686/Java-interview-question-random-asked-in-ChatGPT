# What is stack in java and which classes and interfaces are extended and implemented?

# Stack in Java

In Java, a stack is a data structure that follows the Last-In-First-Out (LIFO) principle, where the last element added to the stack is the first one to be removed. The `java.util.Stack` class provides a standard implementation of a stack.

## Stack in Java
The `Stack` class is part of the `java.util` package and extends the `Vector` class. Here is a brief overview of the `Stack` class, its methods, and the hierarchy it follows:

### Hierarchy
* `java.lang.Object`
   * `java.util.AbstractCollection<E>`
      * `java.util.AbstractList<E>`
         * `java.util.Vector<E>`
             * `java.util.Stack<E>`


### Key Methods of Stack
- **`boolean empty()`**: Checks if the stack is empty.
- **`E peek()`**: Looks at the object at the top of the stack without removing it.
- **`E pop()`**: Removes the object at the top of the stack and returns it.
- **`E push(E item)`**: Pushes an item onto the top of the stack.
- **`int search(Object o)`**: Returns the 1-based position where an object is on the stack.

## Example of Using Stack

```java
import java.util.Stack;

public class StackExample {
    public static void main(String[] args) {
        Stack<Integer> stack = new Stack<>();
        
        // Pushing elements onto the stack
        stack.push(10);
        stack.push(20);
        stack.push(30);
        
        // Peeking the top element
        System.out.println("Top element: " + stack.peek());
        
        // Popping elements from the stack
        System.out.println("Popped element: " + stack.pop());
        System.out.println("Popped element: " + stack.pop());
        
        // Checking if the stack is empty
        System.out.println("Is stack empty? " + stack.empty());
        
        // Remaining elements in the stack
        System.out.println("Remaining elements: " + stack);
    }
}
```

# Interfaces Implemented

The `Stack` class indirectly implements several interfaces through the classes it extends. Here is a breakdown:

- **Collection<E>**: The `Stack` class implements the `Collection` interface via `AbstractCollection`.
- **List<E>**: The `Stack` class implements the `List` interface via `AbstractList`.
- **Iterable<E>**: The `Stack` class implements the `Iterable` interface via `AbstractCollection`.
- **RandomAccess**: The `Stack` class implements the `RandomAccess` interface via `Vector`.
- **Cloneable**: The `Stack` class implements the `Cloneable` interface via `Vector`.
- **Serializable**: The `Stack` class implements the `Serializable` interface via `Vector`.

# Classes Extended

- **java.util.Vector<E>**: The `Stack` class directly extends the `Vector` class, which is a growable array of objects.

# Summary

- **Stack Class**: Part of the `java.util` package, follows the LIFO principle.
- **Hierarchy**: Extends `Vector`, which in turn extends several other classes and implements multiple interfaces.
- **Key Methods**: `push`, `pop`, `peek`, `empty`, and `search`.
- **Interfaces Implemented**: `Collection`, `List`, `Iterable`, `RandomAccess`, `Cloneable`, and `Serializable`.

While the `Stack` class is a straightforward and easy-to-use implementation of a stack, it's worth noting that it extends `Vector`, which is synchronized and thus not as performant as other alternatives for certain use cases. For more modern stack implementations, developers often use `Deque` interface implementations like `ArrayDeque`.

