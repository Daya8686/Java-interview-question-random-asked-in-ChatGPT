# Type Safety in Programming

Type safety in programming ensures that a program operates on data of the expected type, preventing type errors (such as treating an integer as a string). In Java, type safety helps to avoid runtime errors by catching type mismatches at compile time.

## Type Safety in Java
Java provides type safety primarily through:

- **Strong Typing**: Variables must be declared with a specific type, and only values of that type can be assigned to the variable.
- **Generics**: Introduced in Java 5, generics allow for type-safe operations on collections and other data structures without the need for casting.

## Benefits of Type Safety
- **Compile-Time Checking**: Errors are caught at compile time rather than at runtime, reducing the chances of runtime exceptions.
- **Code Clarity**: Explicit type declarations make the code more readable and maintainable.
- **Enhanced Reliability**: Reduces the risk of type-related bugs.

## Using Type Safety with Generics
Generics enhance type safety by allowing you to define classes, interfaces, and methods with type parameters. This eliminates the need for explicit casting and catches invalid types at compile time.

### Example of Type Safety without Generics
Before generics, collections operated on `Object` types, requiring casting and leading to potential runtime errors.

```java
import java.util.ArrayList;
import java.util.List;

public class NonGenericExample {
    public static void main(String[] args) {
        List list = new ArrayList();
        list.add("Hello");
        list.add(123); // No compile-time error, but it introduces type safety issues

        for (Object obj : list) {
            String str = (String) obj; // ClassCastException at runtime for the integer
            System.out.println(str);
        }
    }
}
```

### Example of Type Safety with Generics
#### Generics enforce type safety by specifying the type of elements that a collection can contain.

```java

import java.util.ArrayList;
import java.util.List;

public class GenericExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Hello");
        // list.add(123); // Compile-time error, preventing type safety issues

        for (String str : list) {
            System.out.println(str); // No casting needed, and no risk of ClassCastException
        }
    }
}

```

## Defining Generic Classes and Methods
#### You can define your own generic classes and methods to provide type safety in your code.

## Generic Class
```java

public class Box<T> {
    private T content;

    public void setContent(T content) {
        this.content = content;
    }

    public T getContent() {
        return content;
    }

    public static void main(String[] args) {
        Box<String> stringBox = new Box<>();
        stringBox.setContent("Type Safe");
        System.out.println(stringBox.getContent());

        Box<Integer> integerBox = new Box<>();
        integerBox.setContent(123);
        System.out.println(integerBox.getContent());
    }
}
```
## Generic Method
```java

public class GenericMethodExample {

    public static <T> void printArray(T[] array) {
        for (T element : array) {
            System.out.println(element);
        }
    }

    public static void main(String[] args) {
        String[] stringArray = {"Hello", "World"};
        Integer[] intArray = {1, 2, 3, 4};

        printArray(stringArray); // Type Safe
        printArray(intArray); // Type Safe
    }
}
```
## Conclusion
Type safety in Java helps to catch errors at compile time, reducing runtime exceptions and improving code reliability. Using generics is a key method for achieving type safety, especially when working with collections and other parameterized types. By defining types explicitly and leveraging generics, you can write cleaner, more maintainable, and safer code.
