Java**Interviewer**: Can you explain the core concepts of Object-Oriented Programming (OOP)?

https://medium.com/edureka/java-oop-cheat-sheet-9c6ebb5e1175
read this link for oops concepts 

**You**: Certainly! Object-Oriented Programming (OOP) is a programming paradigm that structures software design around objects, which can be real-world entities or abstract concepts. The four fundamental pillars of OOP are **Encapsulation**, **Inheritance**, **Polymorphism**, and **Abstraction**. Let me break them down:

1. **Encapsulation**: ''
    
    - This principle involves bundling the data (attributes) and methods (functions ) that operate on that data within a single unit, typically a class.
    - It ensures that the internal representation of an object is hidden from the outside world, which is achieved by using access modifiers like `private`, `public`, and `protected`.
    - For example, in a class, we might make a variable `private` and provide `getter` and `setter` methods to safely access and modify its value. This allows control over how data is accessed and updated, promoting security and integrity.
2. **Inheritance**:
    
    - Inheritance allows a new class (subclass) to inherit attributes and methods from an existing class (superclass). This fosters **code reuse** and establishes a natural hierarchical relationship.
    - For instance, a `Car` class can inherit from a `Vehicle` class, which allows the `Car` class to reuse general methods and attributes, while adding specific details like `numberOfDoors`.
    - **Method overriding** comes into play when a subclass provides its own implementation for a method defined in the superclass, allowing for customized behavior.
3. **Polymorphism**:
    
    - Polymorphism means "many forms." It allows methods or functions to behave differently based on the object they are acting upon.
    - There are two types:
        - **Compile-time (Method Overloading)**: We can define multiple methods with the same name but different parameters.
        - **Runtime (Method Overriding)**: The method that gets executed is determined at runtime. This is achieved through inheritance and method overriding.
    - For example, a method `draw()` in a `Shape` class can have different implementations in `Circle` and `Square`classes, even though the method name is the same.
4. **Abstraction**:
    
    - Abstraction is the concept of hiding the complex implementation details and exposing only the essential features of an object.
    - This is done through **abstract classes** and **interfaces**.
        - An **abstract class** cannot be instantiated and can contain abstract methods (methods without a body), which must be implemented by derived classes.
        - An **interface** defines a contract, outlining method signatures without implementation, and any class that implements that interface must provide its own behavior for these methods.
    - For example, a `Payment` interface might define a method `processPayment()`, which can have different implementations in `CreditCardPayment` or `PaypalPayment` classes.

In addition to these four pillars, other important design concepts like **Composition** (Has-A relationship), **Constructor/Destructor** (special methods for object initialization and cleanup), and **Association/Aggregation** also play a role in building well-structured, maintainable code. Composition, for instance, allows you to create complex objects by combining simpler ones, leading to more flexible and reusable designs compared to inheritance.

OOP emphasizes **modularity**, **reusability**, and **maintainability**—which are crucial for creating scalable and efficient software solutions.





The `static` keyword is an important concept in object-oriented programming, and it often comes up in interviews. Here are some common questions related to the `static` keyword that might be asked during an interview:

### 1. **What is the `static` keyword in Java/C++/any OOP language?**

- **Answer**: The `static` keyword is used to declare class-level variables and methods. It means that a member (variable or method) belongs to the class itself rather than to instances (objects) of the class. Static members are shared by all instances of the class.

### 2. **What are the uses of the `static` keyword?**

- **Answer**:
    1. **Static Variables**: These are variables that are shared across all instances of a class. They are initialized only once and hold a single value for all objects.
    2. **Static Methods**: These are methods that can be called without creating an instance of the class. They can only access static variables and other static methods in the class.
    3. **Static Blocks**: In some languages like Java, static blocks are used to initialize static variables. They are executed when the class is loaded into memory.

### 3. **What is the difference between a static variable and an instance variable?**

- **Answer**:
    - **Static Variable**: A static variable is shared by all instances of a class. It’s initialized once and maintains the same value across all objects.
    - **Instance Variable**: An instance variable is unique to each object. Each object has its own copy of the instance variable, and the value can differ from one object to another.

### 4. **Can a static method access instance variables or methods?**

- **Answer**: No, a static method cannot directly access instance variables or methods because static methods belong to the class, not to any specific instance. Static methods can only access other static members (variables and methods).

### 5. **Can a non-static method access static variables or methods?**

- **Answer**: Yes, a non-static method can access both static and instance variables/methods because the non-static method operates on specific instances and can access all members of the class, including the static ones.

### 6. **What is the purpose of a static block in Java?**

- **Answer**: A static block is used for static initialization of a class. It is executed once when the class is loaded into memory and can be used to initialize static variables or perform any setup required by the class.

### 7. **Can you override a static method?**

- **Answer**: No, you cannot override a static method. Static methods are bound at compile-time (static binding), so the method call is resolved based on the reference type, not the object type. However, you can hide a static method by declaring a static method in a subclass with the same signature, but this is not considered overriding.

### 8. **What is the difference between `static` and `final` keywords?**

- **Answer**:
    - **Static**: The `static` keyword means the variable or method belongs to the class itself and not to instances of the class.
    - **Final**: The `final` keyword means the value of a variable or the implementation of a method cannot be changed. For instance, a `final` variable cannot be reassigned, and a `final` method cannot be overridden.

### 9. **Can a static method be abstract?**

- **Answer**: No, static methods cannot be abstract because abstract methods are meant to be overridden by subclasses, but static methods belong to the class itself and cannot be overridden.

### 10. **What is the lifecycle of a static variable?**

- **Answer**: The lifecycle of a static variable starts when the class is loaded into memory and ends when the program terminates. Static variables are initialized only once, at the time the class is loaded, and they persist for the lifetime of the application.

### 11. **Can we create an instance of a class inside a static method?**

- **Answer**: Yes, you can create an instance of a class inside a static method. The static method itself does not require an instance to be called, but it can still instantiate objects of the class if necessary.

### 12. **What happens if we try to access a non-static member from a static method?**

- **Answer**: You will get a compile-time error because non-static members belong to instances of the class, and a static method does not have an instance associated with it.

### 13. **What are the advantages and disadvantages of using static variables?**

- **Answer**:
    - **Advantages**: Static variables are useful when you want to store data that is shared across all instances of a class. They reduce memory usage since the data is shared and initialized only once.
    - **Disadvantages**: Overuse of static variables can lead to issues with memory management and make the code harder to test and maintain because static variables maintain state across different objects.

### 14. **Can a constructor be static?**

- **Answer**: No, constructors cannot be static because they are used to create instances of the class, and static methods belong to the class itself, not to instances of the class.

### 15. **What is the "Singleton" design pattern and how does the static keyword relate to it?**

- **Answer**: The **Singleton pattern** is a design pattern that ensures a class has only one instance, and it provides a global point of access to that instance. The `static` keyword is commonly used to implement the Singleton pattern by creating a static variable to hold the single instance and a static method to provide access to it.



if in a coding question i used static keyword :

```
public class MaxIntInArray {  
  
    static int[] arrayOfInt = new int[]{1,2,3,4,5,6,0};  
  
  
    public static int findMax(int[] arrayOfInt){  
  
        OptionalInt max = Arrays.stream(arrayOfInt).max();  
        System.out.println("this is the max integer value in the array :" + max);  
        return max.getAsInt();  
    }  
  
  
    public static void main(String[] args) {  
        MaxIntInArray.findMax(arrayOfInt);  
    }  
}
```

the interviewer might ask :

The `static` keyword in Java is often used to indicate that a particular field or method belongs to the class itself, rather than to instances of the class. It is not inherently good or bad practice; it depends on the context of how and why you're using it.

### What the `static` keyword does:

- **For variables**: A `static` variable is shared by all instances of a class. It means that all objects of that class will have access to the same variable, and any changes to it will affect all objects.
- **For methods**: A `static` method can be called without creating an instance of the class. It operates on class-level data, not instance-level data.

### Why you might use `static`:

- **Utility or helper methods**: If the method doesn't need to access instance-level data, and it's meant to operate on data that is common to all instances (or no instance data at all), then it makes sense to make it static.
- **When you don’t need an object**: For example, in your case, the `findMax` method doesn't need an object of `MaxIntInArray` to find the maximum value. It’s just operating on the static array, so it’s convenient to make the method static.

### How you might answer in an interview:

#### 1. **If the question is about why you used `static`**:

- "I used the `static` keyword because the `findMax` method does not rely on any instance-specific data. The method operates on a class-level array (`arrayOfInt`) and is designed to be called directly on the class itself, without needing to instantiate an object of the `MaxIntInArray` class. This makes the code simpler and more direct, as we can call the method directly with `MaxIntInArray.findMax()`."

#### 2. **If the question is about whether `static` is a good or bad practice**:

- "Using `static` is neither inherently good nor bad—it depends on the use case. It's good practice when the method or variable is independent of object state, like utility functions or constants. However, overusing `static` can lead to code that’s harder to test or maintain, as it can tightly couple parts of your program to global state or class-level data. In this case, `static` makes sense because we're dealing with a class-level array and the function doesn’t need to work with instance-specific data."

#### 3. **Important considerations**:

- You should use `static` when the method or variable is not dependent on any instance of the class.
- It’s important to note that excessive use of `static` can make your code more difficult to maintain, especially if you're designing a complex system, as it can lead to dependencies that are hard to manage.

### Conclusion:

In this case, you're using `static` because you're dealing with a method that doesn't need to interact with instance-specific data. In an interview, it's important to demonstrate that you understand when and why `static` should be used. As long as you're using it for the right reasons (e.g., utility methods or class-level variables), you can justify your choice effectively.





#interviewquestions Difference between put and patch :

The main difference between `PUT` and `PATCH` in HTTP methods is how they update resources:

1. **PUT**:
   - **Full Update**: `PUT` is used to update a resource completely. When you send a `PUT` request, you must send the entire resource (all fields), even if you only want to update a small part of it. If any fields are missing, they may be overwritten or set to their default values.
   - **Idempotent**: `PUT` is considered idempotent, meaning that making the same `PUT` request multiple times will have the same effect as making it once. The resource's state will remain the same after the request.

   Example: If you have a resource representing a user with a name and email, and you send a `PUT` request with only a new email, the name might get wiped out or set to null if not included in the request.

   ```json
   {
     "name": "John",
     "email": "john.doe@example.com"
   }
   ```

2. **PATCH**:
   - **Partial Update**: `PATCH` is used to update a resource partially. You only send the fields that need to be updated, leaving other fields intact. This is more efficient when you want to change just one or two attributes of the resource.
   - **Not Necessarily Idempotent**: `PATCH` can be idempotent, but it doesn't always guarantee this. If the update modifies data based on conditions that may change (like timestamps or other dynamic data), multiple `PATCH` requests could result in different outcomes.

   Example: If you only want to update the email of a user and leave the name unchanged, you would use a `PATCH` request:

   ```json
   {
     "email": "new.email@example.com"
   }
   ```

In summary:
- **PUT** is for complete replacements (you send the whole resource).
- **PATCH** is for partial updates (you only send the fields to be updated).

Yes, here are a few additional important points to consider about **PUT** and **PATCH** when preparing for an interview:

### 1. **Usage Scenarios**:
   - **PUT**:
     - Best used when you are replacing an entire resource.
     - Appropriate when you have all the information to update the resource and want to ensure consistency (e.g., updating a user profile where every field is provided).
     - If you're building a REST API and need to ensure the resource reflects exactly what the client sends, `PUT` is the right choice.
   
   - **PATCH**:
     - Used when you want to update only a subset of the resource.
     - Ideal for cases where you don’t need to send the entire resource but only a few attributes (e.g., changing a user’s email, or updating just one part of a complex document).
     - More efficient when updating large resources with only small changes.

### 2. **Performance Considerations**:
   - **PUT** could be less efficient because it requires sending the full resource, even if only part of it needs updating.
   - **PATCH** is generally more efficient when you only need to update certain fields, as it reduces the payload size.

### 3. **Idempotency**:
   - **PUT** is guaranteed to be **idempotent**. This means that calling the same `PUT` request multiple times will always have the same result, which is important for maintaining consistency, especially in distributed systems.
   - **PATCH** is **not guaranteed** to be idempotent. For example, a `PATCH` request might update a value depending on the current state of the resource (e.g., incrementing a counter), and repeated calls could result in different outcomes.

### 4. **Overwriting vs. Modifying**:
   - **PUT** typically overwrites the resource entirely, which could result in loss of information if the client doesn’t send the full data (e.g., if you don't send all fields, they might be deleted).
   - **PATCH** is usually intended for modification, and should only update the fields provided, leaving the rest of the resource intact.

### 5. **Standards and Best Practices**:
   - The **HTTP/1.1** specification describes both methods, and they have distinct semantics in RESTful design.
   - Some APIs or systems may accept both methods but expect specific formats or behaviors (e.g., `PUT` for full updates, `PATCH` for partial updates).
   
### 6. **Security Considerations**:
   - With **PUT**, you might face security concerns because it could overwrite a resource entirely, potentially causing data loss if the update is not carefully managed.
   - **PATCH** might be more secure in some cases because it limits changes to only certain parts of the resource, which can reduce the risk of inadvertent data loss.

### 7. **Cacheability**:
   - **PUT** requests can potentially be cached if the URL doesn't change, but since it represents a complete replacement of the resource, caching may need to be managed carefully.
   - **PATCH** requests, on the other hand, might be more challenging to cache, as they don’t represent a full replacement of the resource, and cache invalidation mechanisms could vary depending on how partial updates are handled.

### 8. **Request Body**:
   - **PUT** typically requires sending the full representation of the resource in the request body, which might sometimes include default values or fields that were not intended to be changed.
   - **PATCH** can vary in its request body format. It might use different formats like JSON Patch (RFC 6902) or Merge Patch (RFC 7386) to specify the changes to apply to the resource.

### Example Use Cases:
   - **PUT**: 
     - Updating an entire user profile: changing name, email, phone number, etc., at once.
     - Replacing a product description or entire product details.
   - **PATCH**:
     - Changing only the email of a user without affecting other fields.
     - Updating a product’s stock quantity or price.

### 9. **RFC Specifications**:
   - **PUT**: Defined in [RFC 7231](https://tools.ietf.org/html/rfc7231#section-4.3.4).
   - **PATCH**: Defined in [RFC 5789](https://tools.ietf.org/html/rfc5789), which describes how partial updates to a resource should be handled.

---

**Interview Tip**: When asked about `PUT` vs `PATCH`, you should:
1. Explain the differences clearly (full vs partial update).
2. Discuss the concept of idempotency and the impact on consistency.
3. Provide real-world scenarios where each would be appropriate.
4. Address performance, security, and caching considerations.
5. Know about different patching strategies (like JSON Patch or Merge Patch) when it comes to `PATCH` requests.

By understanding these nuances, you'll be able to answer questions confidently and provide a detailed explanation that goes beyond just the basics!


 #QUESTION DEEP COPY VS SHALLOW COPY 
## **🌟 Shallow Copy**

- **Definition**: Copies the references **only** — not the actual objects.
    
- **Meaning**: The copied object and the original object share the same _references_ to the inner objects (not new inner objects).
    
- **Impact**: If you change a nested object (like a field that is a list, map, or another object), **both** copies will reflect the change because they point to the _same_ object inside.

### **Example:**

```
class Student {
    String name;

    Student(String name) {
        this.name = name;
    }
}

class School {
    Student student;

    School(Student student) {
        this.student = student;
    }
}

public class Main {
    public static void main(String[] args) {
        Student student1 = new Student("Alice");
        School school1 = new School(student1);

        // Shallow copy: just copying the reference
        School school2 = school1;

        school2.student.name = "Bob"; // changing through school2

        System.out.println(school1.student.name); // Output: Bob (changed!)
    }
}
```

▶ **Observation**:

- school1 and school2 are different references **BUT** the student inside them is the **same object**.
    
- When you changed school2.student.name, it **affected** school1 too.
    

---

## **🌟 Deep Copy**

- **Definition**: Copies **everything**, including _all nested objects_.
    
- **Meaning**: The new object and its inner objects are completely _separate_ from the original.
    
- **Impact**: Changing a nested object in the copy will **NOT** affect the original.
    

---

### **Example:**

```
class Student implements Cloneable {
    String name;

    Student(String name) {
        this.name = name;
    }

    // Deep copy of Student
    protected Object clone() throws CloneNotSupportedException {
        return new Student(this.name);
    }
}

class School implements Cloneable {
    Student student;

    School(Student student) {
        this.student = student;
    }

    // Deep copy of School
    protected Object clone() throws CloneNotSupportedException {
        Student newStudent = (Student) student.clone();
        return new School(newStudent);
    }
}

public class Main {
    public static void main(String[] args) throws CloneNotSupportedException {
        Student student1 = new Student("Alice");
        School school1 = new School(student1);

        // Deep copy
        School school2 = (School) school1.clone();

        school2.student.name = "Bob"; // Changing through school2

        System.out.println(school1.student.name); // Output: Alice (NOT changed)
    }
}
```

▶ **Observation**:

- school2 is a completely **independent copy**.
    
- Even the student object inside was separately copied.
    
- Changing school2.student.name **doesn’t** affect school1.student.name.
    

---

## **✨ Quick Summary Table**

|**Feature**|**Shallow Copy**|**Deep Copy**|
|---|---|---|
|Object Fields|References are copied|New objects are created and copied|
|Independence|Changes in inner objects affect both|Changes do **not** affect each other|
|Speed|Faster (since it just copies references)|Slower (needs to copy entire object graph)|
|How to create?|Default clone() behavior (Object class)|Need to override clone() carefully or manually copy|

  

---

## **✋ Important Notes for Java**

- **Default .clone()** in Java gives a **shallow copy**.
    
- To make a **deep copy**, you usually **override** clone() manually or use other techniques (like serialization, copy constructors, or libraries like Jackson).
    

---

## **🎯 Real Life Example:**

  

Imagine copying a _classroom_:

- **Shallow copy**: The new classroom gets **the same desks and chairs** as references. If you break a chair in one classroom, it’s broken in the other too!
    
- **Deep copy**: The new classroom gets **its own desks and chairs** (copied separately). Breaking a chair in one does **not** affect the other.
    

---

Would you like me to also show:

- 🔥 **How shallow/deep copy can cause real bugs in production**?
    
- 🔥 **How to deep-copy easily using Java serialization (trick)?**
    
- 🔥 **How popular libraries (like Apache Commons or Jackson) can deep-copy for you?**
    

  

I can even draw a **small diagram** if you want! 🚀

Want me to? 🎯

Perfect! Let’s dive into all of them 🔥 — **real-world bugs, serialization trick, libraries, and a visual diagram** to make it crystal clear for you.

---

# **1️⃣ How Shallow/Deep Copy Can Cause Real Bugs in Production**

  

🔴 **Bug scenario with shallow copy**:

Suppose you’re building a **banking app**.

You copy a Customer object to modify their new loan details.

  

But because you made a **shallow copy**, their original **account balance** object was **shared**, and accidentally **updated in the original customer too!**

  

Example:

```
class Account {
    double balance;
}

class Customer {
    Account account;
    String name;
}

// Somewhere in code:
Customer originalCustomer = new Customer(new Account(10000), "Alice");

// Shallow copy (bad)
Customer copyCustomer = originalCustomer;

// Modifying copy
copyCustomer.account.balance -= 5000;

// Now originalCustomer.account.balance is also reduced! ❌
```

▶ **Production Issue**: Customer account balance gets incorrectly deducted. 🧨 Huge disaster!

---

# **2️⃣ How to Deep-Copy Easily Using Java Serialization (The Trick)**

  

Instead of manually cloning everything, you can **serialize** and **deserialize** the object to make a deep copy magically.

  

Here’s how:

  

✅ **Steps**:

- Serialize the object into bytes (memory).
    
- Deserialize it back into a completely _new object_.
    

  

### **Example:**

```
import java.io.*;

class Student implements Serializable {
    String name;

    Student(String name) {
        this.name = name;
    }
}

class School implements Serializable {
    Student student;

    School(Student student) {
        this.student = student;
    }

    public static Object deepCopy(Object object) throws Exception {
        ByteArrayOutputStream baos = new ByteArrayOutputStream();
        ObjectOutputStream out = new ObjectOutputStream(baos);
        out.writeObject(object);

        ByteArrayInputStream bais = new ByteArrayInputStream(baos.toByteArray());
        ObjectInputStream in = new ObjectInputStream(bais);
        return in.readObject();
    }
}

public class Main {
    public static void main(String[] args) throws Exception {
        Student student1 = new Student("Alice");
        School school1 = new School(student1);

        // Deep copy using serialization
        School school2 = (School) School.deepCopy(school1);

        school2.student.name = "Bob";

        System.out.println(school1.student.name); // Output: Alice ✅
    }
}
```

▶ **Notes**:

- You must make your classes Serializable.
    
- Works super cleanly for complex objects.
    
- But _heavyweight_: not best for high-performance systems.
    

---

# **3️⃣ How Popular Libraries Deep Copy for You**

  

Instead of manually writing code, big projects use libraries to deep copy easily.

  

✅ **Examples**:

|**Library**|**How it Helps**|**Notes**|
|---|---|---|
|Apache Commons Lang|SerializationUtils.clone(object)|Needs Serializable|
|Jackson (JSON library)|ObjectMapper serialization-deserialization|Fast, can deep-copy even non-Serializable|

### **Example using Apache Commons:**

```
import org.apache.commons.lang3.SerializationUtils;

School school2 = SerializationUtils.clone(school1);
```

  

---

# **📊 Visual Diagram (Simple)**

  

Imagine School object pointing to a Student.

  

### **Shallow Copy (shared pointer):**

```
school1 --------> [Student: "Alice"]
school2 ---------/
```

▶ Both school1 and school2 point to the **same Student**.

---

### **Deep Copy (separate objects):**

```
school1 --------> [Student: "Alice"]

school2 --------> [Student: "Alice"]
```

▶ Two completely **different Students** (copied values, different memory).

---

# **🧠 Final Tips**

|**Context**|**Recommendation**|
|---|---|
|Small simple apps|Shallow copy is fine|
|Banking, Trading, E-commerce|Deep copy is safer (critical systems)|
|Many nested objects|Prefer library deep copy|
|Large systems (performance)|Manual deep-copy over serialization|

  

---

# **🔥 Quick Interview-Line You Can Say**

  

> “In Java, a shallow copy copies references leading to shared nested objects, whereas a deep copy clones the entire object graph recursively. Shallow copy risks bugs like shared state mutation, especially in financial and multithreaded systems. In practice, deep copy can be achieved manually, via serialization tricks, or using libraries like Apache Commons or Jackson.”

  
  ## **✅  What are the main Concurrent Collection classes in Java?**
| **Collection Type** | **Class**                               | **Notes**                      |
| ------------------- | --------------------------------------- | ------------------------------ |
| **List**            | CopyOnWriteArrayList                    | Read-heavy use cases           |
| **Set**             | CopyOnWriteArraySet                     | Backed by CopyOnWriteArrayList |
| **Map**             | ConcurrentHashMap                       | Highly concurrent              |
| **Queue**           | ConcurrentLinkedQueue                   | Lock-free                      |
| **Deque**           | ConcurrentLinkedDeque                   | Double-ended, lock-free        |
| **BlockingQueue**   | ArrayBlockingQueue, LinkedBlockingQueue | Blocking on insert/retrieve    |
> ✅ All classes in java.util.concurrent designed for high concurrency without external synchronization.

## **✅ How will you convert a Collection to SynchronizedCollection in Java?**
  

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




