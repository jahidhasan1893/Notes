### 1. **What is the difference between primitive types and reference types?**

**solution:** 

 [Java Objects vs References Explained Simply — A Beginner's Guide to Java Memory Management](https://freedium.cfd/https://blog.stackademic.com/java-objects-vs-references-explained-simply-a-beginners-guide-to-java-memory-management-0e4369618d34?__cf_chl_tk=371StRPox2czBRCT4F.Q6udSGnZHCWarNA0Ymjf3RUA-1753875805-1.0.1.1-ld3KXSyf9WILNoRUUuA4d4n0LO5hKwMWCoLGP2NaPLw)

---

### 2.  **What is the difference between parallelism and concurrency in java?**

 **solution:**

 [Java: Parallelism and concurrency a complete guide](https://pedrosilvatech.medium.com/java-parallelism-and-concurrency-a-complete-guide-d426957538aa)

---

### 3. **What is ExecutorService in java?**

 **solution:**

 [Java: Parallelism and concurrency a complete guide](https://pedrosilvatech.medium.com/java-parallelism-and-concurrency-a-complete-guide-d426957538aa)


---

### 4. **What's the difference between `synchronized` and `Lock` in Java?**

 **solution:**

In Java, `synchronized` and explicit `Lock` implementations (like `ReentrantLock` from `java.util.concurrent.locks`) are both mechanisms for achieving thread synchronization and ensuring mutual exclusion for shared resources.


**Synchronized**
* **Purpose**: Provides mutual exclusion — ensures only one thread can access the synchronized code at a time.
* **Usage**: Can be applied to methods or code blocks.
* **Behavior**:
  * Automatically acquires and releases locks
  * Implicit Locking
  * JVM handles the locking mechanism
  * Blocking — threads wait until the lock is available
  * Cannot be interrupted while waiting
  * Always releases locks even if exceptions occur <br /><br />

```java
synchronized void method() {
    // thread-safe code
}

synchronized (object) {
    // thread-safe code
}
```


 **Lock (`java.util.concurrent.locks`)**

* **Purpose**: Explicit, more flexible locking mechanism
* **Implementation**: Interface with various implementations (`ReentrantLock`, `ReadWriteLock`, etc.)
* **Advantages over `synchronized`**:
  * **Interruptible lock attempts** via `lockInterruptibly()`
  * Ability to try acquiring lock without blocking (`tryLock()`)
  * Non-block-structured locking (can acquire in one method, release in another)
  * Read/write locks for better concurrency
  * Fair/unfair lock ordering policies
  * Performance monitoring via lock condition stats <br /><br />

```java
Lock lock = new ReentrantLock();
try {
lock.lock(); // or lock.tryLock(), or lock.lockInterruptibly()
// thread-safe code
} finally {
lock.unlock(); // must explicitly release!
}
```

**When to Use Each**

* **`synchronized`**:
  Use for simple use cases when automatic lock release is preferred.

* **`Lock`**:
  Use for complex scenarios requiring:
  * Timed waits
  * Interruptibility
  * Fairness control

`Lock` provides more fine-grained control and flexibility at the cost of increased complexity, while `synchronized` is simpler but less flexible.

---

### 5. ** How to Implement a Thread Safe Singeleton? **

**solution:**

[How to Implement a Thread-Safe Singleton in Java?](https://www.baeldung.com/java-implement-thread-safe-singleton?ref=dailydev)

---
