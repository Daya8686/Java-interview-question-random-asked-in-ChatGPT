# Does Comparative and comparable are the function interfaces ?

# Comparable and Comparator Interfaces in Java

In Java, the `Comparable` and `Comparator` interfaces are used for sorting objects. Both interfaces provide ways to compare objects, but they have different use cases and approaches. Let's explore the differences between them, along with how they relate to functional interfaces.

## 1. Comparable Interface

### Purpose:
The `Comparable` interface is used to define the natural ordering of objects of a class. It is typically implemented by the class whose objects are to be ordered.

### Method:
The `Comparable` interface has a single method:
```java
int compareTo(T o);
```

This method compares the current object with the specified object `o` and returns:

- A negative integer if the current object is less than `o`.
- Zero if the current object is equal to `o`.
- A positive integer if the current object is greater than `o`.

### Implementation:
When a class implements `Comparable`, it must override the `compareTo` method to provide a default comparison logic.

### Example:
```java
public class Employee implements Comparable<Employee> {
    private int id;
    private String name;

    public Employee(int id, String name) {
        this.id = id;
        this.name = name;
    }

    @Override
    public int compareTo(Employee other) {
        return this.id - other.id; // Natural ordering by id
    }

    // Getters and toString() omitted for brevity
}
```
- **Use Case:** Use Comparable when you want to define a default sorting order for objects, such as sorting by an ID or name.

## Comparator Interface

### Purpose:
The `Comparator` interface is used to define a custom order for objects that is different from the natural ordering. It is typically used when you need multiple sorting criteria or when you cannot modify the class to implement `Comparable`.

### Method:
The `Comparator` interface has a single method:
```java
int compare(T o1, T o2);
```

This method compares two objects `o1` and `o2` and returns:

- A negative integer if `o1` is less than `o2`.
- Zero if `o1` is equal to `o2`.
- A positive integer if `o1` is greater than `o2`.

### Implementation:
You can implement `Comparator` in a separate class or as a lambda expression.

### Example:
```java
public class EmployeeNameComparator implements Comparator<Employee> {
    @Override
    public int compare(Employee e1, Employee e2) {
        return e1.getName().compareTo(e2.getName()); // Custom ordering by name
    }
}

// Using Comparator with a lambda expression
Comparator<Employee> byName = (e1, e2) -> e1.getName().compareTo(e2.getName());
```

### Use Case:
Use `Comparator` when you need multiple or custom sorting orders, or when you cannot modify the original class to implement `Comparable`.

## 3. Functional Interface

### Comparable as a Functional Interface:
The `Comparable` interface is not considered a functional interface because it is designed to be implemented by the class itself rather than used as a lambda expression. However, it still has only one abstract method.

### Comparator as a Functional Interface:
The `Comparator` interface is a functional interface because it has a single abstract method (`compare`). This allows it to be used with lambda expressions or method references.

```java
Comparator<Employee> byId = (e1, e2) -> Integer.compare(e1.getId(), e2.getId());
```

# Summary of Differences:

## Comparable:
- **Purpose**: Defines natural ordering of objects.
- **Implemented By**: The class itself.
- **Method**: `compareTo(T o)`.
- **Use Case**: When there is a single natural order for a class.

## Comparator:
- **Purpose**: Defines custom ordering of objects.
- **Implemented By**: A separate class, lambda, or method reference.
- **Method**: `compare(T o1, T o2)`.
- **Use Case**: When multiple or alternative sorting orders are needed.

## Example Usage Together:
You can use both `Comparable` and `Comparator` together. For example, an `Employee` class may implement `Comparable` to define a natural order by id, but you can use `Comparator` to sort by name or another attribute when needed.

```java
Collections.sort(employeeList); // Uses Comparable (natural order by id)
Collections.sort(employeeList, new EmployeeNameComparator()); // Uses Comparator (custom order by name)
```
