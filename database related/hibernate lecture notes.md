- JPA simplifies database access by introducing object-relational mapping and higher-level abstractions. Hibernate and JDBC: Hibernate abstracts JDBC, providing a higher-level API for developers. While JDBC is manually code-intensive, Hibernate automates many aspects of database access.JPA simplifies database access by introducing object-relational mapping and higher-level abstractions. Hibernate and JDBC: Hibernate abstracts JDBC, providing a higher-level API for developers. While JDBC is manually code-intensive, Hibernate automates many aspects of database access.
- In simple terms, JPA can be called the interface, while Hibernate is the implementation of these interfaces. JPA specifies standards for developers to perform database operations seamlessly, while Hibernate uses these standards of the Java Persistence API to carry out operations on the database.
- Hibernate metadata are all the annotations used to describe the behaviour of the POJO fields , to get rid of  the metadata u can use the Session.detach(user)
- Object Relational Mapping - Hibernate ->>>>>> benefits
- Productivity: Faster development with reduced boilerplate code 
- Maintainability: Easier to manage  with an OOPs approach 
- Performance:  Optimized data access and caching mechanisms
- Vendor Independence: Works with various database vendors without changing the code.

  

It consists of:

- **An API**: To perform CRUD (Create, Read, Update, Delete) operations on objects of persistent classes.
- **A Query Language**: To specify queries that refer to classes and properties of classes.
- **Mapping Metadata Facility**: To specify mapping metadata.
- **ORM Interaction Technique**: For the ORM implementation to interact with transactional objects, perform dirty checking, lazy association, fetching, and other optimization functions.

  

  

Object-Relational Impedance Mismatch refers to the conceptual and technical differences between object-oriented programming (OOP) and relational databases (RDBMS). In the context of Hibernate, a popular Java ORM (Object-Relational Mapping) framework, this mismatch can be challenging because OOP and RDBMS handle data differently:

1. **Inheritance**: OOP supports inheritance, allowing objects to inherit properties and methods. However, relational databases don't have a direct concept of inheritance, making it tricky to map class hierarchies to database tables.
2. **Identity**: Objects in OOP are identified by memory references, while rows in relational databases are identified by primary keys. Handling this difference in identity can lead to synchronization issues.
3. **Granularity**: In OOP, an object can be composed of smaller objects (fine-grained). In relational databases, data is usually stored in tables that represent a coarser granularity (e.g., single rows).
4. **Associations**: Objects can have complex relationships (e.g., one-to-many, many-to-many) that are difficult to represent in RDBMS, which mostly uses foreign keys and join tables.
5. **Navigation**: In OOP, you can easily navigate object relationships via references. In RDBMS, relationships are navigated using joins, which can lead to performance issues.

Hibernate helps bridge these gaps by providing mechanisms to map classes to tables, handle relationships via annotations or XML mappings, and manage transactions and caching to synchronize objects and database states.
  

**You said:**

Objects in OOP are identified by memory references, while rows in relational databases are identified by primary keys. Handling this difference in identity can lead to synchronization issues. How it can lead to the synchronization issues

  
**ChatGPT said:**

ChatGPT

The difference between **object identity** in OOP and **relational identity** in databases can lead to **synchronization issues** in systems using Object-Relational Mapping (ORM) frameworks like Hibernate. These issues arise because the way objects are identified and tracked in memory differs from how rows are identified and tracked in a relational database. Let me explain the key points where this mismatch can cause problems:

**1. Object Identity vs. Database Identity**

- **Object Identity (OOP)**: In object-oriented programming, two objects are considered the same if they refer to the same memory address (i.e., object1 == object2 compares their memory locations). This is managed by the JVM's memory system.
- **Relational Identity (RDBMS)**: In relational databases, two rows are considered the same if they share the same primary key value. Relational identity is managed by the database system.

**Synchronization Issue**:

- If two different objects representing the same database row are loaded separately in memory (because they have different memory addresses), they will not be recognized as the same, leading to **identity confusion**.
- For example, if you load an object A from the database and then load the same row again into object B, A and B will have the same data but different memory references. If changes are made to both objects and saved back to the database, inconsistencies can arise, because both versions of the object might be trying to update the same row.

  

**2. Detached Objects and Synchronization**

- **Persistent Objects**: When an object is loaded from the database using Hibernate (or another ORM), it is in a **persistent state**, meaning it is being tracked by the ORM session.
- **Detached Objects**: If an object is used outside the session or a new session is started, it becomes **detached**. This can lead to problems when an attempt is made to reattach and update the object.

**Synchronization Issue**:

- Imagine you load an object from the database, modify it outside the ORM session, and then try to save the changes. If another user (or another process) has already updated that same row in the database, your modifications may overwrite the new changes, causing **stale data** problems.
- This issue is often referred to as the **Lost Update Problem**—two versions of the same object are not in sync, and one overwrites the other without any conflict detection mechanism.

  

**3. Caching and Identity**

- ORMs like Hibernate use **first-level (session) cache** and sometimes a **second-level (shared) cache** to store objects in memory for performance reasons. This caching can cause problems if the cached object becomes out of sync with the database.

**Synchronization Issue**:

- If the state of an object in memory (cache) doesn’t reflect the latest state in the database, and the object is saved back to the database, it may overwrite the most recent data, leading to **data inconsistency**.
- For example, if an object is fetched from the database and kept in memory for a long period, but during that time, another user updates the corresponding row in the database, the cached object becomes **stale**. When the object is saved again, the latest database changes are overwritten.

  

**4. Multiple Instances of the Same Object**

- In Hibernate, when an object is loaded from the database, the ORM keeps track of it in the current session. If you load the same row again in a new session, a new object instance is created.

**Synchronization Issue**:

- If two different sessions load the same row into different object instances and both modify the objects, when they are saved back to the database, **concurrent updates** could result in **conflicting changes**.
- For example, if Session A and Session B load the same database record into different objects, and both sessions modify their copies and attempt to save them, the session that saves last will overwrite the earlier changes.

  

**5. Versioning and Optimistic Locking**

- To address some of these synchronization issues, Hibernate provides **optimistic locking** using a version field. A version field is incremented every time an object is updated, helping detect conflicts.

**Synchronization Issue**:

- Without a versioning mechanism, updates to the same record by different users or processes will not be detected, resulting in potential **lost updates**.
- With versioning, if one user tries to update an object while another user has already changed the same object (and incremented the version), Hibernate will detect the version conflict and throw an exception, preventing inconsistent updates.

  

**Summary of Synchronization Issues:**

The mismatch between object identity (memory reference) and relational identity (primary key) can cause synchronization issues such as:

- **Identity Confusion**: Different memory references for the same row can lead to conflicting updates.
- **Lost Updates**: Changes can overwrite more recent data due to stale object states.
- **Data Inconsistency**: Cached objects can become stale and cause updates to be based on outdated data.
- **Concurrent Update Conflicts**: Multiple sessions may load and modify the same row, leading to conflicts if no conflict resolution (like optimistic locking) is in place.

To mitigate these issues, Hibernate offers mechanisms like **session management**, **versioning**, **caching strategies**, and **transactional handling**.

- Lombok is a framework which basically gets us rid of all the getter setters and constructors, equalsTo and hashcode.
- @Entity  = persistant Entity 
- @GeneratedValue => Identity (Auto Increment)
- Cascade -> ALL
- **What Is Cascading?**Entity relationships often depend on the existence of another entity, for example the _Person_–_Address_ relationship. Without the _Person_, the _Address_ entity doesn’t have any meaning of its own. When we delete the _Person_ entity, our _Address_ entity should also get deleted.Cascading is the way to achieve this. **When we perform some action on the target entity, the same action will be applied to the associated entity.**

  

  

- If only the flow is bidirectional then the owning side and the reverse side comes into play, otherwise in case of unidirectional there is no reverse side , the side which has the access to the other side automatically becomes the owning side.
- Owning side and reverse side : Address is aware of user as address is keeping the foreign key user _id , so Address is the owning side .
- In one to one -> owning side is the one who carries the foreign key to the other side .(owner side  table will have the foreign key In It)
- In one to one both will have the bidirectional access to their singular instance .

  

  

- Orphaned data refers to data that is no longer associated with a corresponding record or entity in a database, data storage or other information system.
- An object is orphaned when the object is created on one domain controller and the container in which the object is placed is deleted from the directory on another domain controller before the object has a chance to replicate.
- Session.detach(user) or keep the entity persistent and create a DTO (Data Transfer Object ) with the fields you want to show on the screen . 

  

  

  

Hibernate-configuration

- Session-factory
- Property
- Mapping class or mapping package
- hbm is hibernate metadata
- **hibernate.cfg.xml**: Configures database connection and Hibernate properties.

  

  

- A SessionFactory is a connection factory that can use both pooled and non-pooled connections.
- It can utilize HikariCP to obtain connections from a connection pool, or use the DriverManager to open a direct connection socket to the database.

  

- @Embeddable - CompositeKey which implements Serializable
- @EmbeddedId 

Will be a virtual id which is the composite key instance .

- @MapsId means that we tie those keys
- And then backwards  

  

@IdClass annotation is used as an alternative for the composite key , if we use this annotation then we don’t need to create a seprate class for the composite key

Its similar to @EmbeddedId 

Difference : the attributes are defined in the main entity class using @id 

  

Fetching 

FetchType = LAZY , EAGER

FetchMode

- Data Access Pattern ::::: Fetch mode —>>  Eager Load , Lazy Load 
- In one to many relationship , many side should always be lazy loaded , and it should be the owning side. 
- User to books example for one to many relationship , books to authors example for many to many relationship 
- In @onetoone ,and @manytomany  default fetchType is lazy.  
      
      
    in case its a @onetoone 

And the  datatype is a CLOB , then you need a lazy fetch type 

  

  

—————————————————————————————————————————————————

  

  

EXTRA:

  

- Dirty checking collection 
- Flyway and liquibase frameworks
- Cross-cutting -> something which is the common concern of all business apps 
- Hibernate is an implementation which was reverse engineered to build a Spec named JPA (Java persistence API)
- In 2019 , java persistence api ( JPA ) was renamed to Jakarta persistence API.
- The **Java Persistence API (JPA), in 2019 renamed to Jakarta Persistence**, is a Java application programming interface specification that describes the management of relational data in applications using Java Platform, Standard Edition and Java Platform, Enterprise Edition/Jakarta EE.
- [https://blogs.oracle.com/javamagazine/post/transition-from-java-ee-to-jakarta-ee](https://blogs.oracle.com/javamagazine/post/transition-from-java-ee-to-jakarta-ee)

  

J2EE to Spring And SpringBoot Transformation in the industry:
![[J2EETOSPRINGBOOT.m4a]]
  

  

Both Quarkus and Micronaut allow developers to create native executables using the polyglot embeddable virtual machine GraalVM, which enhances application startup times and lowers memory usage. Quarkus has a slight advantage in this regard due to its native image support.
