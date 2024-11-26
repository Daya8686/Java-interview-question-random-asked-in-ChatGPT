# Java Streams API Operations

In Java Streams API, operations are divided into two types: intermediate operations and terminal operations.

## 1. Intermediate Operations
These operations return a new stream and are lazy. They do not perform the actual processing until a terminal operation is invoked. Intermediate operations are chainable.

| Operator              | Description                                                                         |
|-----------------------|-------------------------------------------------------------------------------------|
| `filter(Predicate)`   | Filters elements based on the given predicate.                                       |
| `map(Function)`       | Transforms elements using the provided function (e.g., object to another object).    |
| `flatMap(Function)`   | Similar to map, but flattens the results (used for streams of streams).              |
| `distinct()`          | Removes duplicate elements from the stream.                                          |
| `sorted()`            | Sorts elements in natural order or with a custom comparator.                         |
| `sorted(Comparator)`  | Sorts elements using a custom comparator.                                            |
| `limit(long n)`       | Limits the number of elements in the stream to the given number.                     |
| `skip(long n)`        | Skips the first n elements in the stream.                                            |
| `peek(Consumer)`      | Allows performing an action on each element as it is processed, primarily for debugging. |
| `takeWhile(Predicate)`| Takes elements from the stream while the given condition is true, introduced in Java 9.|
| `dropWhile(Predicate)`| Drops elements from the stream while the given condition is true, introduced in Java 9.|

**Example**:
```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");
names.stream()
     .filter(name -> name.length() > 3)  // Intermediate operation
     .map(String::toUpperCase)           // Intermediate operation
     .forEach(System.out::println);      // Terminal operation
```

## 2. Terminal Operations
These operations trigger the processing of the stream and return either a result or a side effect. They are eager, which means once a terminal operation is invoked, the stream is consumed and cannot be used again.

| Operator                | Description                                                                   |
|-------------------------|-------------------------------------------------------------------------------|
| `forEach(Consumer)`     | Performs the given action for each element in the stream.                     |
| `forEachOrdered(Consumer)` | Like forEach, but respects the encounter order if the stream has one.      |
| `toArray()`             | Converts the stream into an array.                                            |
| `reduce(BinaryOperator)`| Combines elements in the stream using the provided function, returning an Optional.|
| `reduce(identity, BinaryOperator)` | Combines elements with an initial identity value, returning a result.|
| `collect(Collector)`    | Converts the elements of the stream into a collection, like a List or Set.    |
| `min(Comparator)`       | Returns the minimum element based on the provided comparator, wrapped in an Optional.|
| `max(Comparator)`       | Returns the maximum element based on the provided comparator, wrapped in an Optional.|
| `count()`               | Returns the count of elements in the stream.                                  |
| `anyMatch(Predicate)`   | Returns true if any element matches the given predicate.                      |
| `allMatch(Predicate)`   | Returns true if all elements match the given predicate.                       |
| `noneMatch(Predicate)`  | Returns true if no elements match the given predicate.                        |
| `findFirst()`           | Returns the first element of the stream wrapped in an Optional.               |
| `findAny()`             | Returns any element of the stream wrapped in an Optional.                     |
| `iterator()`            | Converts the stream into an iterator.                                         |
| `spliterator()`         | Returns a Spliterator over the elements in the stream.                        |

**Example**:
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
long count = numbers.stream()
                    .filter(num -> num % 2 == 0)  // Intermediate operation
                    .count();                    // Terminal operation
System.out.println(count);  // Output: 3
```
## Differences Between Intermediate and Terminal Operations

- **Intermediate Operations** are lazy and don't perform processing until a terminal operation is invoked. They return a new stream.
- **Terminal Operations** are eager and trigger the processing of the pipeline. They return a concrete result (e.g., `List`, `Optional`, `boolean`, etc.) or produce a side effect (e.g., printing via `forEach`). After a terminal operation is called, the stream is consumed and cannot be used further.
