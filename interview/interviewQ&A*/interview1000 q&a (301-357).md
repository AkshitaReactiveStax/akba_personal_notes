
## **✅ 301.** 

## **Which intrinsic lock is acquired by a synchronized method in Java?**

  

### **🔹 Non-static synchronized method:**

  

Locks on the **current instance (this)**.

```
synchronized void print() {
    // Lock is on 'this'
}
```

### **🔹 Static synchronized method:**

  

Locks on the **Class object**, i.e., MyClass.class.

```
synchronized static void log() {
    // Lock is on MyClass.class
}
```

> 🧠 This is called an **intrinsic lock** or **monitor lock**, managed implicitly by the JVM.

---

## **✅ 302.** 

## **Can we mark a constructor as synchronized in Java?**

  

**No**, constructors **cannot be synchronized** because:

- The object is not fully constructed.
    
- The this reference is not available to other threads yet.
    
- Locking requires an object to lock on (this), which isn’t fully available inside a constructor.
    

  

> 🔍 JVM restriction: synchronized is disallowed on constructors syntactically.

  

**✅ Instead:**

Use synchronized blocks inside constructors if needed:

```
public MyClass() {
    synchronized (MyClass.class) {
        // Safe shared resource setup
    }
}
```

---

## **✅ 303.** 

## **Can we use primitive values for intrinsic locks?**

  

**No**, intrinsic locks (used in synchronized) can only be used on **Objects**, not **primitive types** (int, boolean, etc.).

```
int i = 0;
// synchronized(i) ❌ Invalid — causes compile-time error
```

> ✅ You can use boxed objects like Integer, but be **very cautious**:

> Integer values from -128 to 127 are **interned and shared**, which can lead to unintended lock sharing.

```
Integer i = 127;
synchronized (i) {
    // Dangerous - could lock shared cache object
}
```

---

## **✅ 304.** 

## **Do we have re-entrant property in intrinsic locks?**

  

**Yes**, intrinsic locks in Java are **re-entrant**.

  

### **🔍 Reentrancy means:**

  

A thread that already holds the lock **can acquire it again** (even recursively), without getting blocked.

```
synchronized void outer() {
    inner(); // This is OK
}

synchronized void inner() {
    // Lock is re-acquired by same thread
}
```

> 🔥 Without reentrancy, this would cause a **self-deadlock**.

  

### **✅ Both** 

### **synchronized**

###  **and** 

### **ReentrantLock**

###  **support reentrancy.**

---

## **✅ 305.** 

## **What is an atomic operation?**

  

An **atomic operation** is one that is:

- **Indivisible**: Cannot be split by thread context switches.
    
- **Consistent**: Visible as a complete unit to other threads.
    
- **Uninterruptible**: Either fully happens or doesn’t happen at all.
    

  

### **✅ Examples:**

- int a = 10; (primitive assignment)
    
- volatile reads/writes for 32-bit types
    
- AtomicInteger.incrementAndGet()
    

---

## **✅ 306.** 

## **Can we consider the statement i++ as an atomic operation in Java?**

  

**No**, i++ is **not atomic**. It’s a compound operation:

```
// i++ is broken into:
int temp = i;
temp = temp + 1;
i = temp;
```

This creates a **race condition** when multiple threads execute i++ concurrently.

  

### **🔥 Interview Example:**

```
class Counter {
    int count = 0;
    public void increment() {
        count++; // ❌ Not thread-safe
    }
}
```

---

## **✅ 307.** 

## **What are the Atomic operations in Java?**

  

Java provides the **java.util.concurrent.atomic** package for true atomic operations.

  

### **✅ Key Classes:**

- AtomicInteger, AtomicLong, AtomicBoolean
    
- AtomicReference<T>
    
- LongAdder, DoubleAdder (for contention-heavy counters)
    

  

### **✅ Atomic Methods:**

```
AtomicInteger counter = new AtomicInteger(0);
counter.incrementAndGet(); // Thread-safe ++
counter.getAndSet(10);     // Atomic set
counter.compareAndSet(5, 10); // CAS
```

### **🔍 Under the hood:**

  

Uses **Compare-And-Swap (CAS)** at the hardware level for **lock-free, thread-safe** behavior.

---

## **✅ 308.** 

## **Can you check if the following code is thread-safe?**

```
class Counter {
    private int count = 0;

    public void increment() {
        count++;
    }

    public int getCount() {
        return count;
    }
}
```

### **❌ Answer: This is** 

### **not thread-safe**

### **.**

- count++ is not atomic.
    
- No synchronization or visibility guarantees.
    
- getCount() may return stale data without volatile or synchronization.
    

  

### **✅ Fixes:**

1. Use synchronized:
    

```
synchronized void increment() {
    count++;
}
```

2. Use AtomicInteger:
    

```
AtomicInteger count = new AtomicInteger();
public void increment() {
    count.incrementAndGet();
}
```

3. Use LongAdder for high-throughput counters.
    

---

## **✅ 309.** 

## **What are the minimum requirements for a Deadlock situation in a program?**

  

According to **Coffman’s Conditions**, all 4 must be true:

|**Condition**|**Meaning**|
|---|---|
|Mutual Exclusion|At least one lock is held exclusively|
|Hold and Wait|Threads hold resources while waiting for others|
|No Preemption|Resources can’t be forcefully taken away|
|Circular Wait|A cycle of threads, each waiting on another’s resource|

> 🔥 Even if 3 out of 4 are present, deadlock **cannot** occur.

---

## **✅ 310.** 

## **How can we prevent a Deadlock?**

  

### **🔑 Strategies to prevent deadlock:**

---

### **🔹 1.** 

### **Lock ordering**

  

Acquire multiple locks in a **global fixed order**.

```
synchronized (lock1) {
    synchronized (lock2) {
        // Safe
    }
}
```

---

### **🔹 2.** 

### **Try-Lock with timeout**

  

Use ReentrantLock.tryLock(timeout) to avoid waiting forever.

```
if (lock1.tryLock(100, TimeUnit.MILLISECONDS)) {
    try {
        if (lock2.tryLock(100, TimeUnit.MILLISECONDS)) {
            // Do work
        }
    } finally {
        lock1.unlock();
        lock2.unlock();
    }
}
```

---

### **🔹 3.** 

### **Lock timeout and backoff algorithms**

  

Used in high-concurrency systems — abandon request after a timeout and retry later.

---

### **🔹 4.** 

### **Use high-level constructs**

  

Use:

- Executors
    
- ConcurrentHashMap
    
- BlockingQueue
    
    which **internally manage locks safely**.
    

---

### **🔍 JVM Tools for Detection:**

  

Use tools like:

- jstack
    
- VisualVM
    
- Java Mission Control
    
    to detect deadlocks at runtime.
    

---

## **🔚 Final Interview-Ready Tips:**

|**Topic**|**Don’t Miss**|
|---|---|
|Intrinsic Locks|Locked on this or Class, reentrant|
|Atomicity|Compound ops like i++ are **not** atomic|
|Lock Safety|Use Atomic* classes for high-concurrency counters|
|Deadlock Debugging|Use jstack, design lock ordering|
|Reentrancy|Prevents self-deadlock on recursive synchronized calls|

---




## **✅ 311.** 

## **How can we detect a Deadlock situation?**

  

### **🔹 Programmatically (Java 1.5+):**

```
ThreadMXBean bean = ManagementFactory.getThreadMXBean();
long[] ids = bean.findDeadlockedThreads();
if (ids != null) {
    ThreadInfo[] infos = bean.getThreadInfo(ids);
    for (ThreadInfo info : infos) {
        System.out.println("Deadlocked thread: " + info.getThreadName());
    }
}
```

### **🔹 JVM Tools:**

- jstack <pid> → detects “Found one Java-level deadlock”
    
- **VisualVM**, **Java Mission Control**, **jConsole** → thread tab → detects deadlocks visually
    

  

> 🔍 JVM captures **both intrinsic and explicit lock** deadlocks (e.g., ReentrantLock).

---

## **✅ 312.** 

## **What is a Livelock?**

  

A **livelock** occurs when two or more threads **continuously change state** in response to each other **but make no actual progress**.

  

### **🔥 Example:**

```
Thread A: tries to avoid conflict → yields  
Thread B: tries to avoid conflict → yields  
Repeat forever, no one proceeds
```

> 🧠 Think of two people stepping side-to-side to avoid blocking each other in a hallway — forever.

  

### **🛠️ Solution:**

- Add backoff strategies
    
- Use retry limits
    
- Use atomic coordination
    

---

## **✅ 313.** 

## **What is Thread starvation?**

  

**Starvation** occurs when a thread is **indefinitely blocked from accessing CPU or resources**, because other higher-priority threads are constantly favored.

  

### **🔍 Common Causes:**

- Using unfair locks
    
- Infinite loops with while(true) on high-priority threads
    
- Threads holding shared resource without yielding
    

---

## **✅ 314.** 

## **How can a synchronized block cause Thread starvation in Java?**

  

If a thread holds a **synchronized lock** and:

- Performs long-running tasks
    
- Never yields control
    
- Prevents lower-priority threads from acquiring the lock
    

  

Then **other threads starve** for the monitor lock.

```
synchronized (sharedLock) {
    while (true) {
        // monopolizing the lock — others blocked
    }
}
```

> 🔥 To avoid: Keep synchronized blocks **minimal and efficient**.

---

## **✅ 315.** 

## **What is a Race condition?**

  

A **race condition** occurs when:

- Two or more threads access **shared mutable state**
    
- The **correctness** of the outcome depends on **timing/interleaving**
    
- No synchronization or coordination is present
    

  

### **🔥 Example:**

```
// Both threads increment count concurrently
count++; // Not atomic → leads to lost updates
```

> 🧠 Race conditions can lead to **inconsistent state**, especially in **banking, inventory, or counters**.

---

## **✅ 316.** 

## **What is a Fair lock in multi-threading?**

  

A **fair lock** ensures **first-come-first-serve (FIFO)** acquisition of the lock.

  

### **🔹 Example:**

```
ReentrantLock fairLock = new ReentrantLock(true); // fairness = true
```

> 🔍 With a fair lock, threads **acquire the lock in the order** they requested it.

  

### **⚠️ Downside:**

- More context switches
    
- Slower than unfair locks
    

---

## **✅ 317.** 

## **Which two methods of Object class can be used to implement a Producer-Consumer scenario?**

  

### **✅** 

### **wait()**

###  **and** 

### **notify()**

###  **(or** 

### **notifyAll()**

### **)**

  

Used for **inter-thread communication**, especially in **bounded buffer scenarios**.

```
synchronized (buffer) {
    while (buffer.isEmpty()) {
        buffer.wait();
    }
    buffer.notify(); // Notify waiting producers or consumers
}
```

> 🧠 Use wait() inside a loop (not if) — to re-check condition after spurious wakeups.

---

## **✅ 318.** 

## **How JVM determines which thread should wake up on notify()?**

  

**JVM does not guarantee any order** when selecting which thread to wake up.

- If multiple threads are waiting on the same monitor:
    
    - notify() wakes **one random** thread
        
    - notifyAll() wakes **all** waiting threads → only one gets lock, rest re-enter waiting
        
    

  

> 🔍 Scheduling and wake-up behavior are **OS- and JVM-dependent**.

  

### **✅ Recommendation:**

  

Use notifyAll() unless you’re sure **only one consumer** exists.

---

## **✅ 319.** 

## **Check if the following code is thread-safe for retrieving an integer value from a Queue?**

```
Queue<Integer> queue = new LinkedList<>();

public Integer pollQueue() {
    return queue.poll();
}
```

### **❌** 

### **Not thread-safe**

- LinkedList is not thread-safe.
    
- Concurrent access can lead to:
    
    - Corruption
        
    - NullPointerException
        
    - Infinite loops
        
    

  

### **✅ Fix:**

  

Use BlockingQueue or external synchronization.

```
BlockingQueue<Integer> queue = new LinkedBlockingQueue<>();
public Integer pollQueue() {
    return queue.poll();
}
```

Or:

```
synchronized (queue) {
    return queue.poll();
}
```

---

## **✅ 320.** 

## **How can we check if a thread has a monitor lock on a given object?**

  

### **🔍 JVM provides** 

### **Thread.holdsLock(Object obj)**

### **:**

```
if (Thread.holdsLock(myObject)) {
    System.out.println("Current thread holds lock on myObject");
}
```

### **🔥 Use case:**

- Useful in complex lock management
    
- Helps debug **synchronization issues**
    
- Validate lock preconditions
    

---

## **🧠 Deep Insights Most Candidates Miss**

|**Concept**|**Insight**|
|---|---|
|notify() behavior|Wakes a **random** thread — not FIFO|
|Fair vs unfair locks|Fair locks ≠ always better — adds latency due to context switching|
|wait() in a loop|Required due to **spurious wakeups**|
|Livelock vs Deadlock|Livelock = active but stuck, Deadlock = blocked and stuck|
|Thread.holdsLock()|Often missed in debugging scenarios|
|BlockingQueue vs Queue|Thread-safe alternative that handles producer-consumer cases gracefully|

---



## **✅ 321.** 

## **What is the use of yield() method in Thread class?**

  

The Thread.yield() method is a **hint to the scheduler** that the current thread is willing to **pause its execution**, allowing other threads of **equal or higher priority** to execute.

```
Thread.yield(); // Suggests the scheduler to reschedule
```

### **🔍 Internals:**

- It **does NOT release locks**.
    
- It may or may not cause actual yielding — depends on OS and JVM.
    
- It’s often used in spin-wait loops or low-priority background threads.
    

  

> ⚠️ Do not rely on yield() for synchronization or fairness. It’s non-deterministic.

---

## **✅ 322.** 

## **What is an important point to consider while passing an object from one thread to another thread?**

  

**Thread safety and visibility.**

  

When passing objects between threads:

  

### **✅ Consider:**

1. **Mutability**: Is the object being shared mutable?
    
2. **Thread safety**: Are all accesses to shared state properly synchronized?
    
3. **Happens-before relationship**: Ensure visibility using:
    
    - Volatile
        
    - Synchronization
        
    - Atomic references
        
    - Final fields in constructors
        
    

  

> 🧠 If a thread modifies an object and another thread reads it, there must be a **happens-before** edge to guarantee visibility.

---

## **✅ 323.** 

## **What are the rules for creating Immutable Objects?**

  

### **🔒 To make a class truly** 

### **immutable**

### **:**

1. Declare the class final
    
2. Make all fields private final
    
3. Do not provide setters
    
4. Initialize fields via constructor
    
5. Do **deep copies** of mutable objects (e.g., Date, collections)
    
6. Avoid exposing internal state via getters
    

```
public final class Person {
    private final String name;
    private final List<String> hobbies;

    public Person(String name, List<String> hobbies) {
        this.name = name;
        this.hobbies = List.copyOf(hobbies); // defensive copy
    }

    public List<String> getHobbies() {
        return List.copyOf(hobbies); // prevents mutation
    }
}
```

> 💡 Immutable objects are inherently **thread-safe**.

---

## **✅ 324.** 

## **What is the use of ThreadLocal class?**

  

ThreadLocal<T> provides **thread-local variables** — each thread accessing the variable has its own **independent copy**, isolated from others.

```
ThreadLocal<Integer> threadLocalId = ThreadLocal.withInitial(() -> 0);
```

### **🔍 Internals:**

- Each thread has a **ThreadLocalMap**
    
- ThreadLocal avoids synchronization for per-thread state
    
- Common in:
    
    - Request tracing
        
    - User sessions
        
    - DB connections per thread
        
    

  

> ⚠️ Memory leak risk in **thread pools** if remove() is not called.

---

## **✅ 325.** 

## **What are the scenarios suitable for using ThreadLocal class?**

  

### **✅ Ideal for:**

1. **Per-thread state caching**
    
2. **Avoiding passing context explicitly**
    
3. **Thread-safe object reuse**:
    
    - SimpleDateFormat
        
    - JDBC connections
        
    - Security context
        
    - Request-scoped beans in web apps
        
    

```
private static final ThreadLocal<SimpleDateFormat> formatter =
    ThreadLocal.withInitial(() -> new SimpleDateFormat("yyyy-MM-dd"));
```

> ⚠️ Clean up using remove() after use in thread pools to prevent leaks.

---

## **✅ 326.** 

## **How will you improve the performance of an application by multithreading?**

  

### **✅ Strategies:**

1. **Decompose into independent tasks**
    
    - I/O operations
        
    - CPU-heavy computations
        
    
2. **Parallelize using:**
    
    - ExecutorService
        
    - ForkJoinPool
        
    - CompletableFuture
        
    
3. **Use asynchronous models** where possible:
    
    - Non-blocking I/O
        
    - Reactive programming
        
    
4. **Minimize lock contention**
    
    - Use fine-grained locking or lock-free data structures
        
    
5. **Leverage multi-core CPUs**
    

  

> 🧠 Remember: More threads ≠ better performance unless task granularity is well-managed.

---

## **✅ 327.** 

## **What is scalability in a software program?**

  

Scalability is the system’s ability to **handle increased load** (users, requests, data, etc.) by **increasing resources** without degrading performance.

  

### **🔍 Types:**

- **Vertical scaling**: Adding more power (CPU/RAM) to a single machine
    
- **Horizontal scaling**: Adding more machines (distributed systems)
    

  

### **📈 For multithreading:**

  

A system is scalable if adding threads or cores **leads to higher throughput** — up to a point.

---

## **✅ 328.** 

## **How will you calculate the maximum speed up of an application by using multiple processors?**

  

### **✅ Use** 

### **Amdahl’s Law**

### **:**

  

\text{Speedup} = \frac{1}{(1 - P) + \frac{P}{N}}

  

Where:

- P = Proportion of the program that can be parallelized
    
- N = Number of processors
    

  

### **🔍 Implication:**

- Even with infinite processors, speedup is limited by the **serial portion** of the code.
    

  

> 🧠 Best use: Identify **bottlenecks** that cannot be parallelized.

---

## **✅ 329.** 

## **What is Lock contention in multithreading?**

  

**Lock contention** occurs when multiple threads try to acquire the same lock **simultaneously**, leading to **blocked threads**, **reduced throughput**, and **performance degradation**.

  

### **🔍 Symptoms:**

- High thread CPU usage with low work done
    
- Threads stuck in BLOCKED state
    
- Long GC pauses (due to held locks)
    

  

### **Tools:**

- VisualVM
    
- jstack showing blocked threads
    
- Java Flight Recorder (JFR)
    

---

## **✅ 330.** 

## **What are the techniques to reduce Lock contention?**

  

### **✅ Top Strategies:**

|**Technique**|**Purpose**|
|---|---|
|**Use finer-grained locks**|Reduce scope of locking|
|**Use ReentrantLock.tryLock()**|Avoid waiting forever|
|**Use concurrent collections**|ConcurrentHashMap, BlockingQueue|
|**Use immutable data**|Avoid shared state|
|**Reduce synchronization scope**|Sync only where needed|
|**Read-write locks**|ReentrantReadWriteLock for read-heavy workloads|
|**Lock striping**|Multiple locks for different subsets of data|
|**Use CAS**|Lock-free updates via Atomic* classes|

> 🧠 Lock contention scales **non-linearly** — reducing it early saves more than fixing it later.

---

## **🔚 Final Pro Interview Insights**

|**Topic**|**Interview Edge You’ll Have**|
|---|---|
|ThreadLocal pitfalls|Mention remove() in thread pools to show depth|
|Scalability|Refer to **Amdahl’s Law** with real examples|
|Lock contention|Cite use of **striping, CAS, concurrent utils**|
|yield()|Clarify it’s a **scheduler hint**, not a synchronization tool|
|Immutable patterns|Mention **deep copy**, not just final and no setters|

---



## **✅ 331.** 

## **What technique can be used in the following code to reduce Lock contention?**

```
public class Counter {
    private int[] buckets = new int[10];

    public synchronized void increment(int index) {
        buckets[index]++;
    }
}
```

### **🔥 Problem:**

- Entire method is synchronized → **global lock** across all buckets
    
- Even independent buckets[index] calls must wait
    

  

### **✅ Solution:** 

### **Use Lock Striping**

  

Replace single global lock with **per-bucket lock**.

```
private final Object[] locks = new Object[10];

public Counter() {
    for (int i = 0; i < 10; i++) locks[i] = new Object();
}

public void increment(int index) {
    synchronized (locks[index]) {
        buckets[index]++;
    }
}
```

> 🧠 This reduces contention by **allowing multiple threads to work on different buckets simultaneously**.

---

## **✅ 332.** 

## **What is Lock Splitting technique?**

  

**Lock Splitting** divides a single coarse-grained lock into **multiple independent locks** that guard different internal states of an object.

  

### **🔍 Used When:**

- Object has multiple independent fields
    
- Threads frequently access disjoint parts
    

  

### **🧠 Example:**

  

A Hashtable with one lock suffers from contention. ConcurrentHashMap uses lock splitting:

- Each bucket or segment has its own lock
    

  

### **Benefits:**

- Increased throughput
    
- Fine-grained concurrency
    

  

> 🔥 JVM itself uses lock splitting in class metadata, hash tables, and memory managers.

---

## **✅ 333.** 

## **Which technique is used in ReadWriteLock class for reducing lock contention?**

  

**Reader-writer decomposition** (also known as **read-write lock** pattern)

  

### **✅ Mechanism:**

- Multiple readers can access the resource **concurrently**
    
- Only one writer is allowed at a time (exclusive lock)
    

```
ReadWriteLock lock = new ReentrantReadWriteLock();
lock.readLock().lock();
// multiple readers allowed
```

### **🧠 Ideal for:**

- **Read-heavy** systems like caches, config managers, file scanners
    
- Reduces write starvation via fair locking policies
    

---

## **✅ 334.** 

## **What is Lock Striping?**

  

Lock Striping = Using **an array of smaller locks** to guard a larger shared data structure.

```
Object[] locks = new Object[16]; // stripes
int hash = key.hashCode() % locks.length;
synchronized(locks[hash]) {
    // operate on partitioned resource
}
```

### **✅ Real-World Use:**

- ConcurrentHashMap (Java 7) uses lock striping per segment
    
- Allows higher concurrency with reduced contention
    

  

> 🔍 Modern ConcurrentHashMap (Java 8+) uses **CAS + synchronized fallback**, not lock striping.

---

## **✅ 335.** 

## **What is a CAS operation?**

  

**CAS = Compare-And-Swap**

  

A **lock-free**, atomic operation supported at the **CPU level** that does:

```
if (current == expected) {
    current = newValue;
    return true;
}
```

### **Used in:**

- Atomic classes (AtomicInteger, AtomicReference)
    
- Lock-free queues/stacks
    
- Synchronizers like StampedLock
    

  

### **CPU Instruction:**

- CMPXCHG on x86
    

  

> 🔍 CAS is the foundation of **non-blocking concurrency** in Java and avoids kernel-level locking.

---

## **✅ 336.** 

## **Which Java classes use CAS operation?**

  

### **✅ Key CAS-enabled classes:**

- AtomicInteger, AtomicLong, AtomicReference
    
- ConcurrentLinkedQueue
    
- ConcurrentHashMap (Java 8+)
    
- LongAdder, Striped64
    
- StampedLock
    

  

### **🔍 Internals:**

- Backed by **Unsafe.compareAndSwap*** methods
    
- Uses **looping retry** on CAS failure (spin-based)
    
- Avoids context switching and reduces lock contention
    

---

## **✅ 337.** 

## **Is it always possible to improve performance by object pooling in a multithreading application?**

  

**No** — object pooling is **not a guaranteed performance win** in multithreading. It can actually **degrade performance** due to:

  

### **❌ Downsides:**

- **Contention on the pool itself** (locks/synchronization)
    
- **Wasted memory** (over-pooling)
    
- **GC pressure** due to retained references
    
- **Increased complexity** and bugs
    

  

### **✅ Only use pooling for:**

- **Expensive-to-create** objects (e.g., DB connections, threads)
    
- **Recyclable resources** (e.g., buffers, parsers)
    

  

> 🧠 For cheap, short-lived, non-GC-heavy objects, pooling is **counterproductive** in modern JVMs.

---

## **✅ 338.** 

## **How can techniques used for performance improvement in a single-threaded application degrade the performance in a multithreading application?**

  

### **🔥 Examples:**

|**Single-thread Optim**|**Multithread Penalty**|
|---|---|
|Caching in static field|Shared state → synchronization overhead|
|Using non-thread-safe collections|Race conditions, data corruption|
|Aggressive object reuse|False sharing, cache line contention|
|Manual memory reuse|Increased GC retention → memory leaks|
|Tight loops without yielding|CPU monopolization in thread pools|

> 🧠 Optimizations must shift from **“speed” to “concurrency awareness”** in multi-threaded code.

---

## **✅ 339.** 

## **What is the relation between Executor and ExecutorService interface?**

- Executor is the **base interface** with a single method:
    

```
void execute(Runnable command);
```

- ExecutorService extends Executor and adds:
    
    - Lifecycle management (shutdown(), awaitTermination())
        
    - Task submission (submit())
        
    - invokeAll(), invokeAny()
        
    - Future-based handling
        
    

  

### **✅ Example:**

```
ExecutorService pool = Executors.newFixedThreadPool(10);
pool.submit(() -> System.out.println("Task"));
pool.shutdown();
```

> 🧠 Always prefer ExecutorService or even ScheduledExecutorService for real-world apps — they provide **better control and safety**.

---

## **✅ 340.** 

## **What will happen on calling submit() method of an ExecutorService instance whose queue is already full?**

  

It depends on the **BlockingQueue implementation** and **RejectedExecutionHandler** strategy.

  

### **🔍 Scenario:**

```
ThreadPoolExecutor executor = new ThreadPoolExecutor(
    2, 4,
    60L, TimeUnit.SECONDS,
    new ArrayBlockingQueue<>(2),
    new ThreadPoolExecutor.AbortPolicy() // default
);
```

If the pool size is maxed out and the queue is full:

```
executor.submit(task); // ❌ throws RejectedExecutionException
```

### **✅ Other handlers:**

|**Policy**|**Behavior**|
|---|---|
|AbortPolicy (default)|Throws exception|
|CallerRunsPolicy|Runs task in calling thread|
|DiscardPolicy|Silently drops the task|
|DiscardOldestPolicy|Drops oldest task in queue, enqueues new|

> 🧠 Use metrics + monitoring to detect saturation — not just exception handling.

---

## **🔚 Interview-Winning Tips Summary**

|**Insightful Nugget**|**Why Interviewers Love It**|
|---|---|
|Lock Striping vs Lock Splitting|Demonstrates system-level thinking|
|submit() behavior on full queue|Real-world handling of thread pool saturation|
|CAS Internals|Shows knowledge of lock-free and hardware-level ops|
|Amdahl’s Law vs Object Pooling|Shows you think in tradeoffs, not cargo cults|
|ThreadLocal cleanup|Prevents leaks in real prod systems|

---




## **✅ 341.** 

## **What is a ScheduledExecutorService?**

  

ScheduledExecutorService is an interface in java.util.concurrent that allows you to:

- **Schedule tasks** to run after a delay
    
- **Run tasks periodically** at a fixed rate or fixed delay
    

```
ScheduledExecutorService scheduler = Executors.newScheduledThreadPool(2);
scheduler.schedule(() -> System.out.println("Run after delay"), 5, TimeUnit.SECONDS);
scheduler.scheduleAtFixedRate(() -> doWork(), 0, 10, TimeUnit.SECONDS);
```

### **🔍 Types of Scheduling:**

|**Method**|**Description**|
|---|---|
|schedule()|One-time delay|
|scheduleAtFixedRate()|Fixed interval between **task starts**|
|scheduleWithFixedDelay()|Fixed interval between **task ends** and next start|

### **🔬 Internals:**

- Backed by a **DelayedWorkQueue**
    
- Uses **timer wheels** internally for scheduling precision
    
- Exception in scheduled task will cancel that task but not the scheduler
    

  

> 🧠 Often preferred over Timer because it’s thread-safe, handles exceptions better, and allows concurrent task execution.

---

## **✅ 342.** 

## **How will you create a Thread pool in Java?**

  

Java provides the ExecutorService interface to manage thread pools:

  

### **✅ Common ways:**

```
// Fixed number of threads
ExecutorService fixedPool = Executors.newFixedThreadPool(4);

// Cached pool (unbounded)
ExecutorService cachedPool = Executors.newCachedThreadPool();

// Single-threaded executor
ExecutorService single = Executors.newSingleThreadExecutor();

// Custom thread pool (full control)
ThreadPoolExecutor pool = new ThreadPoolExecutor(
    4, 8, 60L, TimeUnit.SECONDS,
    new ArrayBlockingQueue<>(100),
    Executors.defaultThreadFactory(),
    new ThreadPoolExecutor.AbortPolicy()
);
```

### **🔍 Thread Pool Parameters:**

- **corePoolSize**
    
- **maximumPoolSize**
    
- **keepAliveTime**
    
- **BlockingQueue**
    
- **ThreadFactory**
    
- **RejectedExecutionHandler**
    

  

> 🧠 Always shut down a pool gracefully with shutdown() or shutdownNow().

---

## **✅ 343.** 

## **What is the main difference between Runnable and Callable interface?**

|**Feature**|Runnable|Callable<V>|
|---|---|---|
|Return value|❌ No return|✅ Returns result of type V|
|Exceptions|❌ Can’t throw checked|✅ Can throw checked exceptions|
|Integration|Thread, ExecutorService|Only ExecutorService.submit()|
|Use cases|Fire-and-forget tasks|Compute tasks with result|

```
Callable<Integer> task = () -> 2 + 3;
Future<Integer> result = executor.submit(task);
```

> 🔥 Interview trap: You can’t use Thread constructor with Callable.

---

## **✅ 344.** 

## **What are the uses of Future interface in Java?**

  

Future<V> represents the **result of an asynchronous computation**, returned by ExecutorService.submit().

  

### **🔍 Key methods:**

|**Method**|**Purpose**|
|---|---|
|get()|Block until result is ready|
|get(timeout)|Wait with timeout|
|cancel()|Attempts to stop task|
|isDone()|Returns true if task is complete|
|isCancelled()|Returns true if task was cancelled|

```
Future<Integer> future = executor.submit(() -> expensiveCalculation());
Integer result = future.get(); // blocks
```

### **⚠️ Caveats:**

- get() is **blocking** — avoid calling it on main/UI thread
    
- Canceled tasks may not stop unless task checks Thread.interrupted()
    

  

> 🧠 FutureTask is the implementation that wraps Callable and manages result internally.

---

## **✅ 345.** 

## **What is the difference in concurrency in HashMap and Hashtable?**

|**Feature**|HashMap|Hashtable|
|---|---|---|
|Thread-safety|❌ Not thread-safe|✅ Fully synchronized|
|Performance|Faster in single-threaded|Slower due to locking|
|Null keys/values|✅ Allows 1 null key, many null values|❌ No null key or value allowed|
|Synchronization|You must handle externally|Built-in synchronization|

### **🔥 Internals:**

- Hashtable synchronizes **every method**, even read operations.
    
- HashMap requires **ConcurrentHashMap** or Collections.synchronizedMap() for thread safety.
    

  

> 🧠 Modern Java discourages Hashtable. Prefer **ConcurrentHashMap** for concurrent access.

---

## **✅ 346.** 

## **How will you create synchronized instance of List or Map Collection?**

  

Java provides **wrapper methods** in Collections class:

```
List<String> syncList = Collections.synchronizedList(new ArrayList<>());
Map<String, String> syncMap = Collections.synchronizedMap(new HashMap<>());
```

### **⚠️ Important:**

- These wrappers synchronize **each method**.
    
- **Iteration must be manually synchronized** to avoid ConcurrentModificationException.
    

```
synchronized (syncList) {
    for (String item : syncList) {
        // safe iteration
    }
}
```

> 🧠 These are **coarse-grained** locks. For better scalability, use ConcurrentHashMap, CopyOnWriteArrayList, etc.

---

## **🔍 BONUS: Interview Insights Most Candidates Miss**

|**Detail**|**Why It Matters**|
|---|---|
|ScheduledExecutorService vs Timer|Timer uses a single thread; ScheduledExecutor scales better|
|Future.get() caveats|Blocking call → can hang if not used with timeout|
|ThreadPoolExecutor rejection strategies|Shows real-world readiness (e.g., CallerRunsPolicy)|
|Callable for checked exceptions|Runnable can’t propagate checked exceptions cleanly|
|Manual sync on synchronizedList.iterator()|Missed by 90% of candidates — leads to ConcurrentModificationException|

---




## **✅ 347.** 

## **What is a Semaphore in Java?**

  

A Semaphore is a **counting-based concurrency control mechanism** from java.util.concurrent. It limits the **number of threads** that can access a resource simultaneously.

```
Semaphore semaphore = new Semaphore(3); // 3 permits
semaphore.acquire(); // blocks if no permits available
try {
    // access shared resource
} finally {
    semaphore.release(); // return permit
}
```

### **🔍 Types:**

- **Fair semaphore**: FIFO granting of permits.
    
- **Unfair semaphore**: May allow barging (default, better performance).
    

  

### **🧠 Real-World Uses:**

- Connection pools
    
- Rate limiting
    
- Limiting concurrent API usage
    
- Bounded processing (e.g. printing 3 documents at a time)
    

---

## **✅ 348.** 

## **What is a CountDownLatch in Java?**

  

CountDownLatch allows one or more threads to **wait until a set of operations are completed** by other threads.

```
CountDownLatch latch = new CountDownLatch(3);

new Thread(() -> {
    // Task done
    latch.countDown();
}).start();

latch.await(); // blocks until count reaches 0
```

### **🔍 Key Properties:**

- **One-time use**: Cannot be reset
    
- Thread-safe
    
- Does not support cyclic use like CyclicBarrier
    

---

## **✅ 349.** 

## **What is the difference between CountDownLatch and CyclicBarrier?**

|**Feature**|CountDownLatch|CyclicBarrier|
|---|---|---|
|Resettable|❌ No|✅ Yes (can be reused)|
|Waits for|One or more threads|A fixed number of threads|
|Use case|Master-worker, task dependency|Barrier-based coordination|
|Runnable hook|❌ No callback support|✅ Can run a task at barrier point|

### **🧠 Interview Tip:**

  

Use CountDownLatch when tasks are **independent** but one thread **must wait**, and CyclicBarrier when threads need to **meet at a checkpoint**.

---

## **✅ 350.** 

## **What are the scenarios suitable for using Fork/Join framework?**

  

### **✅ Best for:**

- Divide-and-conquer parallelism
    
- CPU-bound recursive tasks
    
- Tree-based processing (XML, directory traversal)
    
- Mergesort, quicksort, map-reduce-style logic
    

```
ForkJoinPool pool = ForkJoinPool.commonPool();
pool.invoke(new MyRecursiveTask());
```

### **🔍 Internals:**

- **Work-stealing**: Idle threads “steal” subtasks from busy ones
    
- Uses **Deque** internally for load balancing
    
- Introduced in Java 7
    

  

> ⚠️ Inefficient for I/O-bound tasks. Use ExecutorService instead.

---

## **✅ 351.** 

## **What is the difference between RecursiveTask and RecursiveAction?**

|**Feature**|RecursiveTask<V>|RecursiveAction|
|---|---|---|
|Return type|✅ Has return value|❌ Void return|
|Typical usage|Sum, result computation|File traversal, action-only tasks|

### **✅ Example:**

```
class SumTask extends RecursiveTask<Integer> {
    protected Integer compute() { return 1 + 2; }
}

class PrintTask extends RecursiveAction {
    protected void compute() { System.out.println("Hello"); }
}
```

> 🧠 RecursiveTask = “what”, RecursiveAction = “do”.

---

## **✅ 352.** 

## **In Java 8, can we process stream operations with a Thread pool?**

  

### **✅ YES — but** 

### **not with parallelStream() directly**

### **.**

  

To use a **custom thread pool**, you must submit the **entire stream processing** to a pool:

```
ExecutorService executor = Executors.newFixedThreadPool(4);
List<Integer> result = executor.submit(() ->
    list.stream().map(...).collect(Collectors.toList())
).get();
```

> ⚠️ parallelStream() uses **common ForkJoinPool**, which is **shared globally**.

  

### **🧠 Why important?**

  

Using parallelStream() in web servers like Tomcat can cause **ForkJoinPool starvation**, degrading request processing.

---

## **✅ 353.** 

## **What are the scenarios to use parallel stream in Java 8?**

  

### **✅ Best for:**

- CPU-bound operations
    
- Large datasets
    
- Independent, stateless operations
    

  

### **❌ Avoid when:**

- Side effects exist (I/O, shared state)
    
- Order must be preserved
    
- Task is I/O-bound or blocking
    
- Under small dataset (<1000 elements)
    

  

> 🧠 Always measure performance — parallelStream() may be slower due to thread management overhead.

---

## **✅ 354.** 

## **How Stack and Heap work in Java multi-threading environment?**

|**Memory Area**|**Behavior in Multithreading**|
|---|---|
|**Heap**|Shared among all threads. Objects live here.|
|**Stack**|Each thread has its **own stack**. Stores method frames, local vars, PC register.|

### **🔍 Key Concepts:**

- Thread-local variables are stored in **Thread Stack**
    
- All objects created via new are in Heap, but references can be stack-allocated
    
- ThreadLocal uses internal map stored in the **Thread object**
    

  

> 🧠 Stack memory is safe by default. Heap access must be **synchronized or guarded**.

---

## **✅ 355.** 

## **How can we take Thread dump in Java?**

  

### **🔹 Ways to take thread dump:**

|**Method**|**Description**|
|---|---|
|jstack <pid>|CLI tool for live JVM thread dump|
|kill -3 <pid> (Unix)|Sends SIGQUIT, prints to stderr|
|**VisualVM / JMC / jConsole**|GUI-based thread dump|
|Programmatic|Thread.getAllStackTraces()|

> 🧠 Use thread dumps to identify deadlocks, bottlenecks, blocked threads.

---

## **✅ 356.** 

## **Which parameter can be used to control stack size of a thread in Java?**

  

Use Thread constructor:

```
Thread t = new Thread(null, runnable, "worker", 1 * 1024 * 1024);
```

Or, for java command-line:

```
java -Xss512k MyApp
```

### **🧠 Why control it?**

- Large recursion → needs large stack
    
- Small stack → lower memory footprint for thousands of threads
    

  

> ⚠️ Too small = StackOverflowError. Tune based on method call depth.

---

## **✅ 357.** 

## **There are two threads T1 and T2. How will you ensure that these threads run in sequence T1, then T2 in Java?**

  

### **✅ Option 1:** 

### **join()**

```
Thread t1 = new Thread(() -> System.out.println("T1"));
Thread t2 = new Thread(() -> {
    try { t1.join(); } catch (InterruptedException e) {}
    System.out.println("T2");
});

t1.start();
t2.start();
```

### **✅ Option 2:** 

### **CountDownLatch**

```
CountDownLatch latch = new CountDownLatch(1);

Thread t1 = new Thread(() -> {
    System.out.println("T1");
    latch.countDown();
});
Thread t2 = new Thread(() -> {
    try { latch.await(); } catch (InterruptedException e) {}
    System.out.println("T2");
});
```

### **✅ Option 3:** 

### **Executors**

  

Use a single-threaded executor to guarantee order.

---

## **🧠 Hidden Interview Gems Most Miss**

|**Concept**|**Insight**|
|---|---|
|ForkJoinPool common pitfalls|Don’t use parallelStream in servlet containers|
|-Xss tuning|Crucial for high-scale apps with many threads|
|Work stealing|ForkJoinPool uses **Deque + LIFO/FIFO + CAS**|
|Thread.getAllStackTraces()|Can be used in diagnostics or profilers|
|RecursiveAction vs Task|Return value = use Task, else use Action|

---

