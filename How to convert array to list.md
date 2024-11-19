# How to convert array to list?

### In Java, you can convert an array to a list using various methods. Here are some of the most common ways:

## 1. Using Arrays.asList()
The `Arrays.asList()` method provides a fixed-size list backed by the specified array. Note that the list is backed by the array, so changes to the array will be reflected in the list and vice versa.

```java

import java.util.Arrays;
import java.util.List;

public class ArrayToListExample {
    public static void main(String[] args) {
        String[] array = {"A", "B", "C"};
        List<String> list = Arrays.asList(array);

        System.out.println(list); // Output: [A, B, C]
    }
}
```
## 2. Using ArrayList Constructor
### To get a modifiable list, you can pass the result of Arrays.asList() to a new ArrayList.

```java

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class ArrayToListExample {
    public static void main(String[] args) {
        String[] array = {"A", "B", "C"};
        List<String> list = new ArrayList<>(Arrays.asList(array));

        list.add("D"); // Modifiable list
        System.out.println(list); // Output: [A, B, C, D]
    }
}
```
## 3. Using Collections.addAll()
### The Collections.addAll() method adds all elements from an array to a list.

```java

import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class ArrayToListExample {
    public static void main(String[] args) {
        String[] array = {"A", "B", "C"};
        List<String> list = new ArrayList<>();
        Collections.addAll(list, array);

        list.add("D"); // Modifiable list
        System.out.println(list); // Output: [A, B, C, D]
    }
}
```
## 4. Using Java 8 Streams
### Java 8 Streams provide a modern way to convert an array to a list.

```java

import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class ArrayToListExample {
    public static void main(String[] args) {
        String[] array = {"A", "B", "C"};
        List<String> list = Arrays.stream(array)
                                  .collect(Collectors.toList());

        list.add("D"); // Modifiable list
        System.out.println(list); // Output: [A, B, C, D]
    }
}
```
## 5. Using a Loop
### You can manually add elements from the array to a list using a loop.

```java

import java.util.ArrayList;
import java.util.List;

public class ArrayToListExample {
    public static void main(String[] args) {
        String[] array = {"A", "B", "C"};
        List<String> list = new ArrayList<>();

        for (String element : array) {
            list.add(element);
        }

        list.add("D"); // Modifiable list
        System.out.println(list); // Output: [A, B, C, D]
    }
}
```

## Summary

- **`Arrays.asList()`**: Creates a fixed-size list backed by the array.
- **ArrayList Constructor**: Creates a modifiable list.
- **`Collections.addAll()`**: Adds all elements to a modifiable list.
- **Java 8 Streams**: Modern and concise way to convert an array to a list.
- **Loop**: Manual way to add elements to a list.

Choose the method that best fits your specific requirements. For most use cases, using `Arrays.asList()` followed by `new ArrayList<>()` is a common and straightforward approach.
