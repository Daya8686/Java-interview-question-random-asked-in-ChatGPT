# How to Find Unique Elements Inside an Array?

To find unique elements in an array using Java 8, you can convert the array to a Set, which inherently removes duplicates since sets do not allow duplicate elements.

Here's how you can do it:

### Method 1

```java

import java.util.Arrays;
import java.util.Set;
import java.util.stream.Collectors;

public class UniqueElementsInArray {
    public static void main(String[] args) {
        Integer[] array = {1, 2, 2, 3, 4, 4, 5};

        List<Integer> uniqueElements = Arrays.stream(array).sorted().distinct()
                .collect(Collectors.toList());

        System.out.println(uniqueElements);
    }
}

```


### Method 2
```java

import java.util.Arrays;
import java.util.Set;
import java.util.stream.Collectors;

public class UniqueElementsInArray {
    public static void main(String[] args) {
        Integer[] array = {1, 2, 2, 3, 4, 4, 5};

        Set<Integer> uniqueElements = Arrays.stream(array)
                .collect(Collectors.toSet());

        System.out.println(uniqueElements);
    }
}

```

### Method 3
If you need to preserve the order and remove duplicates, you can use a `LinkedHashSet`:

```java
Set<Integer> uniqueElements = Arrays.stream(array)
                                    .collect(Collectors.toCollection(LinkedHashSet::new));

```
