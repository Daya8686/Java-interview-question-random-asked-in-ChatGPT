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
