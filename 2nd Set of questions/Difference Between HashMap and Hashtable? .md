## Difference Between HashMap and Hashtable?

## HashMap vs. Hashtable

### HashMap

- **Non-synchronized:** Not thread-safe.
- **Null Handling:** Allows one null key and multiple null values.
- **Performance:** Better performance than `Hashtable` in single-threaded environments.
Example:
```Java
HashMap<String, String> map = new HashMap<>();

```


### Hashtable

- **Synchronized:** Thread-safe but slower.
- **Null Handling:** Does not allow null keys or null values.
- **Legacy:** Legacy class (part of Java 1.0) and rarely used in modern Java applications.
Example:
```Java
Hashtable<String, String> table = new Hashtable<>();

```
