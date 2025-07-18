•⁠  ⁠how do you do multi-threading in Java  
•⁠  ⁠⁠there is file processign job - how will you increase performance for it  
•⁠  ⁠⁠how do you launch threads -  a lof ot them  
•⁠  ⁠⁠how do you convey data to them  
•⁠  ⁠⁠how do they convey their results back to you  
•⁠  ⁠⁠ do they have to completely be done with their work before they can convey back to you/the caller or is there any other way to do it before  
•⁠  ⁠⁠talk about Futures/ and read about Completeable futures for interview readiness  
•⁠  ⁠⁠how do you achieve Thread Safety | how do you make a project with singleton beans and are able to serve 50 requests at the same time.  
•⁠  ⁠⁠what is the difference between concurrency and parallelism  
•⁠  ⁠⁠trassaction isoloation and propagation
- what are the updates in Java 8
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
  - **how does hashmap work internally**
- How is Arraylist implemented
- How do interfaces resolve multiple inheritance
- Equals and hashcode
- How is hash collision detected and resolved in Hashmap

citibank interview - ICG Risk group  

- abstract class vs interface
- how they do in case of multiple inheritance

- method in interface is by default - abstract or not abstract - wrongly said non-abstract

- abstract class vs final class  -

- hashmap vs concurrentHashMap

- non thread safe vs thread Safe  -- barely pass
- need to explain more

- time complexity of retrieving from hashmap

- its slower as compared to concurrent hashmap (WRONG)
- didn't say O(1)   -- FAIL

- time complexity of linkedlist

- of deleting an element -- FAIL

- java 7 features [diamond operator for type inference, fork join algorithm] - none mentioned
- java 8 features - all mentioned

- difference between marker interface and functional interface - not good

- any java 11 features - none mentioned
- Map vs flatMap - ok , ok
- pseducode for StudentMap to print all course names for each student

- Map<Integer,Student>

Gang of four design pattern  

- Builder pattern advantages
- Builder class returns itself
- Nested class or explicit class both are possible
- What about singleton pattern
    - Synchronized should be at block level
    - Not at method level
    - Critical section
        - Should be Synchronized
        - Reflection can be used to create the singleton in a thread safe way
- How are we serving 100s of requests with singletons serving the requests without getting blocked

- How Kafka improves performance
- Number of consumer groups has to be equal to partitions ??!!  WRONG
- It’s consumer instances that has to be equal to partitions - if we want to get full parallelism

- candidate has to be damn clean about - partition distribution between consumer instances and consumer groups

- Sql queries where employee Id in ()
    - whole sale credit team
    - Devendra wanjara
- Front end
- Backend

Microservices patterns (edited)

****, *INTERVIEW PREP*****GoF (Gang of Four) Design Patterns - Read and understand the design patterns from the patterns book1) Creational PatternFactory Method Pattern  
Abstract Factory Pattern  
Singleton Pattern  
Prototype Pattern  
Builder Pattern  
Object Pool Pattern2) Structural PatternAdapter Pattern  
Bridge Pattern  
Composite Pattern  
Decorator Pattern  
Facade Pattern  
proxy Pattern3) Behavioral PatternChain of Responsibility  
Command Pattern  
Observer Pattern  
State Pattern  
Strategy Pattern  
Template PatternMicroservices PatternsRead the microservices patterns here  
[https://microservices.io/patterns/microservices.html](https://microservices.io/patterns/microservices.html)Top 20 Java Interview Questions from Investment Banks  
[https://hackernoon.com/top-20-java-interview-questions-from-investment-banks-80a2c405802](https://hackernoon.com/top-20-java-interview-questions-from-investment-banks-80a2c405802)Read Thread, Concurrency, Collections, IO sections on this site  
[https://www.javamex.com/tutorials/synchronization_volatile.shtml#](https://www.javamex.com/tutorials/synchronization_volatile.shtml#)Read Java 8 book for Lambda, Streams and Completable Futures21 Essential Java Interview Questions and Answers  
[https://www.toptal.com/java/interview-questions](https://www.toptal.com/java/interview-questions)Java Interview Questions And Answers | Java Questions 2019  
[https://intellipaat.com/interview-question/java-interview-questions/](https://intellipaat.com/interview-question/java-interview-questions/)100+ Java Interview Questions And Answers For 2019 | Edureka  
[https://www.edureka.co/blog/interview-questions/java-interview-questions/#exception](https://www.edureka.co/blog/interview-questions/java-interview-questions/#exception)Top 50+ Core Java Interview Questions and Answers  
[https://www.softwaretestinghelp.com/core-java-interview-questions/](https://www.softwaretestinghelp.com/core-java-interview-questions/)Commonly Asked Java Programming Interview Questions | Set 2 - GeeksforGeeks  
[https://www.geeksforgeeks.org/commonly-asked-java-programming-interview-questions-set-2/](https://www.geeksforgeeks.org/commonly-asked-java-programming-interview-questions-set-2/)300 Core Java Interview Questions | OOPs interview questions - javatpoint  
[https://www.javatpoint.com/corejava-interview-questions](https://www.javatpoint.com/corejava-interview-questions)Java Interview Questions [UPDATE 2019] - CodinGame for Work  
[https://www.codingame.com/work/java-interview-questions/](https://www.codingame.com/work/java-interview-questions/)Top 100 Java Interview Questions with Answers  
[https://www.guru99.com/java-interview-questions-answers.html](https://www.guru99.com/java-interview-questions-answers.html)Core Java Interview Questions and Answers - JournalDev  
[https://www.journaldev.com/2366/core-java-interview-questions-and-answers](https://www.journaldev.com/2366/core-java-interview-questions-and-answers)Java Interview Questions - tutorialspoint  
[https://www.tutorialspoint.com/java/java_interview_questions.htm](https://www.tutorialspoint.com/java/java_interview_questions.htm)


[https://youtube.com/playlist?list=PL63BDXJjNfTElajNCfg_2u_pbe1Xi7uTy&si=6a8hzb0vrddhfb3z](https://youtube.com/playlist?list=PL63BDXJjNfTElajNCfg_2u_pbe1Xi7uTy&si=6a8hzb0vrddhfb3z)

![YouTube](https://slack-imgs.com/?c=1&o1=wi32.he32.si.gu&url=https%3A%2F%2Fwww.youtube.com%2Fs%2Fdesktop%2F716a93d8%2Fimg%2Flogos%2Ffavicon.ico)YouTube

Java 8 Streams API Interview Questions (Most Asked)

Java 8 Streams API Interview Questions (Most Asked)

you can start reviewing the interview questions if you have bandwidth/cycles available..  
we will add lot more stuff over time..[https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture9-interview-questions.md](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture9-interview-questions.md)


topics 
Java Core Topics:  

- *Requirements/Contract Driven Top Down Model - Building Microservices
- *Singleton
    - Difference Variants
    - Coding
    - Understanding why we use the synchronized, static keywords
- Builder (Low Priority)
- *String manipulation Coding questions
- *Fibonacci Coding
    - Recursively and Non-Recursively
- *Factorial
- *OOPS Concepts
- *Thread Safety
    - What is Thread Safety
    - Performance Discussion
    - ThreadJoins
- *Deadlocks
    - Creating Deadlocks
    - How to prevent deadlock
    - Live Lock
    - Reentrant Lock
    - Semaphore
    - Mutex
    - Latches
- Static Keyword
- DB, SQL
    - Left Join, Right Join, Left Outer Join, Right Outer Join\
- Final VS Finally VS Finalize
- Volatile, Atomic Integers
- Hashmap - Bucketing, Collisions
- *ConcurrentHashmap and Hashmap
- *Equals and hashcode
- Comparable and Comparator
- Serializable
- Time Complexity and Performance on different data structures
- *Java 8 Streams API, and Lambda
    - Functional Interfaces - Functions

- Runnable VS Callable
- Spring VS Spring-Boot
- Compile-time VS Run-time polymorphism
- 2-Way SSL


kafka Rebalancing Protocol [https://www.youtube.com/watch?v=MmLezWRI3Ys](https://www.youtube.com/watch?v=MmLezWRI3Ys)
[https://kafka.apache.org/documentation/#consumer_rebalance_protocol](https://kafka.apache.org/documentation/#consumer_rebalance_protocol)


#interview-prep**hsbc screening -****if you are in hashmap**  
  **- key is employee class then what thing you need to manage**  
   **you have to put proper equals and hashcode for proper**    
   **duplicate detection****-where do you use kafka in project**  
**- consumer, producers, streaming**  
**- multithreading**  
**- global variable in class, how to ensure its thread-safe** **- sticky vs round-robin**  
**- how do i make sure the messages for a given creditcard to cusotmer go to same partition every time -****- avro benefits**  
**- it saves on the space on disk because its binary format**  
**- JSON is very wasteful with lots of white space**  
   **- it is very fast for serialization/deserialization that improves processing speed of our kafka pipeline**  
   **- we use Confluent AvroSerializer/DeSerializer**  
   **- it allows to give message schema. that can evolve over time and keeps the consumers backward compatible**  
   **- basically it allows schema evolution**  
   **- it works with schema registry**   
**- React**  
**- functional vs class components**  
  **- how you do navigation - navigation using react router**  
  **- how you secure the react to backend integration**  
**- Spring Security , JWT tokens**  
     **- how do you verify the JWT tokens -**
     
#interviewquestions hibernate 
https://medium.com/@pratik.941/mastering-hibernate-key-interview-questions-3bcc5f2b7775




#links-to-read for kafka related questions :
https://medium.com/@gaddamnaveen192/kafka-230-all-scenario-interview-questions-to-help-you-crack-40c146432b43#7676