##  Difference Between Vector and ArrayList?

## ArrayList vs. Vector

### ArrayList

- **Not synchronized:** Not thread-safe by default.
- **Performance:** Better performance in single-threaded environments.
- **Growth:** Grows dynamically by increasing its size by 50% when needed.
Example:
```Java
ArrayList<String> list = new ArrayList<>();

```

### Vector

- **Synchronized:** Thread-safe.
- **Performance:** Slower in performance due to synchronization.
- **Growth:** Grows dynamically by doubling its size when needed.
- **Legacy:** Legacy class, replaced by `ArrayList` in most cases.

Example:
```Java
Vector<String> vector = new Vector<>();

```
