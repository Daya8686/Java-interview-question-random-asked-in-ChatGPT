# How clone in java works? and what is shallow copy and deep copy??

# Cloning in Java

In Java, cloning is a process of creating a copy of an object. The `Object` class in Java provides a `clone()` method that allows you to create a copy of an object. However, the behavior of cloning depends on whether the object implements the `Cloneable` interface or not.

## 1. Cloning in Java
Cloning in Java can be done by calling the `clone()` method on an object. By default, the `clone()` method performs a shallow copy, meaning it copies the values of the fields of the object. If you want to enable cloning, the class must implement the `Cloneable` interface. Otherwise, calling `clone()` will throw a `CloneNotSupportedException`.

### Example:
```java
class Person implements Cloneable {
    String name;
    int age;

    // Constructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Override clone() method
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone(); // Calls Object's clone method
    }
}

public class Main {
    public static void main(String[] args) throws CloneNotSupportedException {
        Person p1 = new Person("Alice", 25);
        Person p2 = (Person) p1.clone(); // Clone the object

        System.out.println(p1 == p2); // false, different memory locations
        System.out.println(p1.name + " - " + p1.age);
        System.out.println(p2.name + " - " + p2.age);
    }
}

```

In this example:

`p1.clone()` creates a shallow copy of `p1`, so `p2` is a new object with the same values for `name` and `age` as `p1`, but they are distinct objects in memory.

## 2. Shallow Copy vs. Deep Copy

### Shallow Copy:
In a shallow copy, the object is copied as-is, but if the object contains references to other objects (such as arrays or other class instances), only the references (not the referenced objects themselves) are copied. As a result, both the original object and the cloned object share references to the same objects.

For example, if an object has a reference to an array or another object, the shallow copy will copy the reference, not the actual data.

### Deep Copy:
In a deep copy, all the objects are recursively copied, meaning not only the original object but also all objects it refers to are cloned as well. In other words, a deep copy creates a new object for each referenced object, ensuring that the original and the cloned object are completely independent.

### Shallow Copy Example:
```java
class Person implements Cloneable {
    String name;
    int[] scores;

    // Constructor
    public Person(String name, int[] scores) {
        this.name = name;
        this.scores = scores;
    }

    // Override clone() for shallow copy
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone(); // Performs shallow copy
    }
}

public class Main {
    public static void main(String[] args) throws CloneNotSupportedException {
        int[] scores = {100, 90, 85};
        Person p1 = new Person("Alice", scores);
        Person p2 = (Person) p1.clone(); // Shallow copy

        // Modifying p2's scores array
        p2.scores[0] = 50;

        // Both p1 and p2 share the same scores array reference
        System.out.println(p1.scores[0]); // 50 (since both p1 and p2 refer to the same array)
    }
}
```


# Key Differences Between Shallow and Deep Copy

| **Aspect**      | **Shallow Copy**                                           | **Deep Copy**                                          |
|-----------------|------------------------------------------------------------|--------------------------------------------------------|
| **References**  | Copies the references to objects (not the objects themselves) | Copies the objects themselves recursively              |
| **Nested Objects** | Nested objects are shared between the original and the clone | Nested objects are fully copied                        |
| **Performance** | Faster, as it only copies references                       | Slower, as it involves copying all nested objects      |
| **Use Case**    | Suitable when you don't need independent copies of the referenced objects | Suitable when you need completely independent copies of all objects |


