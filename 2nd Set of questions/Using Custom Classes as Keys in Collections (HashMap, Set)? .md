## Using Custom Classes as Keys in Collections (HashMap, Set)?

## Using Custom Class as Key in HashMap or HashSet

To use a custom class as a key in a `HashMap` or `HashSet`, you must override the `hashCode()` and `equals()` methods in your custom class.

### Methods to Override:

- **hashCode():** Used to calculate the bucket in which the entry will be placed.
- **equals():** Used to check whether two keys are identical.

### Example:

```java
class Person {
    private String name;
    private int age;

    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Person person = (Person) o;
        return age == person.age && Objects.equals(name, person.name);
    }
}
```
