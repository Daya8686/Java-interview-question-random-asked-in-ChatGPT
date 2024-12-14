## Difference Between Enumerator and Iterator?
## Enumerator

- **Legacy Interface:** It's a legacy interface (used in Java 1.0).
- **Methods:** `hasMoreElements()` and `nextElement()`.
- **Limitation:** Does not support the removal of elements during iteration.
- **Example Usage:** Used in older collections like `Vector` and `Stack`.

### Example:

```java
Enumeration<String> en = vector.elements();
```
## Iterator

- **Introduction:** Introduced in Java 2 as part of the Collection framework.
- **Methods:** `hasNext()`, `next()`, and `remove()`.
- **Advantage:** Allows safe removal of elements during iteration using `remove()`.
- **Usage:** It is more modern and used with most collections like `List`, `Set`, `Map`.

### Example:

```java
Iterator<String> it = list.iterator();
while(it.hasNext()) {
    it.next();
}
```
