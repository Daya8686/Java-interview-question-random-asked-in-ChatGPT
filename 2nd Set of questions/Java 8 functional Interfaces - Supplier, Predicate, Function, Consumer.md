# Java 8 Functional Interfaces

In Java 8, functional interfaces are interfaces with a single abstract method (SAM). They can be implemented using lambda expressions, method references, or anonymous classes. Some commonly used functional interfaces include `Predicate`, `Function`, `Consumer`, and `Supplier`.

## 1. Predicate
- **Description**: Represents a boolean-valued function of one argument.
- **Method**: `boolean test(T t)`
- **Usage**: Typically used for filtering or matching conditions.

Example:
```java
Predicate<Integer> isEven = num -> num % 2 == 0;
System.out.println(isEven.test(4));  // Output: true

```



## 2. Function
- **Description**: Represents a function that accepts one argument and produces a result.
- **Method**: `R apply(T t)`
- **Usage**: Used for transforming an object from one type to another.

Example:
```java
Function<String, Integer> stringLength = str -> str.length();
System.out.println(stringLength.apply("Hello"));  // Output: 5

```


## 3. Consumer
- **Description**: Represents an operation that accepts a single input argument and returns no result.
- **Method**: `void accept(T t)`
- **Usage**: Typically used when you need to perform an action on an input without returning any result.

Example:
```java
Consumer<String> print = str -> System.out.println(str);
print.accept("Hello World!");  // Output: Hello World!

```

## 4. Supplier
- **Description**: Represents a supplier of results with no input.
- **Method**: `T get()`
- **Usage**: Used when you need to supply objects (like factories).

Example:
```java
Supplier<Double> randomValue = () -> Math.random();
System.out.println(randomValue.get());  // Output: A random number

```

These functional interfaces are part of the `java.util.function` package and are commonly used with streams and other functional programming constructs in Java. They allow writing concise, readable, and maintainable code using lambda expressions.
