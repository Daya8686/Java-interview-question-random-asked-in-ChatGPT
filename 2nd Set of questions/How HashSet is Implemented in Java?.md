## How HashSet is Implemented in Java?
## HashSet Implementation

`HashSet` is implemented using a `HashMap` internally. Each element in the `HashSet` is stored as a key in the `HashMap`, with the value being a constant dummy object (usually `PRESENT`).

### Uniqueness

- Ensured by the keys of the `HashMap`, which means duplicates are not allowed.

### Hashing

- Elements are hashed using their `hashCode()`, and stored in the appropriate bucket in the underlying `HashMap`.

### Example Implementation

```java
private transient HashMap<E, Object> map;
private static final Object PRESENT = new Object();

public boolean add(E e) {
    return map.put(e, PRESENT) == null;
}
```
