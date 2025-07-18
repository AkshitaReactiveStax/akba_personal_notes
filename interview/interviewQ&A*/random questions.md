
#### 1**What is the difference between a `HashMap` and a `TreeMap` in Java?*
- **Answer**:
    - **HashMap** is an implementation of the `Map` interface, and it uses a hash table for storage. It does not guarantee the order of the elements.
    - **TreeMap** is a `Map` that uses a red-black tree structure, so it stores the elements in a sorted order according to their natural ordering or by a custom comparator.

#### 2 **What are Java Collections? Can you name some of the main collections and their uses?**

- **Answer**: Java Collections refer to a framework that provides various classes and interfaces for storing and manipulating data. Some of the main collections are:
    - **List** (e.g., `ArrayList`, `LinkedList`) – Ordered collections that allow duplicates.
    - **Set** (e.g., `HashSet`, `TreeSet`) – Unordered collections that do not allow duplicates.
    - **Map** (e.g., `HashMap`, `TreeMap`) – Key-value pairs, where each key is unique.
    - **Queue** (e.g., `LinkedList`, `PriorityQueue`) – Collections used for holding elements prior to processing, typically in a FIFO (First-In-First-Out) order.

#### 3. **What is the difference between `String`, `StringBuilder`, and `StringBuffer` in Java?**

- **Answer**:
    - **String** is immutable, meaning its value cannot be changed after it's created. Every modification creates a new string object.
    - **StringBuilder** is mutable and designed for single-threaded use, providing efficient modification of strings.
    - **StringBuffer** is also mutable but is thread-safe, making it suitable for multi-threaded environments, though slightly less efficient than `StringBuilder`.

#### 4. **What are Java Streams and what are some benefits of using them?**

- **Answer**: Java Streams are part of the `java.util.stream` package and allow for functional-style operations on collections of data. Some benefits include:
    - **Concise code** – Streams allow you to perform operations like filtering, mapping, and reducing in a more declarative way.
    - **Parallel processing** – Streams support parallel operations, which can be useful for performance on large datasets.
    - **Lazy evaluation** – Operations on streams are lazy, meaning they are not executed until a terminal operation (like `collect()` or `forEach()`) is invoked.

#### 5. **Can you explain what a `deadlock` is in Java and how it can be avoided?**

- **Answer**:
    - A **deadlock** occurs when two or more threads are blocked forever because they are waiting for each other to release a resource. This can happen if two threads hold locks and wait for the other to release a lock.
    - **Avoidance**: You can avoid deadlocks by using proper synchronization, always locking resources in the same order, or using higher-level concurrency utilities from the `java.util.concurrent` package.

#### 6. **What is the difference between `synchronized` and `volatile` in Java?**

- **Answer**:
    - **synchronized** is used to control access to a block of code or an object, ensuring that only one thread can access it at a time.
    - **volatile** ensures that a variable's value is always read from and written to the main memory, which helps with visibility of variables across threads.

#### 7. **What are the differences between a `try-catch` block and a `throws` declaration in Java?**

- **Answer**:
    - A **try-catch** block is used to handle exceptions within the code by catching and responding to exceptions as they occur.
    - **throws** is used in a method declaration to indicate that the method can throw a particular exception and leaves it up to the caller of the method to handle it.

#### 8. **What is the purpose of the `final` keyword in Java?**

- **Answer**: The `final` keyword is used to:
    - **Final variable**: Makes the variable’s value constant (it cannot be reassigned).
    - **Final method**: Prevents the method from being overridden.
    - **Final class**: Prevents the class from being subclassed.

#### 9. **What is garbage collection in Java? How does it work?**

- **Answer**:
    - **Garbage collection** is the process of automatically freeing up memory by reclaiming objects that are no longer in use. The Java Virtual Machine (JVM) runs the garbage collector, which identifies and removes unreferenced objects from memory.


#interviewquestions about servlets :
https://medium.com/edureka/servlet-interview-questions-266b8fbb4b2d

#interviewquestions 
https://medium.com/edureka/java-interview-questions-1d59b9c53973
this link includes a lot of interview questions regarding core java , spring , servlets , jsp 

#interviewquestions about collections :
https://medium.com/edureka/java-collections-interview-questions-6d20f552773e

#interviewquestions about hibernate :
https://medium.com/edureka/hibernate-interview-questions-78b45ec5cce8

#interviewquestions about Destructor :
https://medium.com/edureka/destructor-in-java-21cc46ed48fc

#interviewquestions about MVC pattern :
https://medium.com/edureka/mvc-interview-questions-cd568f6d7c2e

#interviewquestions how to avoid deadlock :
https://medium.com/edureka/deadlock-in-java-5d1e4f0338d5


Sping boot features over spring framework :


Spring Boot is a framework designed to simplify the development of Spring applications by reducing boilerplate code, configuration, and setup. It comes with several **flagship features** out of the box that differentiate it from traditional Spring Framework. Here are **6 to 8 key features** that Spring Boot provides:

### 1. **Auto-Configuration:**
   - **Spring Boot** automatically configures your application based on the dependencies in your classpath. For example, if you include `spring-boot-starter-web`, Spring Boot auto-configures a web application, sets up a `DispatcherServlet`, and configures embedded servers (e.g., Tomcat, Jetty, or Undertow) without any manual configuration.
   - **Contrast with Spring**: In traditional Spring, you need to manually configure and specify various beans, components, and properties for common functionalities (e.g., data source, JPA, etc.).

### 2. **Standalone Applications (Embedded Servers):**
   - Spring Boot applications can run as **standalone Java applications**. It comes with embedded web servers (e.g., Tomcat, Jetty, or Undertow) which eliminates the need to deploy applications to an external application server.
   - **Contrast with Spring**: In traditional Spring applications, you need to deploy the application to an external server like Tomcat or WildFly.

### 3. **Spring Boot Starters:**
   - **Spring Boot** provides a wide range of **pre-configured starters** (e.g., `spring-boot-starter-web`, `spring-boot-starter-data-jpa`, etc.) to easily add common functionalities to your application.
   - These starters encapsulate all the necessary dependencies and configuration settings for specific tasks.
   - **Contrast with Spring**: In traditional Spring, you need to manually manage dependencies for various functionalities, which often leads to complex build configurations.

### 4. **Production-Ready Features:**
   - Spring Boot includes several built-in features aimed at making applications **production-ready**. This includes:
     - **Actuator**: Provides built-in endpoints to monitor and manage your application (e.g., `/health`, `/metrics`, `/info`, etc.).
     - **Health Checks**: Automatically checks the health of the application and its components.
     - **Metrics**: Provides insights into application metrics like memory usage, CPU usage, request counts, etc.
   - **Contrast with Spring**: In traditional Spring, you would need to manually configure these features and integrate third-party tools to monitor, manage, and check the health of the application.

### 5. **Embedded and Configurable Logging:**
   - Spring Boot comes with **pre-configured logging** (using libraries like `Logback` or `Log4j2`) and sensible defaults for logging levels, file outputs, and log formats.
   - **Contrast with Spring**: In traditional Spring applications, you need to set up logging manually by configuring log frameworks like Logback or Log4j and writing the necessary configuration files.

### 6. **Opinionated Defaults:**
   - Spring Boot provides **opinionated defaults** that allow developers to focus on business logic instead of configuration. For example, Spring Boot automatically sets up sensible default configurations for common services, like database connections, message queues, security, etc.
   - **Contrast with Spring**: Traditional Spring requires explicit configuration for most settings, requiring more upfront work from the developer.

### 7. **Minimal Configuration:**
   - Spring Boot reduces the need for XML configuration or Java-based configuration setup. It leverages **convention over configuration** to minimize the setup required to get the application running.
   - **Contrast with Spring**: Traditional Spring requires significant configuration, either in XML or Java classes, to wire up beans and set up context.

### 8. **Command-Line Interface (CLI):**
   - Spring Boot provides a **Command-Line Interface (CLI)** to easily run Spring applications from the command line, execute Groovy scripts, and manage your project without needing an IDE.
   - **Contrast with Spring**: Traditional Spring does not offer a similar CLI out-of-the-box, making development tasks more manual.

---

### Summary:
Spring Boot simplifies the development process by providing out-of-the-box features such as auto-configuration, embedded servers, pre-configured starters, production-ready features, and more, making it much easier to get started and deploy applications compared to traditional Spring Framework. These features significantly reduce configuration and boilerplate code, improving productivity and reducing setup time.



#interviewquestions Difference between CPU, RAM, ROM , Cache, Disks
Sure! Here's a brief breakdown of the key differences between **Disk Storage** (HDD/SSD), **RAM**, **ROM**, **Cache**, and the role of the **CPU** in a computer system.

### 1. **Disk Storage (HDD and SSD)**
   - **Purpose**: Disk storage is used for **long-term** storage of data, files, applications, and the operating system. It retains data even when the computer is powered off.
   - **HDD (Hard Disk Drive)**: 
     - A traditional mechanical storage device.
     - Consists of spinning disks (platters) and a moving read/write head to access data.
     - Slower read/write speeds (compared to SSDs).
     - Prone to mechanical failure because of moving parts.
   - **SSD (Solid State Drive)**:
     - A newer, faster storage device.
     - Uses NAND flash memory (no moving parts).
     - Much faster read/write speeds than HDDs, improving boot times and application load times.
     - More durable because it lacks mechanical parts.
   - **Speed**: Both HDDs and SSDs are used for **persistent storage**, but SSDs are significantly faster than HDDs.

### 2. **RAM (Random Access Memory)**
   - **Purpose**: RAM is **temporary** or **volatile** memory that the CPU uses to store data that is actively being used or processed by running applications. It holds data and instructions that the CPU needs **immediately** while the computer is on.
   - **Volatility**: RAM is volatile, meaning it **loses its data** when the power is turned off.
   - **Speed**: RAM is much faster than both HDDs and SSDs. It is **directly accessible by the CPU**, which makes it essential for fast processing.
   - **Capacity**: RAM is typically smaller in capacity than disk storage but much faster. A typical laptop may have 8GB or 16GB of RAM, whereas disk storage can range from hundreds of gigabytes to several terabytes.

### 3. **ROM (Read-Only Memory)**
   - **Purpose**: ROM is non-volatile memory used to **store firmware** or **system-level instructions** that are needed to boot up the computer and perform essential functions.
   - **Volatility**: ROM retains its data even when the power is off (non-volatile).
   - **Speed**: ROM is typically slower than RAM but is **designed for storing data that doesn't change frequently**, like the BIOS or firmware.
   - **Capacity**: ROM is usually much smaller in size than both RAM and disk storage. It typically stores just the essential instructions for booting the system (like the BIOS in a PC).

### 4. **Cache Memory**
   - **Purpose**: Cache is a small, **high-speed memory** located directly on or near the CPU to store frequently accessed data or instructions. It helps speed up data retrieval by keeping copies of frequently used data closer to the CPU.
   - **Types of Cache**:
     - **L1 Cache**: Smallest and fastest cache, located directly on the CPU. It stores the most frequently accessed data.
     - **L2 Cache**: Larger and slightly slower than L1, it is also located on the CPU or just next to it.
     - **L3 Cache**: Even larger and slower than L2, it is shared among all CPU cores in multicore processors.
   - **Speed**: Cache is **faster than RAM** but much smaller in size. It’s used to avoid frequent access to slower main memory (RAM).
   - **Capacity**: Cache memory is very small, typically ranging from a few kilobytes (KB) for L1 to several megabytes (MB) for L3.

### 5. **CPU (Central Processing Unit)**
   - **Purpose**: The CPU is the **brain** of the computer. It executes instructions from programs, performs calculations, and manages data flow between different components of the system (like RAM, disk storage, and cache).
   - **Role**: It retrieves instructions from memory (RAM or cache), decodes them, and executes them. It works with other parts of the system to process data.
   - **Speed**: The CPU is **much faster** than both RAM and disk storage but requires data to be fetched from RAM or cache for efficient operation.
   - **How it works**: The CPU constantly communicates with memory (especially RAM and cache) and other parts of the system to carry out the operations necessary for running applications and the operating system.

---

### **Summary of the Differences**:

| **Component**          | **Purpose**                                      | **Speed**        | **Volatility**    | **Capacity**      | **Key Role**                                          |
|------------------------|--------------------------------------------------|------------------|-------------------|-------------------|------------------------------------------------------|
| **Disk Storage (HDD/SSD)** | Long-term storage (files, apps, OS)               | SSD > HDD        | Non-volatile      | Large (GBs to TBs) | Stores persistent data                              |
| **RAM**                | Temporary memory for active processes            | Very fast        | Volatile          | Moderate (GBs)     | Holds data actively used by CPU for fast access      |
| **ROM**                | Stores firmware/boot instructions                | Slow             | Non-volatile      | Small (KBs)        | Stores essential startup instructions (BIOS, etc.)  |
| **Cache**              | Fast memory for frequently accessed data         | Faster than RAM  | Volatile          | Small (KBs to MBs) | Speeds up data retrieval for CPU                    |
| **CPU**                | Executes instructions and processes data         | Very fast        | N/A               | N/A               | Executes programs and controls data flow            |

### **Where is the CPU in the picture?**
- The **CPU** is at the **center** of the system's processing. It interacts with **RAM**, **cache**, and **disk storage** to run applications, handle data, and process instructions.
  - **Cache** is the **closest** to the CPU to provide ultra-fast data access.
  - The **CPU** accesses data from **RAM** (for temporary data) and **disk storage** (for long-term data) as needed.

---

In summary:
- **RAM** provides fast, temporary storage for the CPU’s active processes.
- **Disk storage** (HDD/SSD) holds long-term data and files.
- **ROM** contains essential boot instructions.
- **Cache** stores frequently accessed data for fast retrieval by the CPU.
- **CPU** is the processor that runs programs, makes calculations, and manages data flow between components. 




#interviewquestions from citibank - what are the updates in Java 8
- what is Stream API in java? Flatmap vs map, Intermediate Functions in Streams
- Optional.orElse in Java
- how hashmap works internally? what are the changes has been done in Java 8 in hashmap?
- comparator vs comparable
- difference between Wait and join method
- difference between Callable and Runnable
- what is solid principles with examples?
- how can I switch from a Postgres DB to an Oracle DB in Hibernate. List the things I have to do?
- what is SQL injection and how can you prevent it?
- how to perform queries in MongoDB? Explain the SET Modifier in MongoDB?
- how to declare Global Exceptions in Springboot application?
- why to use @Transactional annotation what's the benefit?
- How do microservies communicate with each other
- key Challenges in Microservice Communication
- why is Kafka technology significant to use?
- explain the concept of Leader and Follower.
- what is the purpose of retention period in Kafka cluster?
- explain how to Tune Kafka for Optimal Performance.
  
  