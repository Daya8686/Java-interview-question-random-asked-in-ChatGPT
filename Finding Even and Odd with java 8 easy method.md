# Finding Even and Odd with java 8 easy method

```java
import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

public class PartitioningByExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        // Partition numbers into even and odd
        Map<Boolean, List<Integer>> partitionedNumbers = numbers.stream()
                                                               .collect(Collectors.partitioningBy(num -> num % 2 == 0));

        // Print the partitioned numbers
        partitionedNumbers.forEach((isEven, numList) -> 
            System.out.println((isEven ? "Even" : "Odd") + " numbers: " + numList)
        );
    }
}

```
