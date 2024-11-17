# 2. How to sort a hashmap?

# Sorting a HashMap

Sorting a HashMap directly isn't possible because HashMap does not maintain any order of its keys or values. However, you can sort the entries of a HashMap by converting it to a different data structure that maintains order, such as a List. You can then sort this list based on the keys or values and, if needed, store the sorted entries in a LinkedHashMap to maintain the order.

## Sorting a HashMap by Keys
Here's how you can sort a HashMap by its keys:

```java
import java.util.*;

public class SortHashMapByKey {
    public static void main(String[] args) {
        // Creating a HashMap
        HashMap<String, Integer> map = new HashMap<>();
        map.put("apple", 10);
        map.put("orange", 5);
        map.put("banana", 20);
        map.put("grape", 15);

        // Converting HashMap to a List of Map.Entry
        List<Map.Entry<String, Integer>> list = new ArrayList<>(map.entrySet());

        // Sorting the list by keys
        list.sort(Map.Entry.comparingByKey());

        // Maintaining the order in a LinkedHashMap
        LinkedHashMap<String, Integer> sortedMap = new LinkedHashMap<>();
        for (Map.Entry<String, Integer> entry : list) {
            sortedMap.put(entry.getKey(), entry.getValue());
        }

        // Printing the sorted HashMap
        for (Map.Entry<String, Integer> entry : sortedMap.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
    }
}
```
# Sorting a HashMap by Values

Sorting a HashMap by values is not directly supported because HashMap does not maintain any order. However, you can sort the entries by converting the HashMap to a different data structure like a List that maintains order. Then, sort the list based on the values and store the sorted entries in a LinkedHashMap to maintain the order.

## Sorting a HashMap by Values

Here's how you can sort a HashMap by its values:

```java
import java.util.*;

public class SortHashMapByValue {
    public static void main(String[] args) {
        // Creating a HashMap
        HashMap<String, Integer> map = new HashMap<>();
        map.put("apple", 10);
        map.put("orange", 5);
        map.put("banana", 20);
        map.put("grape", 15);

        // Converting HashMap to a List of Map.Entry
        List<Map.Entry<String, Integer>> list = new ArrayList<>(map.entrySet());

        // Sorting the list by values
        list.sort(Map.Entry.comparingByValue());

        // Maintaining the order in a LinkedHashMap
        LinkedHashMap<String, Integer> sortedMap = new LinkedHashMap<>();
        for (Map.Entry<String, Integer> entry : list) {
            sortedMap.put(entry.getKey(), entry.getValue());
        }

        // Printing the sorted HashMap
        for (Map.Entry<String, Integer> entry : sortedMap.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
    }
}
```
## Explanation

### 1. Convert HashMap to List of Map.Entry:
* `List<Map.Entry<K, V>> list = new ArrayList<>(map.entrySet());`
### 2. Sort the List:

* `By Keys: list.sort(Map.Entry.comparingByKey());
By Values: list.sort(Map.Entry.comparingByValue());`
### 3. Store in `LinkedHashMap`:

* To maintain the order of sorted entries:
  
```java
LinkedHashMap<K, V> sortedMap = new LinkedHashMap<>();
for (Map.Entry<K, V> entry : list) {
    sortedMap.put(entry.getKey(), entry.getValue());
}

```


