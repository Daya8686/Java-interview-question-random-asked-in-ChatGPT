# How to sort each string in array of string using Java 8?

### Sort Strings with String array
```java
import java.util.Arrays;

public class SortStringsInArray {
    public static void main(String[] args) {
        String[] array = {"banana", "apple", "cherry"};
            List<String> sortedArray=Arrays.stream(array).sorted().collect(Collectors.toList());
            System.out.println(sortedArray);

//or
List<String> sortedArray=Arrays.stream(array).sorted().toArray(String[]::new);
System.out.println(Arrays.toString(sortedArray);

    }
}
```

### Sort Strings with characters also to sort and array also

```java
import java.util.Arrays;

public class SortStringsInArray {
    public static void main(String[] args) {
        String[] array = {"banana", "apple", "cherry"};
          String[] sortedArray=Arrays.stream(array).map(str->{
             char[] strChars= str.toCharArray();
                Arrays.sort(strChars);
                return new String (strChars);
              }).toArray(String[]::new);
            System.out.println(Arrays.toString(sortedArray));
        }
}

```
