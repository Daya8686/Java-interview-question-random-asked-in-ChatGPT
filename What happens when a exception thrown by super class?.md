# What happens when a exception thrown by super class?

# Exception Handling in Inheritance

When an exception is thrown by a method in a superclass, it can propagate through the call stack, potentially being caught and handled by a method in the subclass or by any other method in the call chain, depending on how the exception is declared and handled.

## Key Points to Consider:

### Checked vs. Unchecked Exceptions:
- **Checked Exceptions**: These must be either caught or declared in the method signature using `throws`.
- **Unchecked Exceptions**: These are subclasses of `RuntimeException` and `Error`, and they do not need to be declared or caught explicitly.

### Overriding Methods and Exceptions:
If a subclass overrides a method that throws a checked exception, the overriding method in the subclass can:
- Throw the same checked exception.
- Throw a subclass of that checked exception.
- Not throw any checked exception at all.
- The overriding method cannot throw a new or broader checked exception that is not declared in the superclass method.

## Example 1: Checked Exception Thrown by Superclass Method
```java
import java.io.IOException;

class SuperClass {
    void doSomething() throws IOException {
        // Simulating an exception
        throw new IOException("IOException in SuperClass");
    }
}

class SubClass extends SuperClass {
    @Override
    void doSomething() throws IOException {
        super.doSomething(); // Calls the superclass method
    }
}

public class ExceptionExample {
    public static void main(String[] args) {
        SuperClass obj = new SubClass();
        try {
            obj.doSomething();
        } catch (IOException e) {
            System.out.println("Caught exception: " + e.getMessage());
        }
    }
}
```

## Explanation:
- The `doSomething()` method in the superclass `SuperClass` declares that it throws an `IOException`.
- The `SubClass` overrides this method and calls `super.doSomething()`, which can throw an `IOException`.
- The `main()` method catches this exception in the try-catch block.

## Example 2: Unchecked Exception Thrown by Superclass Method

### Code:
```java
class SuperClass {
    void doSomething() {
        // Simulating an exception
        throw new NullPointerException("NullPointerException in SuperClass");
    }
}

class SubClass extends SuperClass {
    @Override
    void doSomething() {
        super.doSomething(); // Calls the superclass method
    }
}

public class ExceptionExample {
    public static void main(String[] args) {
        SuperClass obj = new SubClass();
        try {
            obj.doSomething();
        } catch (NullPointerException e) {
            System.out.println("Caught exception: " + e.getMessage());
        }
    }
}
```
# Explanation:
- The `doSomething()` method in the superclass throws a `NullPointerException`, which is an unchecked exception.
- The subclass `SubClass` overrides this method and calls `super.doSomething()`.
- The `main()` method catches the `NullPointerException`.

## Key Scenarios:

### Exception Propagation:
- If the exception is not caught within the subclass method, it will propagate up the call stack to the method that invoked the subclass method.
- The exception can be caught and handled at any level in the call stack.

### Overriding Method Restrictions:
- The overriding method cannot declare a broader checked exception than the one declared in the superclass method. If the superclass method does not declare a checked exception, the subclass method cannot declare any checked exception.
- However, the overriding method can throw unchecked exceptions without restrictions.

## Summary:
- When a superclass method throws an exception, it can be caught and handled by any method in the call stack, including methods in the subclass.
- For checked exceptions, the overriding method in the subclass must follow certain rules regarding which exceptions it can declare.
- Unchecked exceptions have more flexibility and do not require explicit declaration or handling.
