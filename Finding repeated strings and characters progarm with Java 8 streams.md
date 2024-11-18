# Finding repeated String and characters with Java 8 streams.

## Strings
### This is the easy way to get repeated elements and there count 
---
```java
import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

public class GroupingByExample {
    public static void main(String[] args) {
        List<String> items = Arrays.asList("apple", "banana", "orange", "apple", "banana", "banana");

        Map<String, Long> itemCounts = items.stream()
                                            .collect(Collectors.groupingBy(item -> item, Collectors.counting()));

        itemCounts.forEach((key, value) -> System.out.println(key + ": " + value));
    }
}

```

## Characters

```Java
import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

public class GroupingByExample {
    public static void main(String[] args) {
        String str = "Daya Sagar";

        // Convert char array to List<Character>
        List<Character> items = str.chars()
                                   .mapToObj(c -> (char) c)
                                   .collect(Collectors.toList());

        Map<Character, Long> itemCounts = items.stream()
                                               .collect(Collectors.groupingBy(item -> item, Collectors.counting()));

        itemCounts.forEach((key, value) -> System.out.println(key + ": " + value));
    }
}

```
### This is lengthy process of same (Characters)

```java
import java.util.HashMap;
import java.util.Map;

public class GroupingByExample {
    public static void main(String[] args) {
        String str = "Daya Sagar";
        Map<Character, Integer> frequencyCount = new HashMap<>();

        for (int i = 0; i < str.length(); i++) {
            char c = str.charAt(i);
            if (frequencyCount.containsKey(c)) {
                frequencyCount.put(c, frequencyCount.get(c) + 1);
            } else {
                frequencyCount.put(c, 1);
            }
        }

        System.out.println(frequencyCount);
    }
}

```
