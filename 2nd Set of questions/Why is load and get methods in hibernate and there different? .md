## load() and get() Methods in Hibernate

In Hibernate, both `load()` and `get()` methods are used to retrieve entities from the database, but they differ in their behavior and use cases.

### 1. load() Method

**Purpose:** `load()` is used when you expect the entity to exist in the database but don't need to immediately fetch it. It provides a proxy object that can later be populated with the actual data when required.

**Lazy Loading:** It returns a proxy without hitting the database immediately. The actual database query is triggered only when a method is called on the proxy object (like accessing a field).

**Exception Handling:** If the entity doesn't exist in the database, `load()` throws an `ObjectNotFoundException` at the point when the object is actually accessed (not when `load()` is called).

**Use Case:** Use `load()` when you are certain that the entity exists and don't need the data immediately.

Example:

```java
// Example of load()
Session session = sessionFactory.openSession();
MyEntity entity = session.load(MyEntity.class, 1); // Returns a proxy object
System.out.println(entity.getName()); // Triggers a database query
```

### get() Method

**Purpose:** `get()` is used when you want to immediately retrieve the entity from the database. It directly hits the database to fetch the entity.

**Eager Loading:** Unlike `load()`, `get()` immediately returns the actual object, not a proxy.

**Return Value:** If the entity does not exist, `get()` returns `null` without throwing an exception.

**Use Case:** Use `get()` when you want to immediately fetch the entity or when you're unsure if the entity exists.

Example:

```java
// Example of get()
Session session = sessionFactory.openSession();
MyEntity entity = session.get(MyEntity.class, 1); // Immediately queries the database
if (entity != null) {
    System.out.println(entity.getName());
} else {
    System.out.println("Entity not found");
}
```

## Key Differences

### Timing of Data Fetch

- **load():** Delays the database query until the object is actually accessed (lazy loading).
- **get():** Immediately fetches the entity from the database (eager loading).

### Return Value for Non-Existent Entities

- **load():** Throws `ObjectNotFoundException` when trying to access a non-existent entity.
- **get():** Returns `null` if the entity does not exist.

### Use Case

- **load():** Use when you're certain the entity exists and you want to benefit from lazy loading.
- **get():** Use when you need the entity immediately or aren't sure if it exists.
