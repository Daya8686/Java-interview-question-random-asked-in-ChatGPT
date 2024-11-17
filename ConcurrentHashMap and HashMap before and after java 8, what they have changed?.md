# Changes in HashMap and ConcurrentHashMap in Java 8

In Java, both `HashMap` and `ConcurrentHashMap` have undergone significant changes in Java 8 to improve performance, scalability, and efficiency. Let's explore these changes in detail:

## HashMap

### Before Java 8:
- **Data Structure**: `HashMap` used an array of linked lists to store the entries. This structure could lead to performance issues when many keys hash to the same bucket (i.e., in cases of high hash collisions).
- **Performance**: In the worst case, the time complexity for `get` and `put` operations could degrade to O(n) due to long linked lists.

### After Java 8:
- **Data Structure**: Java 8 introduced an improvement to the internal structure of `HashMap` to handle high collision scenarios. When the number of items in a bucket exceeds a certain threshold (default is 8), the linked list is transformed into a balanced binary tree (a red-black tree).
- **Performance**: This change improves the worst-case time complexity for `get` and `put` operations from O(n) to O(log n) for buckets with many entries. Once the number of entries falls below a certain threshold (6 by default), the bucket is converted back to a linked list.

#### Result of this change:
The overall performance and scalability of `HashMap` improved in collision-heavy scenarios due to the logarithmic search time provided by the red-black tree structure.

## ConcurrentHashMap

### Before Java 8:
- **Segmented Locking**: `ConcurrentHashMap` used a segmented locking mechanism to ensure thread safety. It divided the map into several segments, each functioning as an independent map with a lock.
- **Performance**: Each segment was locked independently, allowing multiple threads to access different segments concurrently without much contention. However, this structure added complexity and increased memory overhead.

### Changes in Java 8:
- **Lock-free Reads and Fine-Grained Locking**: Java 8 introduced a more efficient CAS (Compare-And-Swap) mechanism for reads, removing the need for locking on read operations. This greatly improved performance by making read operations lock-free.
- **Bucket-level Locking**: Instead of segment-based locking, Java 8 adopted a bucket-level locking system. This means that only individual buckets are locked during modifications, allowing for better concurrency compared to the segment-based approach.
- **Tree-based Buckets**: Like `HashMap`, `ConcurrentHashMap` also adopted tree-based buckets to handle collisions more efficiently. When the number of elements in a bucket grows beyond a certain threshold, the linked list is converted into a balanced tree, optimizing the performance of operations in high-collision scenarios.

#### Result of this change:
Java 8's `ConcurrentHashMap` became faster and more scalable, especially in highly concurrent environments, with improved lock-free reads and reduced contention due to finer-grained locking mechanisms.

## Key Takeaways:
- **HashMap** in Java 8 introduced tree-based buckets to handle collisions better, improving the worst-case time complexity from O(n) to O(log n).
- **ConcurrentHashMap** in Java 8 eliminated segment-based locking in favor of bucket-level locking and introduced CAS operations for lock-free reads, improving both read and write performance in concurrent environments.
