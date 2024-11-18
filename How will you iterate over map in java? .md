# How will you iterate over map in java?

# Iterating Over a Map in Java

There are several ways to iterate over a Map in Java. Here are some of the most common methods:

## 1. Iterating Using `entrySet()`
This is the most efficient way to iterate over the entries of a Map. It provides access to both keys and values.

```java
import java.util.HashMap;
import java.util.Map;

public class MapIterationExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("One", 1);
        map.put("Two", 2);
        map.put("Three", 3);

        for (Map.Entry<String, Integer> entry : map.entrySet()) {
            System.out.println("Key: " + entry.getKey() + ", Value: " + entry.getValue());
        }
    }
}
```

## 2. Iterating Using `keySet()`
This method iterates over the keys, and you can get the corresponding value using `map.get(key)`. This method is less efficient than using `entrySet()` because it requires an additional lookup for each key.

```java
import java.util.HashMap;
import java.util.Map;

public class MapIterationExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("One", 1);
        map.put("Two", 2);
        map.put("Three", 3);

        for (String key : map.keySet()) {
            System.out.println("Key: " + key + ", Value: " + map.get(key));
        }
    }
}
```
## 3. Iterating Using `values()`
This method iterates over the values of the Map directly. It’s useful when you only need the values and not the keys.

```java
import java.util.HashMap;
import java.util.Map;

public class MapIterationExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("One", 1);
        map.put("Two", 2);
        map.put("Three", 3);

        for (Integer value : map.values()) {
            System.out.println("Value: " + value);
        }
    }
}

```

## 4. Iterating Using Java 8 `forEach` and Lambda
Java 8 introduced the `forEach` method that allows you to iterate over the Map using a lambda expression.

```java
import java.util.HashMap;
import java.util.Map;

public class MapIterationExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("One", 1);
        map.put("Two", 2);
        map.put("Three", 3);

        map.forEach((key, value) -> System.out.println("Key: " + key + ", Value: " + value));
    }
}
```

## 5. Iterating Using an Iterator
You can also use an `Iterator` to iterate over a Map. This method is particularly useful if you need to remove entries during iteration.

```java
import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;

public class MapIterationExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("One", 1);
        map.put("Two", 2);
        map.put("Three", 3);

        Iterator<Map.Entry<String, Integer>> iterator = map.entrySet().iterator();
        while (iterator.hasNext()) {
            Map.Entry<String, Integer> entry = iterator.next();
            System.out.println("Key: " + entry.getKey() + ", Value: " + entry.getValue());
            if (entry.getKey().equals("Two")) {
                iterator.remove(); // Remove entry with key "Two"
            }
        }

        System.out.println("Map after iteration: " + map);
    }
}
```

## Summary

- **`entrySet()`**: Best way to iterate over both keys and values.
- **`keySet()`**: Iterate over keys and fetch values using `get`.
- **`values()`**: Iterate over values directly.
- **Java 8 `forEach`**: Clean and concise way to iterate using lambda expressions.
- **`Iterator`**: Useful for removing entries during iteration.

Choose the method that best fits your use case. For most general purposes, `entrySet()` or `forEach` are recommended due to their simplicity and efficiency.
