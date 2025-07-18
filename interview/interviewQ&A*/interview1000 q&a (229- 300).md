
## **✅ 229. What are the main Concurrent Collection classes in Java?**

| **Collection Type** | **Class**                               | **Notes**                      |
| ------------------- | --------------------------------------- | ------------------------------ |
| **List**            | CopyOnWriteArrayList                    | Read-heavy use cases           |
| **Set**             | CopyOnWriteArraySet                     | Backed by CopyOnWriteArrayList |
| **Map**             | ConcurrentHashMap                       | Highly concurrent              |
| **Queue**           | ConcurrentLinkedQueue                   | Lock-free                      |
| **Deque**           | ConcurrentLinkedDeque                   | Double-ended, lock-free        |
| **BlockingQueue**   | ArrayBlockingQueue, LinkedBlockingQueue | Blocking on insert/retrieve    |
> ✅ All classes in java.util.concurrent designed for high concurrency without external synchronization.


## **✅ 230. How will you convert a Collection to SynchronizedCollection in Java?**

Use Collections.synchronized*() wrapper methods:
```

List<String> syncList = Collections.synchronizedList(new ArrayList<>());
Set<String> syncSet = Collections.synchronizedSet(new HashSet<>());
Map<String, Integer> syncMap = Collections.synchronizedMap(new HashMap<>());
```

### **⚠️ Caveats:**

- Synchronization is done at **collection level**, not iteration level.
    
- Always **wrap iteration block** with synchronized keyword:
```
synchronized(syncList) {
    for (String item : syncList) {
        // Safe iteration
    }
}
```

> ✅ Prefer Concurrent classes over these in multithreaded environments for better performance.


## **✅ 231. How is** IdentityHashMap different from a regular map in java?

  

IdentityHashMap is a **Map** implementation where **key equality is based on reference (==) instead of equals()**.

  

### **⚖️ Comparison with HashMap:**

|**Feature**|HashMap|IdentityHashMap|
|---|---|---|
|**Key Comparison**|equals() method|== (reference equality)|
|**hashCode usage**|hashCode() method|System.identityHashCode()|
|**Allows null keys**|✅ Yes (only one null key)|✅ Yes (multiple null keys allowed)|
|**Use-case**|General-purpose key-value|Object identity tracking|
|**Performance**|Better for logical equality|Slightly faster for identity comparison|
|**Internals**|Hash table with chaining|Open-addressing hash table|

### **💡 Example:**

```
Map<String, String> map1 = new HashMap<>();
Map<String, String> map2 = new IdentityHashMap<>();

String a = new String("key");
String b = new String("key");

map1.put(a, "A");
map1.put(b, "B"); // Overwrites value due to equals()

map2.put(a, "A");
map2.put(b, "B"); // Keeps both since a != b (by reference)
```

---

## **✅ 232. What is the main use of** 

## **IdentityHashMap**

## **?**

  

The primary use of IdentityHashMap is when **reference identity (==) is required instead of logical equality**.

  

### **✅ Typical Use Cases:**

- **Object graph traversal** where identity matters (e.g., serialization frameworks).
    
- **Caching objects** with **no overridden equals() and hashCode()**.
    
- Implementing **“visited” tracking** during recursive graph algorithms.
    

  

> 🧠 Example: Used internally in Java’s ObjectOutputStream for detecting previously serialized objects.

---

## **✅ 233. How can we improve the performance of** 

## **IdentityHashMap**  ?

  

While IdentityHashMap is already lightweight, you can improve its performance by:

  

### **🔧 Optimization Tips:**

1. **Set initial capacity correctly** to avoid resizing:
    

```
Map<Object, String> map = new IdentityHashMap<>(100);
```

1.   
    
2. **Avoid frequent resizing**: IdentityHashMap uses **open addressing**, so resizing is costly.
    
3. **Avoid autoboxing of primitives** (like Integer, Double), since identity semantics with boxed values can be **confusing** due to caching of some boxed values.
    
4. **Use where identity comparison is meaningful** — misuse (e.g., with Strings) can lead to subtle bugs.
    

  

> ✅ Best used in internal framework code where you control object instantiation.

---

## **✅ 234. Is IdentityHashMap thread-safe  ? 


  

❌ **No**, IdentityHashMap is **not thread-safe**.

  

> All operations are **non-synchronized**. If multiple threads access the map concurrently and at least one thread modifies it structurally, external synchronization is required.

  

### **✅ To make it thread-safe:**

```
Map<Object, String> syncMap = Collections.synchronizedMap(new IdentityHashMap<>());
```

### **⚠️ Caution:**

  

Even with synchronization, iterating over the map still requires manual synchronization:

```
synchronized(syncMap) {
    for (Object key : syncMap.keySet()) {
        // Safe iteration
    }
}
```

---

## **✅ 235. What is a** WeakHashMap in java ?

  

A WeakHashMap is a **Map** implementation where the keys are held using **weak references**.

  

> When a key is **no longer in ordinary use** (i.e. not strongly reachable elsewhere), it becomes eligible for **garbage collection**, and its entry is removed from the map automatically.

  

### **🧠 Internal Working:**

- Keys are wrapped in java.lang.ref.WeakReference.
    
- A background thread (ReferenceQueue) cleans up stale entries.
    

  

### **💡 Example:**

```
Map<Object, String> map = new WeakHashMap<>();
Object key = new Object();
map.put(key, "value");

key = null; // Now only the weak reference remains
System.gc(); // Entry may be removed
```

### **✅ Use Cases:**

- **Caches**: where you don’t want to prevent GC of unused keys.
    
- **Canonicalization tables**.
    
- Used internally in frameworks (e.g., **Spring**, **Hibernate**).
    

  

### **🔍 Comparison Table:**

|**Feature**|**WeakHashMap**|**HashMap**|
|---|---|---|
|Key storage|WeakReference|Strong reference|
|GC behavior|Automatically removed|Remains until explicitly removed|
|Thread-safe|❌ No|❌ No|


|**Feature**|**WeakHashMap**|
|---|---|
|GC behavior|Removes key-value when key is GC’ed|
|Reference type|WeakReference for keys|
|Null keys allowed|✅|
|Use-case|Caching, canonical mappings|

---

## **✅ 236. How can you make a Collection class read-only in Java?**

  

Use **unmodifiable wrappers** from Collections utility class.

```
List<String> original = new ArrayList<>();
List<String> readOnly = Collections.unmodifiableList(original);
```

Similarly:

```
Set<String> readOnlySet = Collections.unmodifiableSet(originalSet);
Map<String, Integer> readOnlyMap = Collections.unmodifiableMap(originalMap);
```

> ✅ Throws UnsupportedOperationException on mutation attempts.

---

## **✅ 237. When is** 

## **UnsupportedOperationException**

##  **thrown in Java?**

  

This exception is thrown when a **modification method is called on an unmodifiable collection** or unsupported collection type.

  

### **💥 Example 1:**

```
List<String> readOnly = Collections.unmodifiableList(new ArrayList<>());
readOnly.add("fail"); // Throws UnsupportedOperationException
```

### **💥 Example 2:**

```
List<String> fixed = Arrays.asList("A", "B");
fixed.add("C"); // Throws UnsupportedOperationException
```



---

## **✅ 237. When is** 

## **UnsupportedOperationException**

##  **thrown in Java?**

  

UnsupportedOperationException is a **runtime exception** thrown when an operation is not supported by a collection implementation.

  

### **🔥 Common Scenarios:**

- **Unmodifiable collections** created by:
    

```
Collections.unmodifiableList(originalList);
```

-   
    
- **Fixed-size lists** like:
    

```
List<String> list = Arrays.asList("A", "B");
list.add("C"); // ❌ Throws UnsupportedOperationException
```

-   
    
- **Immutable collections** in Java 9+:
    

```
List<String> immutable = List.of("A", "B");
immutable.remove(0); // ❌ Unsupported
```

  

  

> ✅ Always check the documentation of the collection implementation before assuming it supports all operations.

---

## **✅ 238. How can we sort** Customer objects in an ArrayList by firstName ?

  

Assume the following class:

```
class Customer {
    private String firstName;
    // constructor, getter
    public String getFirstName() { return firstName; }
}
```

### **✅ Java 8+ (Lambda/Method Reference)**

```
list.sort(Comparator.comparing(Customer::getFirstName));
```

### **✅ Traditional Comparator**

```
Collections.sort(list, new Comparator<Customer>() {
    public int compare(Customer c1, Customer c2) {
        return c1.getFirstName().compareTo(c2.getFirstName());
    }
});
```

> ✅ Ensure firstName is non-null or add a null-safe comparator.

---

## **✅ 239. What is the difference between Synchronized Collection and Concurrent Collection?**

|**Feature**|**Synchronized Collection**|**Concurrent Collection**|
|---|---|---|
|Locking|Locks entire collection (coarse-grained)|Locking is fine-grained or lock-free|
|Performance|Slower under heavy concurrency|Optimized for concurrent access|
|Iteration|Must be manually synchronized|Weakly consistent, no exceptions|
|Examples|Collections.synchronizedList(...)|ConcurrentHashMap, CopyOnWriteArrayList|

> 🧠 **Synchronized** is good for low-concurrency apps. Use **Concurrent** in high-throughput, multithreaded environments.

---

## **✅ 240. What is the scenario to use** 

## **ConcurrentHashMap**

##  **in Java?**

  

ConcurrentHashMap is ideal when:

- You need **thread-safe Map** operations without global locking
    
- You expect **high read/write concurrency**
    
- You want **non-blocking reads** and **fast atomic updates**
    

  

### **🔥 Use Cases:**

- Caching (e.g., session cache)
    
- Counting (e.g., analytics metrics)
    
- Task coordination (e.g., work queues)
    

```
ConcurrentHashMap<String, Integer> map = new ConcurrentHashMap<>();
map.put("key", 1);
map.computeIfAbsent("newKey", k -> 100);
```

> ✅ It allows concurrent updates using compute(), merge(), putIfAbsent() with minimal locking.

---

## **✅ 241. How will you create an empty Map in Java?**

  

### **✅ Pre-Java 9:**

```
Map<String, String> emptyMap = new HashMap<>();
```

### **✅ Java 9+:**

```
Map<String, String> emptyMap = Map.of();
```

> 🧠 Map.of() returns an **immutable** empty map.

---

## **✅ 242. What is the difference between** 

## **remove()**

##  **in Collection vs Iterator?**

|**Method**|Collection.remove(Object o)|Iterator.remove()|
|---|---|---|
|Purpose|Removes object from collection|Removes current element during iteration|
|Thread-safe during iteration|❌ May throw ConcurrentModificationException|✅ Safe during iteration|
|When to use|Outside iteration context|During iteration|

### **🔥 Example:**

```
Iterator<String> it = list.iterator();
while (it.hasNext()) {
    if (it.next().equals("A")) {
        it.remove(); // ✅ Safe
    }
}
```

---

## **✅ 243. Array vs ArrayList — which is preferred for storing objects?**

|**Feature**|**Array**|**ArrayList**|
|---|---|---|
|Size|Fixed|Dynamic|
|Type safety|Works with both primitives & objects|Objects only|
|Flexibility|Low|High (resizable, supports many methods)|
|Performance|Slightly better for fixed-size data|Scales better with growth|

> ✅ Use **ArrayList** for most application logic unless you’re doing performance-critical low-level optimizations.

---

## **✅ 244. Is it possible to replace** 

## **Hashtable**

##  **with** 

## **ConcurrentHashMap**

## **?**

  

✅ Yes. In modern Java, ConcurrentHashMap is the recommended replacement for legacy Hashtable.

|**Feature**|Hashtable|ConcurrentHashMap|
|---|---|---|
|Thread-safety|Synchronized methods|Fine-grained concurrency|
|Performance|Poor under load|High throughput|
|Null keys/values|❌ Not allowed|❌ Nulls not allowed (key/value)|

> ✅ ConcurrentHashMap is non-blocking for reads and uses segment locks (Java 7) or CAS (Java 8+).

---

## **✅ 245. How is** CopyOnArrayList different from ArrayList and Vector ?

|**Feature**|ArrayList|Vector|CopyOnWriteArrayList|
|---|---|---|---|
|Thread-safe|❌ No|✅ Yes (synchronized)|✅ Yes (copy-on-write)|
|Write performance|Fast|Slower|Slow (copies array on every write)|
|Read performance|Fast|Medium|Very Fast (no locks)|
|Iteration|Fail-fast|Fail-fast|Fail-safe (no ConcurrentModificationException)|

> ✅ Best suited when reads are much more frequent than writes.

---

## **✅ 246. Why does** ListIterator have add() but iterator doesn't ?

- ListIterator is bidirectional and **supports structural modifications** like add() and set().
    
- Iterator is **unidirectional and read-only**, with only remove() allowed.
    

```
ListIterator<String> it = list.listIterator();
it.add("newElement"); // ✅ Valid
```

> 🧠 Iterator provides minimal API to reduce risk of modification during iteration.

---

## **✅ 247. Why do we sometimes get ConcurrentModificationException during iteration?**


Because a **fail-fast iterator** detects **structural modifications** to the collection after the iterator was created.

### **Example:**

```
for (String s : list) {
    list.add("new"); // ❌ throws ConcurrentModificationException
}
```

### **How to prevent:**

- Use Iterator.remove() instead of Collection.remove()
    
- Use concurrent collections like CopyOnWriteArrayList, ConcurrentHashMap
    
- Use Java 8 streams where safe
    

---

## **✅ 248. How to convert a** Map to a List ?

  

### **✅ Convert entries to list:**

```
List<Map.Entry<String, Integer>> entries = new ArrayList<>(map.entrySet());
```

### **✅ Convert keys or values:**

```
List<String> keys = new ArrayList<>(map.keySet());
List<Integer> values = new ArrayList<>(map.values());
```

> ✅ Java 8+:

```
List<String> keys = map.keySet().stream().collect(Collectors.toList());
```

---

## **✅ 249. How to create a Map with reverse view and lookup?**

  

Create a **bidirectional map** manually or use BiMap from **Guava**:

  

### **Manual reverse map:**

```
Map<String, Integer> original = Map.of("A", 1, "B", 2);
Map<Integer, String> reverse = new HashMap<>();
original.forEach((k, v) -> reverse.put(v, k));
```

### **Guava BiMap:**

```
BiMap<String, Integer> biMap = HashBiMap.create();
biMap.put("A", 1);
Integer value = biMap.get("A");
String key = biMap.inverse().get(1);
```

---

## **✅ 250. How will you create a** shallow copy of a Map ?
  

### **✅ Using constructor:**

```
Map<String, String> shallowCopy = new HashMap<>(originalMap);
```

> 🔍 Only the references to values are copied — not deep copies.

---

## **✅ 251. Why can’t we create a** generic array in java ?

  

Due to **type erasure**, the JVM can’t track the generic type at runtime. Java arrays are **reifiable**, but generics are not.

```
T[] array = new T[10]; // ❌ Compile error
```

Workaround:

```
@SuppressWarnings("unchecked")
T[] array = (T[]) new Object[10]; // ✅
```

> ✅ Generics and arrays don’t play well together because arrays enforce runtime type safety, but generics are erased at runtime.

---

## **✅ 252. What is a** PriorityQueue in java ?

  

A **heap-based data structure** that retrieves elements in **priority order** (natural or comparator-defined).

```
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.add(10);
pq.add(2);
System.out.println(pq.poll()); // 2
```

|**Feature**|**Value**|
|---|---|
|Order|Sorted by natural order (min-heap)|
|Null allowed|❌ No nulls|
|Thread-safe|❌ No|
|Backed by|Binary Heap|

> ✅ Use PriorityQueue for scheduling, greedy algorithms, or any use-case needing sorted order access.

---

## **✅ 253. What are the important points to remember about Java Collections?**

1. ✅ Always pick the right data structure (Map, Set, List) for your use case.
    
2. ✅ Prefer ArrayList for fast access, LinkedList for frequent insert/delete.
    
3. ✅ Use HashSet/HashMap for O(1) operations, TreeSet/TreeMap for sorted data.
    
4. ✅ Prefer ConcurrentHashMap over Hashtable.
    
5. ✅ Always use generics to avoid casting and ensure type safety.
    
6. ✅ Choose fail-safe collections when working in multi-threaded environments.
    
7. ✅ Be aware of **modification during iteration** and ConcurrentModificationException.
    
8. ✅ Use Collections.unmodifiableX() or Java 9+ List.of() for immutability.
    
9. ✅ Streams are powerful but must be used wisely to avoid performance penalties.
    



---

## **✅ 254. How can we pass a Collection as an argument to a method and ensure that the method will not modify it?**

  

Use **immutable or unmodifiable wrappers** to block mutation operations.

  

### **✅ Option 1:** 

### **Collections.unmodifiableXxx()**

```
List<String> list = new ArrayList<>();
processCollection(Collections.unmodifiableList(list));

void processCollection(List<String> readOnlyList) {
    readOnlyList.add("X"); // ❌ Throws UnsupportedOperationException
}
```

### **✅ Option 2: Java 9+ Factory Methods**

```
List<String> list = List.of("A", "B"); // Immutable list
```

> ✅ Best practice: expose only read-only views of collections in APIs.

---

## **✅ 255. How does** HashMap work in java ?

  

A HashMap is a **hash table-based** implementation of the Map interface that stores key-value pairs with **O(1) average time complexity**.

  

### **⚙️ Internal Mechanics:**

1. Calls hashCode() on the key.
    
2. Applies hash(key) & (n - 1) to locate a **bucket index**.
    
3. Stores entries in a **linked list** or **balanced tree (Java 8+)** if hash collisions occur.
    
4. Uses equals() to check for key equality within the bucket.
    

```
Map<String, String> map = new HashMap<>();
map.put("A", "Apple");
```

### **✅ Java 8+ Tree Optimization:**

- If a bucket exceeds a threshold (≥ 8 entries), it’s converted to a **Red-Black Tree** for faster lookup.
    

  

> ✅ Resizes when size >= threshold = capacity * loadFactor (default 0.75)

---

## **✅ 256. How is** HashSet implemented in java ?
  

HashSet is backed internally by a HashMap.

```
Set<String> set = new HashSet<>();
```

Internally:

```
private transient HashMap<E, Object> map;
```

- Elements are stored as keys in the map.
    
- A dummy constant PRESENT is used as value.
    

  

### **✅ add() method:**

```
public boolean add(E e) {
    return map.put(e, PRESENT) == null;
}
```

> ✅ Guarantees **no duplicates**, fast O(1) average time for add, contains, and remove.

---

## **✅ 257. What is a** NavigableMap in java ?

  

NavigableMap is a **sorted map** that provides **navigation methods** to access elements relative to given keys.

  

### **✅ Key Features:**

- Subviews: headMap(), tailMap(), subMap()
    
- Navigation: lowerKey(), floorKey(), ceilingKey(), higherKey()
    
- Reverse traversal: descendingMap(), descendingKeySet()
    

```
NavigableMap<Integer, String> navMap = new TreeMap<>();
navMap.put(10, "A"); navMap.put(20, "B"); navMap.put(30, "C");

System.out.println(navMap.floorKey(25)); // 20
```

---

## **✅ 258. Difference between descendingKeySet() and descendingMap() ?


|**Method**|**Return Type**|**Description**|
|---|---|---|
|descendingKeySet()|NavigableSet<K>|Returns a set view of keys in reverse|
|descendingMap()|NavigableMap<K,V>|Returns a full reverse-ordered map|

### **Example:**

```
NavigableMap<Integer, String> map = new TreeMap<>();
map.put(1, "A"); map.put(2, "B");

map.descendingKeySet(); // [2, 1]
map.descendingMap();    // {2=B, 1=A}
```

---

## **✅ 259. What is the advantage of** NavigableMap over Map ?

### **🚀 Advantages:**

|**Feature**|Map|NavigableMap|
|---|---|---|
|Sorted keys|❌ No|✅ Yes (natural or custom comparator)|
|Range views|❌ No|✅ headMap(), tailMap(), subMap()|
|Navigation|❌ No|✅ floorKey(), ceilingKey(), etc.|
|Reverse traversal|❌ No|✅ descendingMap(), descendingKeySet()|

> ✅ Perfect for time-based events, range-based queries, and ordered access.

---

## **✅ 260. Difference between** headMap() , tailMap() and subMap() in NavigableMap 

|**Method**|**Returns keys**|**Example (map = [1=A, 2=B, 3=C, 4=D])**|
|---|---|---|
|headMap(K)|< K|headMap(3) → {1=A, 2=B}|
|tailMap(K)|>= K|tailMap(3) → {3=C, 4=D}|
|subMap(K1, K2)|>= K1 && < K2|subMap(2, 4) → {2=B, 3=C}|

> ✅ Overloaded versions allow inclusive/exclusive flags.

---

Absolutely, Akshita. Let’s break down and deeply answer each of these questions, making sure you’re conceptually strong and interview-ready. I’ll also mention variations, internal mechanisms, and best practices where needed.

---

### **✅** 

### **261. How will you sort objects by Natural order in a Java List?**

  

**✔️ Answer:**

To sort objects by their _natural order_, the class must implement the Comparable<T> interface and override the compareTo() method.

```
List<String> names = Arrays.asList("Charlie", "Alice", "Bob");
Collections.sort(names); // or names.sort(null); from Java 8 onwards
System.out.println(names); // [Alice, Bob, Charlie]
```

> ✅ Natural order is what is defined inside the compareTo() method of the object.

  

**If you have a custom object:**

```
class Employee implements Comparable<Employee> {
    String name;
    int age;

    public Employee(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public int compareTo(Employee other) {
        return this.age - other.age; // Natural order: by age
    }
}
```

```
List<Employee> employees = List.of(new Employee("A", 30), new Employee("B", 25));
List<Employee> sorted = new ArrayList<>(employees);
Collections.sort(sorted); // uses compareTo
```

**🧠 Deep Tip:**

- Use List.sort(null) or Collections.sort(list) for natural ordering.
    
- Java 8’s list.sort(Comparator.naturalOrder()) also works if the element is Comparable.
    

---

### **✅** 

### **262. How can we get a Stream from a List in Java?**

  

**✔️ Answer:**

In Java 8+, every Collection interface (like List) has a .stream() method:

```
List<String> names = List.of("Alice", "Bob", "Charlie");
Stream<String> stream = names.stream();
```

**Variants:**

- stream() → Sequential stream
    
- parallelStream() → Parallel stream for multithreaded processing
    

  

**Why use Streams?**

To perform declarative operations like filter, map, reduce, sort, collect, etc.

```
List<String> filtered = names.stream()
                             .filter(name -> name.startsWith("A"))
                             .collect(Collectors.toList());
```

**🧠 Deep Tip:**

- Streams are **lazy** — nothing happens until a terminal operation is called (like collect(), count(), forEach()).
    
- Don’t reuse a stream once a terminal operation has been called on it — it becomes closed.
    

---

### **✅** 

### **263. Can we get a Map from a Stream in Java?**

  

**✔️ Answer:**

Yes. You can convert a Stream<T> into a Map<K, V> using the Collectors.toMap() collector.

  

Example:

```
List<Employee> list = List.of(new Employee("A", 30), new Employee("B", 25));
Map<String, Integer> nameToAge = list.stream()
    .collect(Collectors.toMap(e -> e.name, e -> e.age));
```

**Be careful of duplicate keys!**

  

If keys can repeat, pass a merge function:

```
.collect(Collectors.toMap(
    e -> e.name,
    e -> e.age,
    (age1, age2) -> age1  // or some logic to resolve duplicates
))
```

**To convert a stream of entries:**

```
Map<String, Integer> map = Stream.of(Map.entry("A", 1), Map.entry("B", 2))
    .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue));
```

**🧠 Deep Tip:**

- Prefer LinkedHashMap::new as a 4th parameter to preserve insertion order:
    

```
.collect(Collectors.toMap(
    e -> e.name,
    e -> e.age,
    (a, b) -> a,
    LinkedHashMap::new
));
```

---

### **✅** 

### **264. What are the popular implementations of Deque in Java?**

  

**✔️ Answer:**

Deque (Double Ended Queue) is a linear collection that supports **insertion and removal from both ends**.

  

📌 Java provides the following key implementations of Deque<E>:

  

#### **✅** 

#### **1. ArrayDeque**

- Backed by a **resizable array**
    
- **Faster than LinkedList** for stack/queue operations
    
- **Not thread-safe**
    
- No capacity restrictions (doubles in size when full)
    

```
Deque<String> deque = new ArrayDeque<>();
deque.addFirst("A");
deque.addLast("B");
```

#### **✅** 

#### **2. LinkedList**

- Implements both List and Deque
    
- Backed by a **doubly-linked list**
    
- More memory overhead (each node stores pointers)
    
- Can be used as a **queue**, **stack**, or **deque**
    

```
Deque<String> deque = new LinkedList<>();
deque.offerFirst("X");
deque.offerLast("Y");
```

#### **✅** 

#### **3. ConcurrentLinkedDeque**

- A **lock-free** thread-safe deque based on linked nodes
    
- Suitable for **high-concurrency environments**
    
- Available since Java 7
    

```
Deque<String> deque = new ConcurrentLinkedDeque<>();
```

---

### **✅ BONUS: Interview Tips & Must-Know Extras**

  

**🔸 Understand compareTo() vs Comparator:**

- Comparable: defines natural order
    
- Comparator: allows custom ordering externally
    

```
list.sort(Comparator.comparing(Employee::getName)); // custom sort
```

**🔸 Always handle duplicate keys in .toMap() to avoid IllegalStateException.**

  

**🔸 ArrayDeque is recommended over Stack class for LIFO use cases. Stack is legacy.**

  

**🔸 Deque is ideal when you need both queue and stack behavior in one structure.**

  

**🔸 Streams are for processing, not storing. Don’t use streams for side effects.**

---



---

## **✅** 

## **265. What is a Thread in Java?**

  

**✔️ Answer:**

A **thread** is a lightweight unit of execution within a process. In Java, threads allow concurrent execution of two or more parts of a program for maximum CPU utilization.

  

Java provides two ways to create a thread:

1. **Extend Thread class** and override run()
    
2. **Implement Runnable or Callable interface**
    

```
public class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is running");
    }
}
```

### **🔍 Internals:**

- Threads in Java are mapped to **native OS threads** (1:1 model)
    
- Java uses the **Thread Scheduler** to determine the order of thread execution
    

---

## **✅** 

## **266. What is the priority of a Thread and how is it used in scheduling?**

  

**✔️ Answer:**

Each Java thread has a **priority**, an integer between 1 (MIN_PRIORITY) and 10 (MAX_PRIORITY). It hints to the scheduler about the importance of a thread.

```
thread.setPriority(Thread.MAX_PRIORITY); // 10
```

### **⚠️ Important:**

- **Thread priorities are hints**, **not guarantees**.
    
- Thread scheduling is **OS-dependent** (preemptive on Windows, time-slicing on Linux)
    

---

## **✅** 

## **267. What is the default priority of a thread in Java?**

  

**✔️ Answer:**

```
Thread.NORM_PRIORITY // value is 5
```

Unless set explicitly, every thread inherits the priority of its **parent thread** (usually main thread with priority 5).

---

## **✅** 

## **268. What are the three different priorities that can be set on a Thread in Java?**

```
Thread.MIN_PRIORITY  = 1
Thread.NORM_PRIORITY = 5
Thread.MAX_PRIORITY  = 10
```

You can set any priority between 1 to 10, but these three are most commonly used constants.

---

## **✅** 

## **269. What is the purpose of join() method in Thread class?**

  

**✔️ Answer:**

join() tells the current thread to **wait** until the thread on which it is called **completes its execution**.

```
Thread t = new Thread(() -> {
    System.out.println("Child thread");
});
t.start();
t.join(); // Main waits for t to finish
System.out.println("Main continues...");
```

### **💡 Real-world use:**

  

Used when you want to ensure that one thread finishes before another starts — e.g., loading configuration before server start.

---

## **✅** 

## **270. What is the fundamental difference between wait() and sleep() methods?**

|**Feature**|sleep()|wait()|
|---|---|---|
|Belongs to|Thread class|Object class|
|Lock release|**Does NOT** release lock|**Releases** the object’s lock|
|Used for|Pausing thread for given time|Thread communication (sync)|
|Must be in sync block|❌ No|✅ Yes (synchronized)|
|Throws|InterruptedException|InterruptedException|

```
Thread.sleep(1000); // pauses for 1s

synchronized(obj) {
    obj.wait(); // releases lock and waits
}
```

> 🧠 sleep() is for delay; wait() is for thread coordination.

---

## **✅** 

## **271. Is it possible to call run() method instead of start() on a thread in Java?**

  

**✔️ Answer:**

Yes, you **can** call run() directly, but **it won’t start a new thread**. It will execute the run() method in the **current thread**, just like a normal method call.

```
MyThread t = new MyThread();
t.run(); // executes on main thread, not a new one
```

> ✅ Only start() creates a new call stack (thread). Interviewers love to test this.

---

## **✅** 

## **272. What is a Daemon thread in Java?**

  

**✔️ Answer:**

A **daemon thread** is a background thread that runs in support of user threads — like the garbage collector.

- JVM **exits when only daemon threads remain**.
    
- They should not perform critical tasks like writing to a database.
    

```
Thread t = new Thread(() -> {
    while(true) { System.out.println("Daemon running..."); }
});
t.setDaemon(true);
t.start();
```

> 🧠 JVM doesn’t wait for daemon threads to finish.

---

## **✅** 

## **273. How can we make a regular thread a Daemon thread in Java?**

  

**✔️ Answer:**

Use setDaemon(true) **before** the thread is started.

```
Thread t = new Thread(() -> { /* ... */ });
t.setDaemon(true);
t.start();
```

> ⚠️ You **cannot set daemon status after the thread is started** — throws IllegalThreadStateException.

---

## **✅** 

## **274. How will you make a user thread into daemon thread if it has already started?**

  

**✔️ Answer:**

You **cannot**. Once a thread is started, its daemon status **cannot be changed**.

```
t.start();
t.setDaemon(true); // ❌ IllegalThreadStateException
```

If you need a daemon thread, you **must set it before** calling start().

---

## **🎯 Deep Interview-Ready Nuggets**

- A **thread can die naturally**, via return, or throwing an uncaught exception.
    
- Thread.yield() is a hint to the scheduler to pause and let other threads run (not guaranteed).
    
- ExecutorService (from Java 5+) is the preferred way of managing threads (scalable and robust).
    
- A thread’s state can be checked via getState() → NEW, RUNNABLE, BLOCKED, WAITING, TIMED_WAITING, TERMINATED.
    

---





---

# **🧵 Advanced Multithreading in Java (Q275–290)**

---

## **✅ 275. Can we start a thread two times in Java?**

  

**No**, a thread can only be started **once**. If you call start() again after it has already started or completed, a java.lang.IllegalThreadStateException will be thrown.

```
Thread t = new Thread();
t.start(); // ✅ OK
t.start(); // ❌ IllegalThreadStateException
```

---

## **✅ 276. What is a Shutdown hook in Java?**

  

A **shutdown hook** is a special thread that is executed **just before the JVM shuts down**.

```
Runtime.getRuntime().addShutdownHook(new Thread(() -> {
    System.out.println("Cleanup before shutdown...");
}));
```

🔸 Useful for:

- Saving logs
    
- Closing DB connections
    
- Releasing resources
    

---

## **✅ 277. What is synchronization in Java?**

  

**Synchronization** is a mechanism to control access to shared resources by multiple threads. It prevents **race conditions** and ensures **thread safety**.

```
synchronized void criticalSection() {
    // Only one thread can execute this at a time
}
```

---

## **✅ 278. What is the purpose of Synchronized block in Java?**

  

A **synchronized block** provides **fine-grained control** over synchronization. Instead of locking the entire method, we can lock **only the necessary section**.

```
void update() {
    synchronized(this) {
        // Critical section
    }
}
```

🔹 Reduces lock contention and improves performance.

---

## **✅ 279. What is static synchronization?**

  

**Static synchronization** locks on the **class object**, not an instance.

```
synchronized static void log() {
    // Lock is on MyClass.class
}
```

🔹 Useful when you want to synchronize **across all instances** of a class.

---

## **✅ 280. What is a Deadlock situation?**

  

A **deadlock** occurs when two or more threads are waiting **forever** for each other to release resources, leading to a blocked system.

  

### **🔄 Example:**

```
Thread 1: locks A → waits for B  
Thread 2: locks B → waits for A
```

### **🔥 Avoid deadlocks by:**

- Acquiring locks in a consistent order
    
- Using timeout for locks
    
- Using higher-level concurrency tools (ReentrantLock, etc.)
    

---

## **✅ 281. What is the meaning of concurrency?**

  

**Concurrency** is the ability of a system to execute **multiple tasks (threads)** at the same time, either truly in parallel (multi-core) or by **context switching**.

  

> 💡 All parallel systems are concurrent, but not all concurrent systems are parallel.

---

## **✅ 282. What is the main difference between process and thread?**

|**Feature**|**Process**|**Thread**|
|---|---|---|
|Memory|Has its own memory space|Shares memory with other threads|
|Overhead|High (heavyweight)|Low (lightweight)|
|Communication|Through IPC (slower)|Shared memory (faster)|
|Crash Impact|One process crash doesn’t affect others|A thread crash can affect the process|

---

## **✅ 283. What is a process and thread in the context of Java?**

- **Process**: A Java program running in the JVM is a process.
    
- **Thread**: A unit of execution within that process. Multiple threads can exist in a single Java program sharing the same heap memory.
    

---

## **✅ 284. What is a Scheduler?**

  

The **Thread Scheduler** is part of the JVM and OS that **decides which thread to run next**. It’s **non-deterministic** and can’t be controlled directly from Java.

  

> 🧠 Priorities are hints; actual behavior is OS-dependent.

---

## **✅ 285. What is the minimum number of threads in a Java program?**

  

At least **two**:

1. **Main thread**
    
2. **Garbage Collector (Daemon)**
    

  

More may exist (e.g., Finalizer thread, Signal Dispatcher), but main + GC is the bare minimum.

---

## **✅ 286. What are the properties of a Java thread?**

- **Name**: Thread.getName()
    
- **ID**: Unique identifier
    
- **Priority**: Between 1–10
    
- **Daemon Status**: Background or user thread
    
- **State**: NEW, RUNNABLE, etc.
    
- **UncaughtExceptionHandler**
    

```
Thread t = new Thread();
t.setName("Worker-1");
t.setPriority(Thread.MAX_PRIORITY);
```

---

## **✅ 287. What are the different states of a Thread in Java?**

```
| State           | Description                                             |
|----------------|---------------------------------------------------------|
| NEW             | Thread is created but not started                      |
| RUNNABLE        | Eligible to run (might be running or waiting to run)   |
| BLOCKED         | Waiting to acquire a lock                              |
| WAITING         | Waiting indefinitely for another thread (e.g. join)    |
| TIMED_WAITING   | Waiting for specified time (e.g. sleep, join with timeout) |
| TERMINATED      | Finished execution                                     |
```

```
Thread.State state = thread.getState();
```

---

## **✅ 288. How will you set the priority of a thread in Java?**

```
Thread t = new Thread();
t.setPriority(Thread.MAX_PRIORITY); // 10
```

🔹 Values:

- Thread.MIN_PRIORITY = 1
    
- Thread.NORM_PRIORITY = 5 (default)
    
- Thread.MAX_PRIORITY = 10
    

  

⚠️ **Thread priorities may be ignored** by the OS scheduler.

---

## **✅ 289. What is the purpose of Thread Groups in Java?**

  

ThreadGroup is a way to group multiple threads for:

- Collective interruption
    
- Priority management
    
- Monitoring
    

```
ThreadGroup group = new ThreadGroup("Workers");
Thread t1 = new Thread(group, task1);
Thread t2 = new Thread(group, task2);
```

⚠️ ThreadGroup is **legacy**; not commonly used in modern Java (use ExecutorService instead).

---

## **✅ 290. Why we should not stop a thread by calling its** 

## **stop()**

##  **method?**

  

Thread.stop() is **unsafe and deprecated** because it:

- **Forcibly terminates** a thread without giving it a chance to release resources
    
- Can leave shared objects in **inconsistent state**
    

  

### **✅ Safe alternative:**

  

Use a **flag**:

```
volatile boolean running = true;

public void run() {
    while (running) {
        // work
    }
}
public void stopThread() {
    running = false;
}
```

---

### **🧠 Final Pro Interview Tips:**

- Always understand **why** something is dangerous (e.g., stop()), not just that it is.
    
- Understand the **life cycle** of a thread and thread-safe design patterns.
    
- For modern multithreading, learn ExecutorService, ForkJoinPool, CompletableFuture.
    





---

## **✅ 275.** 

## **Can we start a thread two times in Java?**

  

**No**, a thread can only be started once. Attempting to call start() on a thread that has already been started or finished will result in a java.lang.IllegalThreadStateException.

  

### **🔍 Why?**

  

When start() is called:

- The JVM creates a new **call stack** for the thread.
    
- That thread enters the **Runnable** state and eventually starts executing the run() method.
    

  

Once terminated, the thread object is **not reusable**.

  

### **🧠 Interview Trap:**

  

Calling run() multiple times is legal because it’s just a method. But that won’t create a new thread.

```
Thread t = new Thread(() -> System.out.println("Hello"));
t.start(); // ✅ Creates new thread
t.start(); // ❌ IllegalThreadStateException
```

---

## **✅ 276.** 

## **What is a Shutdown hook in Java?**

  

A **shutdown hook** is a special thread that the JVM invokes during:

- System.exit()
    
- Ctrl+C (SIGINT)
    
- JVM shutdown (not kill -9)
    

```
Runtime.getRuntime().addShutdownHook(new Thread(() -> {
    System.out.println("Cleaning up resources...");
}));
```

### **🔍 Use cases:**

- Flushing logs
    
- Closing DB connections
    
- Notifying external systems
    

  

### **🧠 JVM internals:**

- Shutdown hooks are executed in **parallel**, not sequentially.
    
- You can register multiple hooks.
    
- Hooks can **delay shutdown**, but not **prevent** it.
    

---

## **✅ 277.** 

## **What is synchronization in Java?**

  

Synchronization is a **mutual exclusion mechanism** to ensure only **one thread** at a time can access a **critical section** — usually involving shared resources.

```
synchronized void updateSharedCounter() {
    counter++;
}
```

### **🔍 What happens behind the scenes?**

- A **monitor lock** (intrinsic lock) is acquired on the object (this or class).
    
- Other threads trying to access the synchronized block/method are **blocked**.
    

  

### **🔐 Types of synchronization:**

- **Method-level**: Lock on this (instance) or Class (static)
    
- **Block-level**: Lock on a custom object for better granularity
    

---

## **✅ 278.** 

## **What is the purpose of synchronized block in Java?**

  

The synchronized block lets you **fine-tune synchronization scope**. Instead of locking the whole method, only protect the section of code that needs atomicity.

```
void update() {
    // non-critical logic
    synchronized (lock) {
        // critical section
    }
}
```

### **🔍 Benefits:**

- **Improves concurrency** by reducing lock contention.
    
- Allows **multiple locks** in different parts of the object/class.
    

  

### **🧠 Real-World Example:**

  

Used when only part of the method deals with shared resources (e.g., a cache or shared counter).

---

## **✅ 279.** 

## **What is static synchronization?**

  

When you synchronize a **static method**, the lock is acquired on the **Class object**, not an instance.

```
synchronized static void logEvent() {
    // lock acquired on MyClass.class
}
```

### **🧠 Internals:**

- Useful when shared data is **static** and must be synchronized across **all instances**.
    
- Only one thread across **all instances** can execute the static synchronized block at a time.
    

---

## **✅ 280.** 

## **What is a Deadlock situation?**

  

A **deadlock** occurs when two or more threads are blocked forever, each waiting on the **lock held by the other**.

  

### **🧶 Example:**

```
Thread-1: locks Resource A, waits for B  
Thread-2: locks Resource B, waits for A
```

### **🔍 Conditions for Deadlock (Coffman’s):**

1. Mutual exclusion
    
2. Hold and wait
    
3. No preemption
    
4. Circular wait
    

  

### **🔥 Prevention strategies:**

- Acquire locks in a fixed order
    
- Use tryLock() with timeout
    
- Use **lock hierarchy**
    
- Apply **deadlock detection algorithms** in real-time systems
    

---

## **✅ 281.** 

## **What is the meaning of concurrency?**

  

**Concurrency** = Multiple tasks **in progress**, possibly overlapping (e.g., interleaved execution on a single core via context switching).

  

It contrasts with **parallelism**, which is **truly simultaneous execution** (multi-core CPU).

  

### **🧠 Key Insight:**

  

Concurrency is a **design pattern**, parallelism is a **hardware execution detail**.

---

## **✅ 282.** 

## **What is the main difference between process and thread?**

|**Feature**|**Process**|**Thread**|
|---|---|---|
|Memory|Own address space|Shares process memory|
|Creation|Expensive|Lightweight|
|Communication|IPC, sockets|Shared variables, faster|
|Failure Impact|Doesn’t affect other processes|May affect entire process|
|Scheduling Unit|OS-level|Subunit of a process|

---

## **✅ 283.** 

## **What is a process and thread in the context of Java?**

- A **process** is a **running instance of a Java application** with its own JVM, heap, and stack.
    
- A **thread** is an **independent path of execution** within the same Java process. All threads share:
    
    - Heap memory (objects, class metadata)
        
    - Static data
        
    

  

But each thread has:

- Its own **call stack**, **program counter**, and **local variables**
    

---

## **✅ 284.** 

## **What is a Scheduler?**

  

The **Thread Scheduler** is part of the JVM + OS that determines **which thread gets CPU time** and in what order.

  

### **🔍 Scheduling types:**

- **Preemptive**: OS forcibly suspends threads
    
- **Time-sliced**: Each thread gets a time slice (quantum)
    

  

> JVM does **not guarantee fairness or ordering**, only attempts it via **priorities**.

---

## **✅ 285.** 

## **What is the minimum number of Threads in a Java program?**

  

At least **2**:

1. **Main Thread** – runs your main() method
    
2. **Garbage Collector** – a background daemon
    

  

Other JVM internal threads:

- Finalizer
    
- Signal Dispatcher
    
- Reference Handler
    
- Compiler (in HotSpot)
    

---

## **✅ 286.** 

## **What are the properties of a Java thread?**

  

Each thread in Java has the following attributes:

|**Property**|**Example**|
|---|---|
|Name|"main", "worker-1"|
|ID|Thread.getId()|
|Priority|1–10 (Thread.MIN_PRIORITY to MAX_PRIORITY)|
|Daemon status|isDaemon()|
|State|NEW, RUNNABLE, BLOCKED, etc.|
|Uncaught handler|Handles uncaught exceptions|

```
Thread t = new Thread(() -> {});
t.setName("Worker");
t.setPriority(Thread.MAX_PRIORITY);
t.setDaemon(true);
```

---

## **✅ 287.** 

## **What are the different states of a Thread in Java?**

  

Java Thread.State enum defines 6 possible states:

|**State**|**Description**|
|---|---|
|NEW|Thread created but not started|
|RUNNABLE|Eligible to run, waiting for CPU|
|BLOCKED|Waiting for lock on an object (e.g., synchronized)|
|WAITING|Waiting indefinitely (e.g., join(), wait())|
|TIMED_WAITING|Waiting for a period (e.g., sleep(), join(timeout))|
|TERMINATED|Completed execution or exited due to exception|

---

## **✅ 288.** 

## **How will you set the priority of a thread in Java?**

  

Use:

```
thread.setPriority(Thread.MAX_PRIORITY); // 10
```

### **🎯 Ranges:**

- MIN_PRIORITY = 1
    
- NORM_PRIORITY = 5 (default)
    
- MAX_PRIORITY = 10
    

  

**OS and JVM may ignore priorities**, especially in modern multi-core systems.

---

## **✅ 289.** 

## **What is the purpose of Thread Groups in Java?**

  

ThreadGroup is used to:

- Organize threads hierarchically
    
- Perform group-level actions (e.g., interrupt, enumerate)
    
- Set max priority at group level
    

```
ThreadGroup group = new ThreadGroup("ServiceGroup");
Thread t1 = new Thread(group, task1);
```

> ⚠️ **Deprecated in modern designs**. Use **Executors** and **ThreadPoolExecutor** instead.

---

## **✅ 290.** 

## **Why we should not stop a thread by calling its stop() method?**

  

Because Thread.stop() is:

- **Unsafe**
    
- **Deprecated since Java 1.2**
    
- Terminates a thread **without cleanup**, possibly while holding locks
    

  

### **🔥 Consequences:**

- Shared resources may be left in an inconsistent state
    
- Deadlocks or data corruption can occur
    

  

### **✅ Safe alternative:**

  

Use a **volatile flag**:

```
volatile boolean running = true;

public void run() {
    while (running) {
        // safe work
    }
}

public void shutdown() {
    running = false;
}
```



## **✅ 291.** 

## **How will you create a Thread in Java?**

  

You can create a thread in 3 standard ways:

  

### **🔹 1.** 

### **Extend Thread class**

```
class MyThread extends Thread {
    public void run() {
        System.out.println("Running");
    }
}
new MyThread().start();
```

### **🔹 2.** 

### **Implement Runnable (preferred for reusability)**

```
Runnable task = () -> System.out.println("Runnable running");
new Thread(task).start();
```

### **🔹 3.** 

### **Implement Callable + Future (if result is needed)**

```
Callable<String> task = () -> "result";
Future<String> future = Executors.newSingleThreadExecutor().submit(task);
```

### **🧠 Key Insight:**

- Use **Runnable** for fire-and-forget
    
- Use **Callable** when you need a **return value** or **checked exception**
    

---

## **✅ 292.** 

## **How can we stop a thread in the middle of execution in Java?**

  

### **❌ Don’t use** 

### **Thread.stop()**

###  **→ it is unsafe and deprecated**

  

### **✅ Preferred way: Use an** 

### **interruption flag**

```
class Task implements Runnable {
    public void run() {
        while (!Thread.currentThread().isInterrupted()) {
            // Do work
        }
    }
}
```

Then interrupt the thread externally:

```
Thread t = new Thread(new Task());
t.start();
t.interrupt(); // sets the interrupt flag
```

> 🔥 Use isInterrupted() to check the flag, **never forcefully stop a thread**.

---

## **✅ 293.** 

## **How do you access the current thread in a Java program?**

  

Use:

```
Thread current = Thread.currentThread();
System.out.println("Running in: " + current.getName());
```

Useful for:

- Debugging
    
- Logging
    
- Managing thread-specific actions
    

---

## **✅ 294.** 

## **What is Busy waiting in Multi-threading?**

  

Busy waiting is when a thread **keeps checking a condition in a loop** (spin-wait), consuming CPU cycles **without yielding or sleeping**.

```
while (!conditionMet) {
    // Busy wait: wastes CPU
}
```

### **🧠 Why bad?**

- Increases CPU usage
    
- Causes contention
    
- Not scalable
    

---

## **✅ 295.** 

## **How can we prevent busy waiting in Java?**

  

Use **blocking constructs** instead:

  

### **🔹 1.** 

### **Object.wait() + notify()**

```
synchronized(lock) {
    while (!condition) lock.wait();
}
```

### **🔹 2.** 

### **Lock + Condition.await()**

```
lock.lock();
while (!condition) {
    condition.await();
}
```

### **🔹 3.** 

### **Higher-level utilities**

- BlockingQueue.take()
    
- CountDownLatch.await()
    
- Semaphore.acquire()
    
- CyclicBarrier.await()
    

  

These **block efficiently** without burning CPU.

---

## **✅ 296.** 

## **Can we use Thread.sleep() method for real-time processing in Java?**

  

**No**, Thread.sleep() is **not reliable for precise real-time timing**.

  

### **Why?**

- It causes the thread to pause **for at least** the specified time.
    
- Accuracy is limited by **OS scheduler granularity**.
    
- JVM and GC may add delays.
    

  

### **🧠 Use cases:**

- Good for throttling or simulating delay
    
- Not suitable for real-time systems (e.g., audio/video sync)
    

  

> For real-time Java systems, use **ScheduledExecutorService** or specialized real-time JVMs (like JamaicaVM, RTSJ).

---

## **✅ 297.** 

## **Can we wake up a thread that has been put to sleep by using Thread.sleep() method?**

  

**No**, a thread sleeping via Thread.sleep() **cannot be woken up externally**, except via **interruption**.

```
Thread.sleep(5000); // can only be interrupted
```

If interrupted:

```
try {
    Thread.sleep(5000);
} catch (InterruptedException e) {
    System.out.println("Interrupted during sleep");
}
```

> ⚠️ You must handle the InterruptedException, or the thread will exit.

---

## **✅ 298.** 

## **What are the two ways to check if a Thread has been interrupted?**

  

### **🔹 1.** 

### **Instance method (non-clearing):**

```
if (Thread.currentThread().isInterrupted()) {
    // Flag is still true
}
```

### **🔹 2.** 

### **Static method (clears flag):**

```
if (Thread.interrupted()) {
    // Flag is cleared automatically after call
}
```

### **🔍 Difference:**

- isInterrupted() → just checks the flag.
    
- interrupted() → **checks and resets** the interrupt flag.
    

---

## **✅ 299.** 

## **How can we make sure that Parent thread waits for termination of Child thread?**

  

Use the **join()** method.

```
Thread child = new Thread(() -> {
    // Do something
});
child.start();
child.join(); // Main thread will wait for child to finish
```

### **🔍 Variants:**

```
child.join();        // Waits indefinitely
child.join(3000);    // Waits up to 3 seconds
```

> 💡 Used to maintain **deterministic execution order**, especially in **unit tests** or **batch jobs**.

---

## **✅ 300.** 

## **How will you handle InterruptedException in Java?**

  

### **🔹 Best Practice:** 

### **Propagate or handle carefully**

```
try {
    Thread.sleep(1000);
} catch (InterruptedException e) {
    // Restore interrupt flag if not handled
    Thread.currentThread().interrupt();
    // Optionally log or throw further
}
```

### **🧠 Why restore the interrupt?**

- Some higher-level methods (e.g. Executor, BlockingQueue) rely on the flag.
    
- Silently eating the exception can cause threads to run when they should exit.
    

  

> ⚠️ Never swallow InterruptedException unless you have a **very good reason**.

---

## **🔚 Final Notes**

|**Best Practice**|**Why it matters**|
|---|---|
|Use interrupt() for stopping|Safer, graceful shutdown|
|Avoid busy-waiting|Wastes CPU|
|Prefer join() over polling|More predictable, efficient|
|Restore interrupted status|Ensures proper propagation of interruption|
|Use ExecutorService for thread mgmt|Manages lifecycle and pooling better|

---



---

