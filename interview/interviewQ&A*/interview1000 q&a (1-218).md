  
---

### **Java Basics**

  

**1. What is the difference between JDK and JRE?**

The JDK (Java Development Kit) is a full-featured software development kit that includes the JRE (Java Runtime Environment), compiler (javac), debugger, and other tools for developing Java applications. The JRE, on the other hand, only provides the libraries and JVM necessary to run Java programs but cannot compile them. In short, JDK = JRE + development tools. For developers, JDK is essential, while end users typically only need JRE.

  

**2. What is Java Virtual Machine (JVM)?**

The JVM is an abstract machine that provides a runtime environment for executing Java bytecode. It abstracts away the underlying operating system, enabling Java’s platform independence. It includes a class loader, a bytecode verifier, a runtime execution engine, and memory management (GC). JVMs can differ between vendors but must follow the JVM specification, ensuring Java programs behave consistently.

  

**3. What are the different types of memory areas allocated by JVM?**

The JVM organizes memory into several areas:

- **Heap**: Stores objects and class instances.
    
- **Stack**: Stores method call frames and local variables.
    
- **Method Area (MetaSpace in Java 8+)**: Stores class metadata.
    
- **Program Counter Register**: Tracks the current executing instruction.
    
- **Native Method Stack**: Used for native (non-Java) method calls.
    
    Each area serves a specific runtime need and is managed automatically by the JVM.
    

  

**4. What is JIT compiler?**

JIT (Just-In-Time) compiler is part of the JVM that improves performance by compiling bytecode into native machine code at runtime. Instead of interpreting bytecode line-by-line, JIT compiles frequently used (“hot”) code paths, caches them, and reuses them, reducing execution time. It works alongside the interpreter and is key to Java’s performance competitiveness.

  

**5. How Java platform is different from other platforms?**

Java is platform-independent at the source and binary level due to the JVM. Unlike C/C++, Java doesn’t compile to platform-specific binaries. Instead, Java code compiles to bytecode, which the JVM interprets or compiles on the target platform. This architecture enables the same compiled code to run on any device with a compliant JVM.

  

**6. Why people say that Java is ‘write once and run anywhere’ language?**

This phrase stems from Java’s use of bytecode and the JVM. Once a Java program is compiled into bytecode, it can run on any platform with a JVM, regardless of underlying hardware or OS. This cross-platform capability is built into the Java specification and makes Java ideal for distributed systems and enterprise applications.

  

**7. How does ClassLoader work in Java?**

The ClassLoader dynamically loads Java classes into the JVM during runtime. It follows a parent delegation model: the Bootstrap loader loads core Java classes, the Extension loader loads ext libraries, and the Application loader loads user-defined classes. Developers can also define custom ClassLoaders to override or extend the loading behavior, often used in frameworks and containers.

  

**8. Do you think ‘main’ used for main method is a keyword in Java?**

No, main is not a keyword. It is just the conventional name used as the entry point for standalone Java applications. The JVM looks for a method named main with the signature public static void main(String[] args) as the starting point of execution. It can be named differently internally but wouldn’t be recognized by the JVM for execution.

  

**9. Can we write main method as public void static instead of public static void?**

No, the order matters because static is a modifier for the method, not its return type. In Java syntax, modifiers must precede the return type. Writing public void static results in a compilation error. The correct order is public static void, where void is the return type and static indicates that the method belongs to the class, not an instance.

  

**10. In Java, if we do not specify any value for local variables, then what will be the default value of the local variables?**

Local variables in Java do **not** have a default value. They must be explicitly initialized before use, or the compiler will throw an error. This design prevents unintentional logic errors and encourages safer coding practices. This differs from instance or static variables, which do have default values like 0, false, or null.

  

**11. Let’s say we run a Java class without passing any arguments. What will be the value of the String array of arguments in Main method?**

If no arguments are passed, the String[] args parameter is initialized as an empty array, not null. This means args.length == 0, and you can safely check the length without a NullPointerException. It’s good practice to validate the presence of arguments using this property to avoid out-of-bounds exceptions.

  

**12. What is the difference between byte and char data types in Java?**

The byte is an 8-bit signed data type that stores integer values from -128 to 127. It’s primarily used for memory-efficient numerical storage. The char type is a 16-bit unsigned Unicode character representation, capable of storing a single character from the Unicode set. Internally, Java uses UTF-16 encoding, making char suitable for international characters.

---

### **OOPs**

  

**13. What are the main principles of Object Oriented Programming?**

OOP is based on four key principles:

- **Encapsulation**: This principle involves bundling the data (attributes) and methods (functions ) that operate on that data within a single unit, typically a class.
    - It ensures that the internal representation of an object is hidden from the outside world, which is achieved by using access modifiers like `private`, `public`, and `protected`.
    
- **Abstraction**: Abstraction is the concept of hiding the complex implementation details and exposing only the essential features of an object.
    - This is done through **abstract classes** and **interfaces**.
        - An **abstract class** cannot be instantiated and can contain abstract methods (methods without a body), which must be implemented by derived classes.
        - An **interface** defines a contract, outlining method signatures without implementation, and any class that implements that interface must provide its own behavior for these methods.
    
- **Inheritance**:  Inheritance allows a new class (subclass) to inherit attributes and methods from an existing class (superclass). This fosters **code reuse** and establishes a natural hierarchical relationship.
    
- **Polymorphism**: Polymorphism means "many forms." It allows methods or functions to behave differently based on the object they are acting upon.
    - There are two types:
        - **Compile-time (Method Overloading)**: We can define multiple methods with the same name but different parameters.
        - **Runtime (Method Overriding)**: The method that gets executed is determined at runtime. This is achieved through inheritance and method overriding.
    
    These principles enhance code reusability, modularity, testability, and maintainability.
    

  

**14. What is the difference between Object Oriented Programming language and Object Based Programming language?**

OOP languages (like Java, C++) support all four OOP principles, including inheritance and polymorphism. Object-Based languages (like JavaScript pre-ES6 or VBScript) support objects but not inheritance or polymorphism in the classical sense. Java is a pure OOP language except for primitives, while JavaScript is prototype-based, not class-based originally.

  

**15. In Java what is the default value of an object reference defined as an instance variable in an Object?**

The default value of an object reference as an instance variable is null. Unlike local variables, instance variables are initialized automatically by the JVM. Developers should ensure proper instantiation before use to avoid NullPointerException, especially in real-time systems or constructors.

  

**16. Why do we need constructor in Java?**

Constructors are special methods used to initialize objects. When an object is created with new, the constructor sets the initial state. It ensures that necessary data is set before any method usage. Java allows constructor overloading for flexible object creation and also supports constructor chaining using this() or super().

  

**17. Why do we need default constructor in Java classes?**

If no constructor is explicitly defined, the Java compiler provides a default no-arg constructor. It is crucial for frameworks like Hibernate or Jackson that instantiate classes via reflection. If you define a parameterized constructor and still need a no-arg one, you must explicitly declare it, or you’ll face a compilation error when no-arg construction is required.

  

**18. What is the value returned by Constructor in Java?**

Constructors do not return any value, not even void. They return the reference to the newly created object implicitly. The return type is omitted because the purpose is to create and initialize objects, not to compute values. If a return type is mistakenly specified, the method becomes a regular method, not a constructor.

  

**19. Can we inherit a Constructor?**

No, constructors are not inherited in Java. Each class must define its own constructors, though you can call a parent constructor using super(). This is by design to prevent ambiguity and ensure encapsulation. However, subclass constructors can reuse superclass constructors’ logic through constructor chaining.

  

**20. Why constructors cannot be final, static, or abstract in Java?**

- **final**: Constructors are never inherited, so marking them final makes no sense.
    
- **static**: Constructors belong to objects, not the class, while static pertains to class-level methods.
    
- **abstract**: Abstract methods must be overridden, but constructors can’t be inherited or overridden.
    
    Hence, such modifiers violate constructor semantics.
    


### **Inheritance and Keywords**


**21. What is the purpose of ‘this’ keyword in Java?**

The this keyword is a reference to the current object within an instance method or constructor. It helps resolve name conflicts between instance variables and method parameters or local variables. It can also be used to invoke other constructors (this()), pass the current object as a parameter, or return the current instance from a method. It’s essential for code clarity and to maintain consistency in chained or fluent APIs.

  

**22. Explain the concept of Inheritance?**

Inheritance allows one class (child or subclass) to acquire fields and methods from another class (parent or superclass), promoting code reuse and hierarchical classification. Java supports single inheritance through the extends keyword. It enables polymorphic behavior—subclasses can override superclass methods for specialized behavior. This design leads to flexible and maintainable code and supports the open/closed principle (open for extension, closed for modification).

  

**23. Which class in Java is superclass of every other class?**

The root class in Java is java.lang.Object. All classes, either directly or indirectly, inherit from it. It defines basic methods like equals(), hashCode(), toString(), clone(), wait(), notify(), etc. These methods provide a common foundation for all Java objects and can be overridden for custom behavior, especially in data classes and concurrent environments.

  

**24. Why Java does not support multiple inheritance?**

Java does not support multiple inheritance with classes to avoid the **Diamond Problem**, where ambiguity arises if two superclasses define the same method or field. Instead, Java supports multiple inheritance via **interfaces**, allowing a class to implement multiple interfaces. Since interfaces have no state (before Java 8), this avoids conflicts, and Java 8+ uses **default methods** with conflict resolution rules.

  

**25. In OOPS, what is meant by composition?**

Composition is a design principle where one object contains another object and delegates tasks to it. It’s a “has-a” relationship and is a preferred alternative to inheritance for code reuse. Composition allows more flexibility because behaviors can be changed at runtime by composing different objects, while inheritance is fixed at compile time. It’s a core principle in design patterns like Strategy and Decorator.

  

**26. How aggregation and composition are different concepts?**

Aggregation is a form of association where the child object can exist independently of the parent (e.g., a department has professors; professors can exist independently). Composition is stronger; the child’s lifecycle depends on the parent (e.g., a house has rooms; rooms don’t exist without the house). In Java, composition is implemented with private fields and no setters, while aggregation can allow external access.

  

**27. Why there are no pointers in Java?**

Java omits explicit pointers to enhance safety and security. Pointers can be dangerous, leading to memory leaks, buffer overflows, and difficult debugging. Instead, Java uses references that behave like safe pointers but without pointer arithmetic. This abstraction simplifies programming and enables the JVM’s garbage collector to manage memory automatically, which is crucial for robust enterprise applications.

  

**28. If there are no pointers in Java, then why do we get NullPointerException?**

Even though Java doesn’t expose raw pointers, object references internally behave like pointers. A NullPointerException occurs when you try to use a reference that points to null. It’s essentially a null memory address error, just hidden behind the abstraction. Tools like Optional in Java 8 and null checks using Objects.requireNonNull() can help mitigate these issues.

  

**29. What is the purpose of ‘super’ keyword in Java?**

The super keyword is used to refer to the immediate parent class. It can be used to call the superclass constructor (super()), access superclass methods/fields that are overridden/hiding in the subclass, and resolve ambiguity in inheritance hierarchies. It is especially useful in constructor chaining and when extending behavior without duplicating code from the parent class.

  

**30. Is it possible to use this() and super() both in same constructor?**

No, you cannot use both this() and super() in the same constructor because both must be the **first statement** in the constructor. You have to choose either to call another constructor of the same class (this()) or the parent class constructor (super()). If both are required, you must refactor logic to indirect method calls or constructor chaining.

---

### **Object Cloning and Static Concepts**

  

**31. What is the meaning of object cloning in Java?**

Object cloning means creating an exact copy of an object using the clone() method. For this to work, the class must implement the Cloneable interface; otherwise, CloneNotSupportedException is thrown. Java performs shallow cloning by default, copying fields as-is. For deep cloning (copying nested objects), manual implementation is needed. Cloning is helpful in caching, undo operations, or prototype design pattern.

  

**32. In Java, why do we use static variable?**

A static variable belongs to the class, not to instances. All instances share the same copy, making it ideal for shared data like counters, configuration, or constants. It’s memory-efficient and supports class-wide behavior. However, care must be taken in multi-threaded environments to avoid race conditions; hence, static fields are often used with synchronization or volatile.

  

**33. Why it is not a good practice to create static variables in Java?**

Excessive use of static variables leads to tight coupling, reduces testability, and makes unit testing difficult due to shared state across instances. It breaks the principles of OOP such as encapsulation and abstraction. In web applications, careless use of statics may cause memory leaks, concurrency bugs, and unexpected behavior across multiple users or sessions.

  

**34. What is the purpose of static method in Java?**

A static method belongs to the class rather than any instance. It can be called without creating an object, making it useful for utility methods (e.g., Math.pow()). Since it cannot access instance variables directly, it’s used for stateless behavior. Static methods also play a key role in factory methods, entry-point methods (main()), and helper functions.

  

**35. Why do we mark main method as static in Java?**

The main() method must be static so the JVM can invoke it without needing to instantiate the class. Since no object exists at the start of execution, a static method ensures that the application has a defined entry point. Marking it static also allows consistent signature recognition across platforms and IDEs for launching Java applications.

  

**36. In what scenario do we use a static block?**

A static block is used for static initialization, such as loading native libraries, setting up static fields, or logging during class loading. It executes once when the class is loaded into memory. It is especially useful when initialization logic is complex or can’t be performed in field declarations alone. It executes before the main method or object creation.

  

**37. Is it possible to execute a program without defining a main() method?**

In traditional Java SE applications, main() is required. However, in earlier Java versions or under specific environments (like static blocks or test frameworks), code could execute without main(). For instance, static blocks were used to print output before main() became mandatory. In Java EE or frameworks like Spring Boot, execution begins via other lifecycle hooks or annotations.

  

**38. What happens when static modifier is not mentioned in the signature of main method?**

If main() is not marked static, the JVM will not recognize it as a valid entry point, and a NoSuchMethodError: main will be thrown at runtime. Since the JVM doesn’t instantiate objects on its own, the absence of static prevents program startup. Correct signature: public static void main(String[] args).

  

**39. What is the difference between static method and instance method in Java?**

Static methods belong to the class and can be invoked using the class name; they can’t access instance variables directly. Instance methods belong to objects and can access instance and static members. Static methods are ideal for utility operations, while instance methods operate on object state. Also, static methods can’t be overridden in the traditional sense, only hidden.

---

### **Method Overloading and Overriding**

  

**40. What is the other name of Method Overloading?**

Method overloading is also known as **compile-time polymorphism** or **static polymorphism**. It allows multiple methods with the same name but different parameter lists in the same class. The method resolution is done at compile time based on method signatures. It improves code readability and enables flexibility in method design without affecting external APIs.



---

### **Method Overloading and Overriding**

  

**41. How will you implement method overloading in Java?**

Method overloading is implemented by defining multiple methods with the **same name** but **different parameter lists** in the same class. You can change the number of parameters, their types, or the order of types. Overloading is resolved during **compile time**, allowing methods to perform similar functions on different data types or argument patterns, enhancing flexibility and readability.

  

**42. What kinds of argument variations are allowed in Method Overloading?**

You can overload methods by:

- Changing the **number of parameters**
    
- Changing the **data types** of parameters
    
- Changing the **sequence** of parameters with different types
    
    However, **changing only the return type** is **not allowed**. Overloading doesn’t consider method return type during resolution—it only looks at the method signature (method name + parameter list).
    

  

**43. Why is it not possible to do method overloading by changing return type of method in Java?**

Java method resolution at compile time is based on the method signature, which includes only the method name and parameter types—not the return type. If overloading based solely on return type were allowed, it would lead to ambiguity, as the compiler wouldn’t know which version to call when the return value isn’t captured.

  

**44. Is it allowed to overload main() method in Java?**

Yes, you can overload the main() method by changing its parameter list. However, the JVM will **only execute** the standard signature: public static void main(String[] args). Other overloaded versions can be invoked **manually from within the standard main method**, which can be useful for testing or internal delegation.

  

**45. How do we implement method overriding in Java?**

Method overriding is implemented by defining a **method in a subclass** with the **same name, return type, and parameter list** as in its superclass. The method in the subclass replaces the inherited version during runtime. This enables **runtime polymorphism** and allows customizing inherited behavior while maintaining a consistent interface.

  

**46. Are we allowed to override a static method in Java?**

No, static methods cannot be overridden. Instead, they can be **hidden** if a subclass defines a static method with the same signature. This is called **method hiding**, not overriding, and it’s resolved at **compile time** based on the reference type, not the actual object. Only instance methods are eligible for true overriding.

  

**47. Why does Java not allow overriding a static method?**

Static methods are bound to the class, not instances. Overriding requires dynamic (runtime) dispatch based on the object’s type, which doesn’t apply to static methods. Allowing overriding for static methods would violate the class-based resolution model and lead to confusion in method behavior based on reference vs. object type.

  

**48. Is it allowed to override an overloaded method?**

Yes, overloaded methods can also be overridden, but **each overloaded version must be explicitly overridden**. That is, a method in the subclass must match the signature of each version of the overloaded method to override it. Overloading and overriding are independent concepts; one relates to compile-time polymorphism and the other to runtime behavior.

  

**49. What is the difference between method overloading and method overriding in Java?**

- **Overloading**: Same method name, different parameter list, within the same class or subclass, resolved at compile time.
    
- **Overriding**: Same method signature, subclass provides a new implementation, resolved at runtime.
    
    Overloading improves usability, while overriding enables polymorphism and behavioral extension.
    

  

**50. Does Java allow virtual functions?**

Yes, **all non-static, non-final, non-private methods in Java are virtual by default**. This means method calls are dynamically resolved at runtime using the actual object’s type. Java supports virtual functions to enable polymorphism. Methods can be made non-virtual using final, which prevents them from being overridden.

  

**51. What is meant by covariant return type in Java?**

Covariant return types allow an overridden method to return a **subclass** of the type declared in the parent method. This feature, introduced in Java 5, enhances polymorphism by enabling more specific return types in overridden methods. It helps avoid unnecessary casting and improves code readability and type safety.

---

### **Polymorphism**

  

**52. What is Runtime Polymorphism?**

Runtime polymorphism refers to the ability of the JVM to **dynamically resolve method calls** at runtime based on the actual object type, not the reference type. This is achieved using method overriding. For example, calling a method on a superclass reference that points to a subclass object results in the subclass method being invoked.

  

**53. Is it possible to achieve Runtime Polymorphism by data members in Java?**

No, data members (fields) are resolved at **compile time** based on the reference type. Only methods participate in runtime polymorphism. Even if a subclass hides a parent’s field, the field accessed depends on the **reference**, not the actual object, unlike overridden methods which depend on the object type.

  

**54. Explain the difference between static and dynamic binding?**

- **Static Binding (Early Binding)**: Method call is resolved at compile time. Applies to static, private, and final methods, and overloaded methods.
    
- **Dynamic Binding (Late Binding)**: Method call is resolved at runtime based on the actual object. Applies to overridden methods.
    
    Dynamic binding enables polymorphism, while static binding favors performance and predictability.
    

---

### **Abstraction**

  

**55. What is Abstraction in Object Oriented programming?**

Abstraction is the concept of **hiding implementation details** and exposing only the relevant functionality to the user. In Java, abstraction is achieved through **abstract classes** and **interfaces**. It helps in reducing complexity, improving maintainability, and focusing on _what_ an object does rather than _how_ it does it.

  

**56. How is Abstraction different from Encapsulation?**

- **Abstraction** is about hiding implementation details and showing only essential features to the outside world.
    
- **Encapsulation** is about bundling data and methods into a single unit (class) and restricting access using access modifiers.
    
    Abstraction is implemented via interfaces/abstract classes, while encapsulation is achieved using private fields and public getters/setters.
    

  

**57. What is an abstract class in Java?**

An abstract class is a class that **cannot be instantiated** and may contain **abstract methods** (methods without a body). It can also have concrete methods. Abstract classes define a common template for subclasses, allowing partial implementation and enforcing method contracts. They are useful in scenarios where code reuse and partial abstraction are required.

  

**58. Is it allowed to mark a method abstract without marking the class abstract?**

No, if a class contains at least one abstract method, it must be declared as abstract. Failing to do so results in a compilation error. This ensures that an incomplete class cannot be instantiated and that subclasses are compelled to provide the missing implementations.

  

**59. Is it allowed to mark a method abstract as well as final?**

No, this is not allowed. abstract means the method must be **overridden**, while final prevents a method from being **overridden**. These two modifiers contradict each other in purpose and semantics, so Java disallows combining them. This ensures clarity and consistency in class hierarchies.

  

**60. Can we instantiate an abstract class in Java?**

No, abstract classes **cannot be instantiated directly** because they may contain unimplemented methods. However, you can instantiate them **indirectly** by creating a concrete subclass or by using anonymous inner classes. Abstract classes are designed to act as templates for other classes, not to represent complete objects themselves.


---

### **🧩 Interfaces**

  

**61. What is an interface in Java?**

An interface is a reference type in Java, similar to a class, that can contain only **abstract methods**, **default methods (Java 8+)**, **static methods**, and **constants**. Interfaces define a contract that classes must fulfill, allowing abstraction without inheritance constraints. A class implements an interface using the implements keyword and must provide implementations for all its abstract methods. Interfaces enable multiple inheritance of type and polymorphic behavior.

  

**62. Is it allowed to mark an interface method as static?**

Yes, since **Java 8**, you can declare static methods in interfaces. These methods belong to the interface itself and are not inherited by implementing classes. They are used for utility or helper methods related to the interface, and are invoked using InterfaceName.methodName(). This keeps code modular and avoids cluttering implementing classes.

  

**63. Why an Interface cannot be marked as final in Java?**

Interfaces are meant to be **implemented**, and final prevents a class or interface from being extended or implemented. Marking an interface as final defeats its very purpose—to be a contract that other classes follow. Java enforces this design principle to preserve flexibility and extensibility in object-oriented design.

  

**64. What is a marker interface?**

A marker interface is an interface with **no methods or constants**, used to signal or mark a class as having a particular property. Examples include Serializable, Cloneable, and Remote. The JVM or frameworks check whether a class implements such interfaces and apply special behavior accordingly, like enabling serialization or deep copying.

  

**65. What can we use instead of Marker interface?**

**Annotations** are the modern alternative to marker interfaces. They offer more flexibility, can hold metadata, and are processed at runtime using reflection. For example, @Override, @Deprecated, or custom annotations like @Entity allow cleaner, extensible, and better-structured code without cluttering class hierarchies with empty interfaces.

  

**66. How Annotations are better than Marker Interfaces?**

Annotations support richer metadata, allow **key-value pairs**, and can target **methods, fields, constructors, or parameters**, whereas marker interfaces only apply at the class level. Annotations can be retained at runtime, parsed via reflection, and do not require altering class inheritance trees. They’re more declarative, concise, and better suited for modern frameworks (Spring, JPA, etc.).

  

**67. What is the difference between abstract class and interface in Java?**

| **Abstract Class**                                  | **Interface**                                      |
| --------------------------------------------------- | -------------------------------------------------- |
| Can have constructors                               | Cannot have constructors                           |
| Can maintain state (fields)                         | Only constants (unless default methods in Java 8+) |
| Can define protected and private methods            | Cannot (till Java 9+, only public or static)       |
| Single inheritance                                  | Multiple inheritance                               |
| Suitable for base class with partial implementation | Suitable for defining a contract                   |
| Use an abstract class for a shared base and state;  | use interfaces to represent capabilities.          |

**68. Does Java allow us to use private and protected modifiers for variables in interfaces?**

No, all variables in interfaces are **implicitly public, static, and final**. They must be initialized at the time of declaration and behave as constants. You cannot use private, protected, or instance-level variables in interfaces, as they are not meant to maintain state but to define behavior.

  

**69. How can we cast an object reference to an interface reference?**

If a class implements an interface, its object can be **upcasted** to the interface type using:

```
MyInterface obj = (MyInterface) new MyClass();
```

This enables **polymorphism**, allowing you to write loosely coupled code where object behavior is abstracted via interface contracts.

---

### **🔒 Final Keyword**

  

**70. How can you change the value of a final variable in Java?**

You **cannot change** the value of a final variable once assigned. For primitive types, it means the value is immutable. For object references, it means the reference cannot change, but the object’s internal state can still be modified unless the object is immutable. Final variables must be initialized either at declaration, in a constructor, or a static block (for static finals).

  

**71. Can a class be marked final in Java?**

Yes, marking a class as final prevents it from being subclassed. It’s useful for security and immutability. For example, String, Integer, and LocalDate are final classes to prevent subclassing, which could break their internal guarantees like hashcode caching or thread safety.

  

**72. How can we create a final method in Java?**

A final method is declared using the final keyword. Once marked, it **cannot be overridden** in any subclass. This is often used in base classes to enforce consistent behavior, avoid tampering in child classes, or ensure secure operations like logging, auditing, or validation logic.

  

**73. How can we prohibit inheritance in Java?**

By marking a class as final, you prevent it from being extended. Alternatively, making the constructor private also prevents subclassing (common in utility classes or singletons). For instance:

```
final class MyFinalClass { ... }
```

**74. Why Integer class is final in Java?**

Integer is immutable and thread-safe, which is critical for performance, caching, and integrity. Marking it final prevents subclassing and ensures that values can’t be changed, hashcodes can’t be altered, and its behavior remains predictable across the JVM, especially when used in collections or as keys in maps.

  

**75. What is a blank final variable in Java?**

A blank final variable is one that is declared final but **not initialized at declaration**. It must be initialized in the constructor (for instance variables) or in a static block (for static variables). It allows delayed initialization while still preserving immutability once set.

  

**76. How can we initialize a blank final variable?**

You can initialize it:

- In the **constructor** (for instance final fields)
    
- In a **static block** (for static final fields)
    
    This ensures the variable is initialized exactly once. For example:
    

```
final int x;
MyClass() {
   x = 10;
}
```

**77. Is it allowed to declare main method as final?**

Yes, the main() method can be declared as final. It does not affect program execution since the JVM simply requires the correct method signature. Marking it final prevents accidental overriding if someone attempts to extend the class and redefine main.

---

### **📦 Packages and Imports**

  

**78. What is the purpose of package in Java?**

Packages help organize classes logically and avoid **naming conflicts**. They support modular development, access control (public, protected), and version management. Java uses reverse domain naming conventions like com.example.module to ensure uniqueness. You import packages to access their classes and interfaces.

  

**79. What is java.lang package?**

java.lang is the **default package** automatically imported in every Java program. It contains fundamental classes like Object, String, Math, System, Integer, Throwable, etc. It is essential for basic language functionality and runtime operations.

  

**80. Which is the most important class in Java?**

The most important class is **java.lang.Object**, the root of the Java class hierarchy. Every class implicitly inherits from it. It defines key methods like toString(), equals(), hashCode(), and clone(), which form the foundation of object behavior and collection handling.

  

**81. Is it mandatory to import java.lang package every time?**

No, java.lang is **automatically imported** by the Java compiler. This means classes like String, Math, or System can be used directly without needing an explicit import statement.

  

**82. Can you import same package or class twice in your class?**

Yes, importing the same class or package multiple times has **no effect**. The compiler eliminates redundancy. However, it’s not recommended as it makes the code messy and could confuse readers or tools analyzing imports.

  

**83. What is a static import in Java?**

static import allows you to access static members of a class **without class qualification**. For example:

```
import static java.lang.Math.*;
double result = sqrt(4); // No need to write Math.sqrt
```

This improves readability for constants or utility methods but can reduce clarity if overused.

  

**84. What is the difference between import static com.test.FooClass and import com.test.FooClass?**

- import com.test.FooClass imports the **class** itself.
    
- import static com.test.FooClass.* imports **static members** (fields and methods) of the class.
    
    The former allows object creation (new FooClass()), while the latter allows direct access to static members (someStaticMethod()).
    

---

### **🌍 Internationalization**

  

**85. What is Locale in Java?**

A Locale is a class that represents a specific **geographical, cultural, or political region**. It’s used in internationalization (i18n) to tailor output like **language**, **currency**, **date format**, etc. For example, Locale.US or Locale.FRANCE ensures formatting matches user expectations in that region.

  

**86. How will you use a specific Locale in Java?**

You can set the Locale while formatting:

```
Locale fr = new Locale("fr", "FR");
NumberFormat nf = NumberFormat.getCurrencyInstance(fr);
System.out.println(nf.format(12345.67));
```

This prints currency in French format. Locale is used with classes like DateFormat, ResourceBundle, and NumberFormat.

---

### **📦 Serialization**

  

**87. What is serialization?**

Serialization is the process of converting an object into a **byte stream** so that it can be stored in a file, sent over a network, or persisted. Java provides Serializable interface for this, and ObjectOutputStream handles the process.

  

**88. What is the purpose of serialization?**

Serialization allows object persistence and **communication between systems** or processes. It is vital for storing state (e.g., in sessions), transferring data across sockets (e.g., in RMI), or saving to disk. It’s the foundation of many distributed and caching frameworks.

  

**89. What is Deserialization?**

Deserialization is the **reverse process**—reconstructing a Java object from a byte stream. Java uses ObjectInputStream for this purpose. It must be used carefully to avoid vulnerabilities like insecure object injection or remote code execution.

  

**90. What is Serialization and Deserialization conceptually?**

Conceptually, serialization is converting objects to a portable format (byte stream), and deserialization is recreating those objects later. It abstracts storage and communication, enabling **distributed computing** and **session state handling** across JVMs and servers.

  

**91. Why do we mark a data member transient?**

transient indicates that a field should **not be serialized**. Sensitive data (passwords), temporary fields, or non-serializable objects are marked transient to avoid security risks or serialization errors.

  

**92. Is it allowed to mark a method as transient?**

No. The transient keyword can only be applied to **fields**, not methods, classes, or local variables. Trying to mark a method as transient results in a compilation error.

  

**93. How does marking a field as transient makes it possible to serialize an object?**

If a class has non-serializable fields (like a Thread), serialization will fail. By marking them transient, the JVM skips those fields during serialization, allowing the remaining object state to be serialized successfully.

  

**94. What is Externalizable interface in Java?**

Externalizable is a sub-interface of Serializable that gives **full control** over serialization. It defines writeExternal() and readExternal() methods, allowing you to manually handle how the object’s state is serialized and deserialized. It offers performance and size optimizations at the cost of complexity.

  

**95. What is the difference between Serializable and Externalizable interface?**

| **Serializable**                 | **Externalizable**                            |
| -------------------------------- | --------------------------------------------- |
| Default serialization            | Custom serialization                          |
| Uses reflection                  | Uses manual logic                             |
| Easy to use                      | More control but complex                      |
| Serializable is for ease of use; |  Externalizable is for fine-grained control.  |

---

### **🔍 Reflection**

  

**96. What is Reflection in Java?**

Reflection is the ability to **inspect and modify** classes, methods, and fields at **runtime**. Java provides it through java.lang.reflect package. It’s powerful for frameworks (e.g., Spring), where object creation, dependency injection, and annotations are handled dynamically.

  

**97. What are the uses of Reflection in Java?**

Reflection enables:

- Instantiating classes dynamically
    
- Accessing private members
    
- Processing annotations
    
- Writing generic frameworks (ORM, DI)
    
- Unit testing tools like JUnit
    
    Though powerful, it’s slower and should be used carefully.
    

  

**98. How can we access private method of a class from outside the class?**

You can use reflection:

```
Method m = MyClass.class.getDeclaredMethod("myPrivateMethod");
m.setAccessible(true); // bypass access check
m.invoke(obj);
```

This is often used in testing, mocking, or internal tooling, though it breaks encapsulation.

  

**99. How can we create an Object dynamically at Runtime in Java?**

Use Class.forName("ClassName").newInstance() (deprecated) or:

```
Class<?> clazz = Class.forName("MyClass");
Object obj = clazz.getDeclaredConstructor().newInstance();
```

This is useful in plugin systems or frameworks needing flexible instantiation.

---

### **🗑️ Garbage Collection**

  

**100. What is Garbage Collection in Java?**

Garbage Collection (GC) is Java’s **automatic memory management** feature. It identifies and deallocates memory occupied by objects that are **no longer reachable**, preventing memory leaks. GC runs in the background and is managed by the JVM. Different algorithms (Serial, G1, CMS) optimize GC for various workloads. You can hint GC using System.gc() but JVM decides when to collect.


**101. Why does Java provide a Garbage Collector?**

Java provides a Garbage Collector (GC) to **automatically manage memory** and relieve developers from the burden of manual memory deallocation (as required in C/C++ using free() or delete). This prevents common memory-related bugs such as memory leaks and dangling pointers, enhances reliability, and improves productivity by allowing developers to focus on business logic rather than memory management. It also helps in optimizing heap usage efficiently.

  

**102. What is the purpose of gc() in Java?**

The gc() method in the Runtime or System class is used to **request** garbage collection explicitly:

```
System.gc();
```

It acts as a **hint to the JVM**, but **does not guarantee** that garbage collection will actually occur immediately. It’s often used when a developer suspects that memory needs to be freed up, especially in memory-sensitive operations, though modern JVMs handle GC automatically and efficiently.

  

**103. How does Garbage Collection work in Java?**

Garbage Collection works by finding **unreachable objects** in the heap and reclaiming their memory. Java uses **tracing GC algorithms** like:

- **Mark-and-sweep**: Marks reachable objects, then sweeps the rest.
    
- **Generational GC**: Divides heap into Young, Old (Tenured), and Permanent (Metaspace).
    
- **G1 GC / ZGC**: Modern low-pause collectors with region-based and concurrent collection.
    
    GC is triggered by JVM based on heuristics (e.g., when memory is low), and it runs on a separate **low-priority daemon thread**.
    

  

**104. When does an object become eligible for Garbage Collection in Java?**

An object becomes eligible for GC when **no live thread or static reference** can reach it. Common cases:

- The reference is set to null
    
- The reference goes out of scope
    
- Object forms an **island of isolation** (e.g., two objects referencing each other but not referenced from anywhere else)
    
    GC uses reachability analysis starting from GC Roots (like static fields, thread stacks, etc.) to determine eligibility.
    

  

**105. Why do we use finalize() method in Java?**

The finalize() method is invoked by the GC **before reclaiming an object’s memory**, giving the object a chance to clean up resources (like closing file handles or DB connections). It’s defined in java.lang.Object and can be overridden. However, its use is **discouraged** in modern Java due to unpredictability, performance issues, and the introduction of better alternatives like try-with-resources and cleaners in Java 9+.

---

### **📎 Java References**

  

**106. What are the different types of References in Java?**

Java provides four types of references in the java.lang.ref package:

1. **Strong Reference** – Default; GC will not collect unless explicitly nullified.
    
2. **Soft Reference** – Collected only when JVM is low on memory (used in caches).
    
3. **Weak Reference** – Collected eagerly during GC; useful for maps and caches.
    
4. **Phantom Reference** – Enqueued after object is finalized, used to track object reclamation (advanced use cases like cleaning up native resources).
    
    These help in fine-tuning memory management strategies.
    

  

**107. How can we reference an unreferenced object again?**

Once an object becomes **unreferenced**, it can only be referenced again **if it’s not yet collected by the GC**, and you still hold a **strong/soft/weak reference** to it. However, if GC has already reclaimed it, you **cannot retrieve it**. This is why caching with WeakReference or SoftReference can preserve potential reusability without preventing GC.

  

**108. What kind of process is the Garbage Collector thread?**

The Garbage Collector runs as a **low-priority daemon thread** managed by the JVM. It operates in the background and does not prevent the application from exiting. It is **automated**, non-deterministic, and works concurrently or in stop-the-world phases depending on the collector type (e.g., Serial, Parallel, G1, ZGC). Being a daemon, it ensures system responsiveness while freeing memory in idle CPU cycles.

---

### **⚙️ Runtime Class**

  

**109. What is the purpose of the Runtime class?**

java.lang.Runtime is a singleton class that allows Java applications to **interact with the environment** in which the application is running. It provides methods to:

- Invoke garbage collection (gc())
    
- Exit the application (exit())
    
- Execute external processes (exec())
    
- Check memory (freeMemory(), totalMemory())
    
    It is accessed via Runtime.getRuntime() and is foundational for resource management and process control.
    

  

**110. How can we invoke an external process in Java?**

You can invoke external OS-level processes using:

```
Process process = Runtime.getRuntime().exec("notepad");
```

Or more robustly via ProcessBuilder:

```
ProcessBuilder pb = new ProcessBuilder("ping", "google.com");
pb.start();
```

This is used in automation, shell integration, invoking Python scripts, etc. It also supports input/output streams to interact with the process programmatically.

  

**111. What are the uses of Runtime class?**

Runtime class is used for:

- **Memory Management**: gc(), freeMemory(), totalMemory()
    
- **Process Control**: exec() to run shell commands or applications
    
- **Application Lifecycle**: exit() to terminate JVM
    
- **Shutdown Hooks**: addShutdownHook() to register cleanup logic
    
    It is especially useful in performance monitoring, native integrations, and application orchestration.
    

---

### **🔄 Nested Classes & Interfaces**

  

**112. What is a Nested class?**

A nested class is a class defined within another class. It helps in logically grouping classes that are only used in one place, enhances encapsulation, and improves readability. Nested classes have access to the members (even private ones) of their enclosing class. They are mainly used when the nested class logically belongs to the outer class.

  

**113. How many types of Nested classes are in Java?**

Java supports four types of nested classes:

1. **Static nested class**
    
2. **Non-static nested class (Inner class)**:
    
    - Member Inner class
        
    - Local Inner class
        
    - Anonymous Inner class
        
        Each has different access rules and use cases, tailored to specific design needs.
        
    

  

**114. Why do we use Nested Classes?**

Nested classes help:

- Group logically related classes for better maintainability.
    
- Encapsulate helper classes that should not be exposed outside.
    
- Access private members of the outer class, allowing tight coupling where necessary.
    
- Enhance modularity by keeping code that is tightly bound, together.
    

  

**115. What is the difference between a Nested class and an Inner class in Java?**

- **Nested class**: Any class defined within another class (static or non-static).
    
- **Inner class**: Specifically a **non-static nested class**, meaning it has access to instance members of the outer class and requires an instance of the enclosing class to be created.
    
    So, every Inner class is a Nested class, but not every Nested class is an Inner class.
    

  

**116. What is a Nested interface?**

A nested interface is an interface declared **inside a class or interface**. If declared inside a class, it is implicitly public static. It can be implemented either within the outer class or elsewhere. It’s useful when the interface is only relevant to its outer class or needs to serve as a contract for inner behavior.

  

**117. How can we access the non-final local variable inside a Local Inner class?**

From Java 8 onward, local variables used in a local inner class must be **effectively final**, meaning they are not modified after being assigned. This allows the inner class to safely capture the variable without creating inconsistent states, especially since the inner class instance may outlive the scope of the variable.

  

**118. Can an Interface be defined in a Class?**

Yes, you can define an interface inside a class. It is implicitly static, meaning it doesn’t depend on the outer class instance. It’s typically used for grouping interfaces logically or providing a type that is only relevant to the enclosing class.

  

**119. Do we have to explicitly mark a Nested Interface public static?**

No. A nested interface defined in a class is implicitly public static. This means you can implement it without creating an instance of the outer class. However, you **must explicitly mark it public** if you want it accessible outside the enclosing class.

  

**120. Why do we use Static Nested Interface in Java?**

Static nested interfaces allow defining a contract closely related to the outer class without needing an outer class instance. They’re commonly used in framework-style designs like Map.Entry, where the inner interface logically belongs to the outer class but should be accessible independently.

---

### **🧵 Strings and Immutability**

  

**121. What is the meaning of Immutable in the context of String class in Java?**

An immutable object’s **state cannot be changed** after it is created. For String, once created, any operation like concat, replace, or substring creates a **new String object** instead of modifying the original. This ensures thread safety, consistent hashcodes, and safe sharing of strings in memory.

  

**122. Why is a String object considered immutable in Java?**

Because:

- Strings are **interned** and shared in the String pool.
    
- Their immutability guarantees that cached hashcodes remain consistent.
    
- It improves performance in hashing and reduces synchronization overhead.
    
- Underlying char[] is declared final inside the String class.
    

  

**123. How many objects does the following code create?**

```
String s = new String("Java");
```

Two objects are created:

1. "Java" (in the String constant pool)
    
2. A new String object in the heap due to the new keyword, referencing the pooled string.
    

  

**124. How many ways are there in Java to create a String object?**

There are **two main ways**:

1. Using **String literals**: String s = "hello"; – stored in String pool.
    
2. Using **new keyword**: String s = new String("hello"); – creates a new object in heap.
    

  

**125. How many objects does the following code create?**

```
String a = "Hello";
String b = "Hello";
```

Only **one object** is created in the **String constant pool**. The second reference (b) points to the same memory location as a because of **string interning**.

  

**126. What is String interning?**

String interning is a **JVM optimization** where string literals are stored in a **common pool**. If a new string literal matches an existing one, the JVM reuses the same object. You can manually intern a string using intern() to store/reuse the pooled version.

  

**127. Why does Java use the String literal concept?**

To improve **memory efficiency and performance**. Since strings are heavily used, pooling avoids duplication. Reusing string literals avoids unnecessary object creation, especially in tight loops or repetitive tasks like key lookups or comparisons.

  

**128. What is the basic difference between a String and StringBuffer object?**

- **String** is immutable. Every modification results in a new object.
    
- **StringBuffer** is mutable and synchronized, allowing in-place modifications.
    
    Use String for small, static content and StringBuffer for concatenations in multi-threaded contexts.
    

  

**129. How will you create an immutable class in Java?**

To create an immutable class:

1. Mark the class final.
    
2. Declare fields private and final.
    
3. No setters; only **getters**.
    
4. Deep copy mutable objects in constructors and getters.
    
5. Initialize fields only once via constructor.
    
    This guarantees no state change after construction.
    

  

**130. What is the use of toString() method in Java?**

toString() returns a **string representation** of an object. By default, it returns ClassName@HashCode, but it’s often overridden to return human-readable content. This method is used in logging, debugging, and printing object data.

  

**131. Arrange the three classes String, StringBuffer and StringBuilder in the order of efficiency for String processing operations?**

In terms of efficiency:

StringBuilder > StringBuffer > String

- StringBuilder: Fastest, not thread-safe
    
- StringBuffer: Thread-safe but slower
    
- String: Slowest due to immutability
    

---

### **🚨 Exception Handling**

  

**132. What is Exception Handling in Java?**

Exception handling in Java is a mechanism to **handle runtime errors** gracefully without crashing the program. It uses try, catch, finally, throw, and throws keywords. It allows developers to define alternate flows, log errors, and recover from failures such as division by zero, file not found, or null references.

  

**133. In Java, what are the differences between a Checked and Unchecked Exception?**

- **Checked Exceptions**: Known at compile time, must be handled (e.g., IOException, SQLException)
    
- **Unchecked Exceptions**: Known at runtime, optional handling (e.g., NullPointerException, ArithmeticException)
    
    Checked exceptions enforce robustness; unchecked exceptions indicate programming logic errors.
    

  

**134. What is the base class for Error and Exception classes in Java?**

The root class is java.lang.Throwable.

It has two direct subclasses:

- Error: Serious issues (e.g., OutOfMemoryError)
    
- Exception: Recoverable issues (IOException, ParseException)
    

  

**135. What is a finally block in Java?**

finally is a block that always executes after try or catch, regardless of whether an exception was thrown or caught. It’s used to release resources like closing files, DB connections, or unlocking resources, ensuring cleanup occurs even during failures.

  

**136. What is the use of finally block in Java?**

The finally block ensures that critical cleanup code (closing files, releasing DB locks, disconnecting sockets) is always executed, regardless of exception occurrence. This prevents resource leaks and is crucial in enterprise-grade applications.

  

**137. Can we create a finally block without creating a catch block?**

Yes, a finally block can be used **without a catch block**, but a try block is still required:

```
try {
   // code
} finally {
   // cleanup
}
```

This is common when you need to clean up resources but don’t want to handle the exception immediately.

  

**138. Do we have to always put a catch block after a try block?**

No. A try block must be followed by **either** a catch, a finally, or **both**. So you can have:

- try-catch
    
- try-finally
    
- try-catch-finally
    
    But you **cannot** have try alone.
    

  

**139. In what scenarios will a finally block not be executed?**

The finally block **may not execute** if:

- The JVM shuts down using System.exit(0)
    
- The thread executing the try block is **killed forcibly**
    
- A catastrophic error like **OutOfMemoryError**
    
- Power failure or hardware crash
    
    In all other cases, it will execute.
    

  

**140. Can we re-throw an Exception in Java?**

Yes, we can re-throw an exception using throw inside a catch block:

```
catch (IOException e) {
    log(e);
    throw e; // re-throw
}
```

This is useful when you want to log or wrap the exception before re-throwing it for higher-level handlers.

  

**141. What is the difference between throw and throws in Java?**

- throw: Used to **explicitly throw** an exception object.
    

```
throw new NullPointerException();
```

- throws: Declares that a method **might throw** an exception.
    

```
public void readFile() throws IOException
```

throw is used inside method bodies; throws is part of method signatures.

  

**142. What is the concept of Exception Propagation?**

Exception propagation occurs when an exception is **not caught in the current method** and is passed up the call stack to the previous method. This continues until a handler is found or the program terminates. Only unchecked exceptions propagate by default; checked exceptions must be declared or handled.

  

**143. When we override a method in a Child class, can we throw an additional Exception that is not thrown by the Parent class method?**

No, if the parent method does **not declare any checked exceptions**, the child method **cannot declare new or broader checked exceptions**. It can:

- Declare **fewer** or **narrower** checked exceptions
    
- Declare **unchecked** exceptions
    
    This ensures the overriding method adheres to the parent’s contract and does not surprise callers.
    
---

### **🧵 Multithreading in Java**

  

**144. How does Multithreading work in Java?**

Java supports multithreading by allowing multiple threads to run concurrently within a single program. Each thread runs independently with its own call stack but shares the process memory space. Threads are created by extending the Thread class or implementing the Runnable or Callable interfaces. The JVM uses native OS-level threads, and thread scheduling is handled by the underlying OS using either **pre-emptive scheduling** or **time slicing**, depending on the system.

  

**145. What are the advantages of Multithreading?**

- **Better CPU Utilization**: Idle CPU cycles can be used by other threads.
    
- **Improved Application Responsiveness**: Especially in GUI or I/O-bound apps.
    
- **Parallelism**: Multiple tasks can be executed simultaneously (on multi-core processors).
    
- **Resource Sharing**: Threads share memory, reducing overhead.
    
- **Scalability**: Suitable for high-performance apps like servers, games, or real-time systems.
    

  

**146. What are the disadvantages of Multithreading?**

- **Complexity**: Writing thread-safe code is harder and more error-prone.
    
- **Race Conditions**: Without synchronization, threads may interfere with each other.
    
- **Deadlocks and Starvation**: Poor locking strategies can block progress.
    
- **Debugging Difficulty**: Bugs are non-deterministic and hard to reproduce.
    
- **Overhead**: Context switching and synchronization costs may degrade performance if misused.
    

  

**147. What is a Thread in Java?**

A thread is the **smallest unit of execution** within a process. It has its own **call stack** but shares heap memory with other threads. Java threads can be created using the Thread class or the Runnable/Callable interface. Each thread goes through states like New, Runnable, Running, Blocked, Waiting, and Terminated, and can be controlled using methods like start(), join(), sleep(), and interrupt().

  

**148. What is a Thread’s priority and how is it used in scheduling?**

Each thread in Java has a **priority (1 to 10)**, set using setPriority(). The default is Thread.NORM_PRIORITY (5). Priorities **suggest** thread importance to the OS thread scheduler, but **they are not guaranteed** to affect execution order, especially across platforms. Higher priority threads may get more CPU time, but scheduling behavior depends on the underlying JVM and OS.

  

**149. What are the differences between Pre-emptive Scheduling and Time Slicing Scheduling?**

- **Pre-emptive Scheduling**: The OS decides which thread to run based on priority or fairness. A thread can be forcibly suspended if another thread has higher priority.
    
- **Time Slicing**: Each thread is given a small unit of CPU time (a slice), after which it’s returned to the ready state.
    
    In reality, modern OSs often use a hybrid approach. Java doesn’t provide control over the scheduling policy—it delegates it to the OS.
    

  

**150. Is it possible to call run() method instead of start() on a thread in Java?**

Yes, but it’s **not the same**. Calling run() directly will **not create a new thread**; it just executes the run() method on the **current thread**. To start a new thread, you must call start(), which internally calls run() via a new thread context. This is a common mistake made by beginners.

  

**151. How will you make a user thread into a daemon thread if it has already started?**

**You cannot.** Once a thread has been started using start(), its daemon status **cannot be changed**. You must call setDaemon(true) **before** calling start(). Attempting to change it after the thread is alive will throw an IllegalThreadStateException.

  

**152. Can we start a thread two times in Java?**

No. Once a thread has started, it can never be restarted. Calling start() on a thread that has already completed or been started will throw an IllegalThreadStateException. You must create a new Thread instance to run the task again.

  

**153. In what scenarios can we interrupt a thread?**

A thread can be interrupted to **signal that it should stop or change behavior**, especially:

- When a thread is **blocked in sleep, wait, or join**
    
- When you want to **cancel a long-running task** gracefully
    
- When implementing cooperative interruption policies (e.g., in thread pools)
    
    Use interrupt() to signal and check Thread.interrupted() or catch InterruptedException to respond.
    

  

**154. In Java, is it possible to lock an object for exclusive use by a thread?**

Yes, by using **synchronized blocks or methods**:

```
synchronized(obj) {
    // critical section
}
```

Only one thread at a time can hold the lock on the object. This ensures mutual exclusion and is the basis of intrinsic locking. More advanced locks (e.g., ReentrantLock) from java.util.concurrent.locks offer greater control over synchronization.

  

**155. How is notify() different from notifyAll() in Java?**

- notify() wakes **one** random thread waiting on the object’s monitor.
    
- notifyAll() wakes **all** threads waiting on that monitor, but only one proceeds after acquiring the lock.
    
    Use notify() when only one waiting thread should resume, and notifyAll() when **any** of the waiting threads could proceed safely. Overusing notifyAll() can cause performance issues due to unnecessary context switching.
      


---

### **🧺 Collections Framework**

**156. What are the differences between Vector and ArrayList?**

- **Synchronization**: Vector is synchronized (thread-safe), ArrayList is not.
    
- **Performance**: ArrayList is faster in single-threaded environments due to no synchronization overhead.
    
- **Growth policy**: Vector doubles size when capacity is exceeded; ArrayList grows by 50%.
    
- **Legacy**: Vector is a legacy class (pre-Java 1.2), retained for backward compatibility.
    
    In modern Java, use ArrayList or Collections.synchronizedList() for thread-safe lists.
    

  
**157. What are the differences between Collection and Collections in Java?**

- **Collection**: An **interface** in java.util defining basic operations for List, Set, and Queue.
    
- **Collections**: A **utility class** in java.util that contains static methods to operate on collections (e.g., sort(), reverse(), synchronizedList()).
    
    Remember: _Collection = interface_, _Collections = helper class_.
    
  

**158. In which scenario is LinkedList better than ArrayList?**

Use LinkedList when:

- Frequent **insertions/deletions** at the beginning or middle.
    
- Constant-time insertion/removal is more important than random access.
    
    ArrayList is better for fast, indexed retrieval (O(1)), while LinkedList excels at manipulating elements (O(1) insertion/removal at ends).
    

  
**159. What are the differences between a List and a Set collection in Java?**

- **List**: Allows **duplicates**, maintains **insertion order**.
    
- **Set**: **No duplicates**, order not guaranteed (unless using LinkedHashSet or TreeSet).
    
    Use List when duplicates are needed or access by index; use Set for uniqueness and fast membership tests.
    

  
**160. What are the differences between a HashSet and a TreeSet in Java?**

|**Feature**|**HashSet**|**TreeSet**|
|---|---|---|
|Order|Unordered|Sorted (natural or custom)|
|Null allowed?|Yes (1 null element)|No (throws NPE for nulls)|
|Performance|Faster (O(1) ops)|Slower (O(log n) ops)|
|Use HashSet for performance, TreeSet when ordering is required.|||

**161. In Java, how do you decide when to use a List, Set, or Map?**

- **List**: When order and duplicates matter (e.g., shopping cart).
    
- **Set**: When uniqueness is required (e.g., usernames).
    
- **Map**: When key-value pairs are involved (e.g., configuration, dictionary).
    
    Evaluate based on access patterns, performance needs, and data semantics.
    



**162. What are the differences between a HashMap and a Hashtable in Java?**

|**Feature**|**HashMap**|**Hashtable**|
|---|---|---|
|Thread-safe?|No|Yes (synchronized)|
|Performance|Faster|Slower|
|Null keys/vals|Allows 1 null key, many null values|No null keys/values|
|Hashtable is legacy; prefer HashMap + ConcurrentHashMap for concurrency.|||


**163. What are the differences between a HashMap and a TreeMap?**

|**Feature**|**HashMap**|**TreeMap**|
|---|---|---|
|Ordering|No specific order|Keys are sorted (natural or custom)|
|Performance|O(1) average for get/put|O(log n) using Red-Black Tree|
|Null keys|Allows one null key|Does not allow null keys|
|Backed by|Hash table|Red-Black Tree|
|Use HashMap for performance, TreeMap when ordering is required (e.g., range queries, navigation).|||

---

**164. What are the differences between Comparable and Comparator?**

|**Aspect**|**Comparable**|**Comparator**|
|---|---|---|
|Location|Implemented by class itself|External class or lambda|
|Method|compareTo(Object o)|compare(Object o1, Object o2)|
|Sorting logic|Natural/default order|Custom sorting logic|
|Use case|Single sort logic per class|Multiple sort orders possible|
|Example:|||

- String, Integer implement Comparable
    
- You pass a Comparator to Collections.sort(list, comparator) for custom sort
    

---

**165. In Java, what is the purpose of Properties file?**

A .properties file stores **key-value pairs** typically used for:

- Application configuration (URLs, DB credentials, messages)
    
- Internationalization (I18N)
    
- Environment settings
    
    It’s loaded via java.util.Properties:
    

```
Properties props = new Properties();
props.load(new FileInputStream("config.properties"));
```

---

**166. What is the reason for overriding equals() method?**

To define **logical equality** between objects.

Without overriding, equals() uses default Object implementation (i.e., reference comparison).

Collections like Set, Map, and sorting mechanisms rely on equals() to:

- Prevent duplicates
    
- Match keys in hash-based structures
    
    Override equals() when object state (not reference) determines equality.
    

---

**167. How does hashCode() method work in Java?**

It returns an integer representing the object’s memory-based hash. In hash-based collections:

- It determines the **bucket index**.
    
- hashCode() must be consistent with equals():
    
    - If a.equals(b) → a.hashCode() == b.hashCode()
        
    - But not vice versa
        
        Custom hashCode() implementations should use relevant fields and prime numbers to reduce collisions.
        
    

---

**168. Is it a good idea to use Generics in collections?**

Absolutely. Generics provide:

- **Type safety at compile time**
    
- No need for explicit casting
    
- Enhanced readability and tooling support
    
- Prevents ClassCastException at runtime
    
    Example:
    

```
List<String> list = new ArrayList<>();  // Safer than List list = new ArrayList();
```

---

### **🔄 Mixed Java Fundamentals**

  

**169. What are Wrapper classes in Java?**

Wrapper classes are **object representations of primitive types**, allowing primitives to be used in:

- Collections (which only support objects)
    
- Generics
    
- APIs requiring objects
    
    Examples: int → Integer, boolean → Boolean
    
    They offer utility methods (parseInt(), compareTo()) and enable **autoboxing/unboxing**.
    

---

**170. What is the purpose of native method in Java?**

A native method is a **Java method implemented in a non-Java language** (usually C/C++), using the native keyword.

Purpose:

- Call platform-specific libraries (e.g., graphics drivers)
    
- Access hardware or OS-level APIs
    
- Improve performance via JNI (Java Native Interface)
    

---

**171. What is System class?**

The System class in java.lang is a **final utility class** used to:

- Access system streams (in, out, err)
    
- Exit or shut down the JVM (System.exit(0))
    
- Interact with the environment (getenv(), getProperties())
    
- Suggest GC (System.gc())
    
    All members are static, and the class cannot be instantiated.
    

---

**172. What is System, out, and println in System.out.println() call?**

- System: A final class from java.lang.
    
- out: A public static field of type PrintStream.
    
- println(): A method in PrintStream that prints text followed by a newline.
    
    So System.out.println("Hi") means:
    
    “Use the standard output stream to print ‘Hi’ followed by a newline.”
    

---

**173. What is the other name of Shallow Copy in Java?**

Shallow Copy is also called **reference copy** or **field-by-field copy**, where:

- The outer object is duplicated.
    
- But its **internal objects are shared** (not deeply copied).
    

---

**174. What is the difference between Shallow Copy and Deep Copy in Java?**

- **Shallow Copy**: Copies the object’s fields, but nested objects still point to the original references.
    
- **Deep Copy**: Recursively copies all referenced objects, creating a fully independent copy.
    
    Shallow copy risks unintended modifications to shared objects.
    

---

**175. What is a Singleton class?**

A Singleton class ensures **only one instance** of itself exists per JVM.

Key elements:

- Private constructor
    
- Static private instance
    
- Public static accessor method (getInstance())
    
    Used for: logging, DB connections, shared config.
    

---

**176. What is the difference between Singleton class and Static class?**

|**Feature**|**Singleton Class**|**Static Class**|
|---|---|---|
|Instance|Only one, but still an object|No instance; only static methods|
|Inheritance|Can implement interfaces|Cannot inherit or implement|
|Flexibility|Allows lazy loading, polymorphism|No flexibility or instantiation|
|Use Singleton when object state/polymorphism is needed; use Static when just utility methods are required.|||

---

### **🔧 Core Java Collections Framework**

  

**177. What is the difference between Collection and Collections Framework in Java?**

- **Collection** is an **interface** representing a group of elements (like List, Set, Queue).
    
- **Collections Framework** is a complete **architecture** that includes:
    
    - Interfaces (List, Set, Map, Queue, Deque)
        
    - Implementations (ArrayList, HashSet, TreeMap)
        
    - Algorithms (sort, shuffle, reverse)
        
    - Utilities (Collections class, Arrays, etc.)
        
        It promotes consistency, reusability, and efficiency in handling groups of objects.
        
    

---

**178. What are the main benefits of Collections Framework in Java?**

- **Reusability**: Common structures are implemented once and reused.
    
- **Type Safety**: With generics, compile-time type checking is possible.
    
- **Performance**: Efficient data structures for different use cases.
    
- **Thread-Safety Options**: Synchronized and concurrent versions available.
    
- **Interoperability**: Unified API makes switching between implementations easy.
    

---

**179. What is the root interface of Collection hierarchy in Java?**

The **java.util.Collection** interface is the root of the Collection hierarchy.

- Extended by List, Set, Queue, and Deque.
    
- Provides core methods like add(), remove(), iterator(), and size().
    
    Note: Map is not part of Collection but is included in the Collections Framework.
    

---

**180. What are the main differences between Collection and Collections?**

|**Feature**|**Collection**|**Collections**|
|---|---|---|
|Type|Interface|Utility class|
|Package|java.util|java.util|
|Purpose|Represents group of elements|Provides static helper methods|
|Examples: List is a Collection. Collections.sort() is from the utility class.|||

---

**181. What are the Thread-safe classes in Java Collections framework?**

Legacy synchronized classes:

- Vector
    
- Hashtable
    
- Stack
    
    Modern concurrent classes:
    
- ConcurrentHashMap
    
- CopyOnWriteArrayList
    
- ConcurrentLinkedQueue
    
- BlockingQueue variants
    
    For wrappers:
    
- Collections.synchronizedList(new ArrayList<>())
    

---

**182. How will you efficiently remove elements while iterating a Collection?**

Use **Iterator’s remove()** method:

```
Iterator<String> it = list.iterator();
while (it.hasNext()) {
    if (condition(it.next())) {
        it.remove();
    }
}
```

Avoid using list.remove(x) inside a for-each loop—it leads to ConcurrentModificationException.

---

**183. How will you convert a List into an array of integers like int[]?**

Using Java 8+ Streams:

```
List<Integer> list = Arrays.asList(1, 2, 3);
int[] arr = list.stream().mapToInt(Integer::intValue).toArray();
```

This avoids manual unboxing and works efficiently.

---

**184. How will you convert an array of primitive integers int[] to a List collection?**

Use:

```
int[] arr = {1, 2, 3};
List<Integer> list = Arrays.stream(arr).boxed().collect(Collectors.toList());
```

You can’t use Arrays.asList(arr) directly—it treats int[] as a single object.

---

**185. How will you run a filter on a Collection?**

Use Stream API:

```
List<String> filtered = list.stream()
    .filter(s -> s.startsWith("A"))
    .collect(Collectors.toList());
```

This is concise, functional, and efficient.

---

**186. How will you convert a List to a Set?**

```
List<String> list = Arrays.asList("a", "b", "a");
Set<String> set = new HashSet<>(list);
```

This removes duplicates automatically. For order preservation, use LinkedHashSet.

---

**187. How will you remove duplicate elements from an ArrayList?**

Convert it to a Set:

```
List<String> list = new ArrayList<>(Arrays.asList("x", "y", "x"));
List<String> unique = new ArrayList<>(new LinkedHashSet<>(list));
```

LinkedHashSet retains the insertion order.

---

**188. How can you maintain a Collection with elements in Sorted order?**

Use:

- TreeSet – sorted, no duplicates.
    
- PriorityQueue – heap-based sorted insertion.
    
- TreeMap – sorted keys.
    
- Manual sort: Collections.sort(list) or list.sort(comparator).
    

---

**189. What is the difference between Collections.emptyList() and creating a new instance of Collection?**

|**Feature**|Collections.emptyList()|new ArrayList<>()|
|---|---|---|
|Mutability|Immutable|Mutable|
|Memory|Lightweight singleton|New object|
|Use Case|Return value|List building|
|Use emptyList() when returning unmodifiable empty results.|||

---

**190. How will you copy elements from a Source List to another list?**

Use:

```
List<String> source = Arrays.asList("A", "B");
List<String> dest = new ArrayList<>(Arrays.asList("", ""));
Collections.copy(dest, source);
```

Destination list must be **pre-sized**. Alternatively, use addAll() for append:

```
dest.addAll(source);
```

---

### **🧾 Class Implementations & Structures**

  

**191. What are the Java Collection classes that implement List interface?**

- ArrayList
    
- LinkedList
    
- Vector
    
- Stack (subclass of Vector)
    
- CopyOnWriteArrayList
    

---

**192. What are the Java Collection classes that implement Set interface?**

- HashSet
    
- LinkedHashSet
    
- TreeSet
    
- CopyOnWriteArraySet
    
- EnumSet
    

---

**193. What is the difference between an Iterator and ListIterator in Java?**

|**Feature**|**Iterator**|**ListIterator**|
|---|---|---|
|Direction|Forward only|Bidirectional|
|Index Access|No|Yes (previousIndex(), nextIndex())|
|Modification|Remove only|Add, remove, and set|
|ListIterator is specific to List types and useful for in-place editing.|||

---

**194. What is the difference between Iterator and Enumeration?**

|**Feature**|**Enumeration**|**Iterator**|
|---|---|---|
|Legacy?|Yes (pre-1.2)|No|
|Remove?|No|Yes (remove())|
|Fail-fast?|No|Yes|
|Use Iterator in all modern code; Enumeration is only for legacy classes like Vector.|||

---

**195. What is the difference between an ArrayList and a LinkedList data structure?**

|**Feature**|**ArrayList**|**LinkedList**|
|---|---|---|
|Access|O(1)|O(n)|
|Insert/Delete (middle)|Slow|Fast|
|Memory|Compact|High (node overhead)|
|Use ArrayList for frequent reads; LinkedList for frequent insertions/deletions.|||

---

**196. What is the difference between a Set and a Map in Java?**

- **Set**: Stores unique values.
    
- **Map**: Stores key-value pairs with unique keys.
    
    Use Set for membership checks; Map for lookup by key. Internally, HashSet uses HashMap.
    

---

**197. What is the use of a Dictionary class?**

Dictionary is a **legacy abstract class** used to store key-value pairs. It’s been replaced by the **Map interface**. Its only concrete subclass is Hashtable. Use Map, HashMap, or ConcurrentHashMap in modern code.

---

**198. What is the default size of load factor in a HashMap collection in Java?**

The default load factor is **0.75**.

This means the HashMap resizes when 75% of the capacity is filled, balancing memory and lookup performance.

---

**199. What is the significance of load factor in a HashMap in Java?**

Load factor controls the **threshold for resizing**.

- Lower load factor = fewer collisions = more space used
    
- Higher load factor = more collisions = slower lookups
    
    Proper tuning improves performance in large-scale hash-based structures.
    

---

**200. What are the major differences between a HashSet and a HashMap?**

|**Feature**|**HashSet**|**HashMap**|
|---|---|---|
|Internal Implementation|Backed by HashMap|Stores key-value pairs|
|Value|Keys only|Key + Value|
|Null|Allows one null element|Allows one null key, many null values|
|Use HashSet for uniqueness; HashMap for key-value associations.|||


---

Absolutely! Here’s an **in-depth, technically rich set of answers** to questions 201–220 covering collections, iteration, hashing, and concurrency in Java. These will help you not only revise but also impress in interviews.

---

### **201. What are the similarities between a HashSet and a HashMap in Java?**

- Both are part of the **Java Collections Framework** and use a **hash table** as the underlying data structure.
    
- Both use **hashing techniques** to store and retrieve elements, ensuring average time complexity of **O(1)** for add, remove, and contains operations.
    
- **HashSet** is internally backed by a **HashMap** — when you add an element to a HashSet, it actually inserts it into a backing HashMap as a key, with a dummy value (PRESENT object).
    
- Both rely on correctly overridden hashCode() and equals() methods of the objects being stored or used as keys.
    

---

### **202. What is the reason for overriding equals() method?**

- To provide **logical equality** rather than reference equality (==).
    
- When you store objects in **collections like Set, Map**, etc., Java uses equals() (along with hashCode()) to determine **object uniqueness**.
    
- If equals() is not overridden properly:
    
    - Set may allow duplicates.
        
    - Map may not retrieve the correct value for a key.
        
    
- Failing to override both equals() and hashCode() consistently breaks the **contract** and leads to unpredictable behavior.
    

---

### **203. How can we synchronize the elements of a List, a Set or a Map?**

  

There are **3 ways** to make collections thread-safe:

1. **Using Collections.synchronizedXxx():**
    

```
List<String> syncList = Collections.synchronizedList(new ArrayList<>());
Map<String, String> syncMap = Collections.synchronizedMap(new HashMap<>());
```

1. - Uses intrinsic locking (synchronized) internally.
        
    - Requires manual synchronization during iteration.
        
    
2. **Using Concurrent Collections (Preferred):**
    
    - CopyOnWriteArrayList, ConcurrentHashMap, ConcurrentSkipListSet — optimized for concurrency.
        
    - No need for external synchronization.
        
    
3. **Using synchronized blocks manually:**
    

```
synchronized(syncList) {
    for (String s : syncList) {
        // thread-safe iteration
    }
}
```

  

---

### **204. What is Hash Collision? How does Java handle hash collisions in HashMap?**

- A **hash collision** occurs when **different keys generate the same hash code**, causing them to map to the same bucket index.
    
- Java handles this using:
    
    - **Chaining** (before Java 8): Collided entries are stored in a **linked list** at that bucket.
        
    - **Treeing** (since Java 8): When collisions in a bucket exceed a threshold (TREEIFY_THRESHOLD = 8), the list is converted into a **balanced Red-Black Tree** for **O(log n)** performance.
        
    

---

### **205. What are the Hash Collision resolution techniques?**

  

Java uses **chaining**, but common techniques include:

1. **Chaining** (Used in Java’s HashMap)
    
    - Store multiple entries in the same bucket via a linked list or tree.
        
    
2. **Open Addressing**
    
    - Find next available bucket using a probing strategy:
        
        - Linear probing
            
        - Quadratic probing
            
        - Double hashing
            
        
    
3. **Rehashing**
    
    - Resize the hash table and recalculate positions to reduce collisions.
        
    

---

### **206. What is the difference between Queue and Stack data structures?**

|**Feature**|**Stack**|**Queue**|
|---|---|---|
|Ordering|LIFO (Last In First Out)|FIFO (First In First Out)|
|Common Methods|push(), pop(), peek()|offer(), poll(), peek()|
|Java Class|java.util.Stack|java.util.Queue, Deque|
|Use Case|Undo operations, recursion|Scheduling, buffering|

---

### **207. What is an Iterator in Java?**

- Iterator is an **interface** used to iterate over collections.
    
- Defined in java.util and supports:
    
    - hasNext(): Checks if more elements exist.
        
    - next(): Returns the next element.
        
    - remove(): Removes the last element returned (optional operation).
        
    

  

> It is **fail-fast**, meaning it throws ConcurrentModificationException if the collection is modified structurally after the iterator is created (except via iterator’s own remove() method).

---

### **208. What is the difference between Iterator and Enumeration in Java?**

|**Feature**|**Enumeration**|**Iterator**|
|---|---|---|
|Package|java.util|java.util|
|Methods|hasMoreElements(), nextElement()|hasNext(), next(), remove()|
|Remove support|No|Yes|
|Fail-fast|No|Yes|
|Usage|Legacy classes like Vector|Modern collections|

---

### **209. What is the design pattern used in the implementation of Enumeration in Java?**

- **Iterator Pattern** — It provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation.
    
- Although Enumeration is a legacy version, it still follows the core idea of the iterator design pattern.
    

---

### **210. Which methods do we need to override to use an object as a key in a HashMap?**

- hashCode(): For computing the hash bucket index.
    
- equals(): For verifying key equality in case of hash collisions.
    

  

**Contract to follow:**

- If a.equals(b) is true, then a.hashCode() == b.hashCode() **must** be true.
    
- Failing to follow this contract can break HashMap logic (retrieval, duplication).
    

---

### **211. How will you reverse a List in Java?**

- Using Collections.reverse():
    

```
List<Integer> list = Arrays.asList(1, 2, 3);
Collections.reverse(list);
```

-   
    
- Using Stream:
    

```
List<Integer> reversed = list.stream()
    .collect(Collectors.collectingAndThen(
        Collectors.toList(), l -> {
            Collections.reverse(l);
            return l;
        }));
```

-   
    
- Using manual iteration or ListIterator from the end.
    

---

### **212. How will you convert an array of String objects into a List?**

- Using Arrays.asList():
    

```
String[] arr = {"a", "b"};
List<String> list = Arrays.asList(arr);
```

  

  

> Note: The list is **backed by the array** — not resizable.

  

- To get a resizable list:
    

```
List<String> modifiableList = new ArrayList<>(Arrays.asList(arr));
```

  

---

### **213. What is the difference between peek(), poll() and remove() in Queue?**

|**Method**|**Returns Element**|**Behavior if Empty**|
|---|---|---|
|peek()|Head (non-destructive)|Returns null|
|poll()|Head (destructive)|Returns null|
|remove()|Head (destructive)|Throws NoSuchElementException|

- Use peek() when you just want to view.
    
- Use poll() when safe remove is needed.
    
- Use remove() when failure on empty queue is expected.
    

---

### **214. What is the difference between Array and ArrayList in Java?**

|**Feature**|**Array**|**ArrayList**|
|---|---|---|
|Size|Fixed|Dynamic|
|Type|Can store primitives|Stores only objects|
|Performance|Faster (less overhead)|Slightly slower|
|Methods|No utility methods|Rich API (add, remove, etc.)|
|Multidim.|Supports|Indirect via nested lists|
|Thread-safe|No|No (Use Collections.synchronizedList)|

---

### **215. How will you insert, delete and retrieve elements from a HashMap in Java?**

- **Insert:**
    

```
map.put(key, value);
```

-   
    
- **Delete:**
    

```
map.remove(key);
```

-   
    
- **Retrieve:**
    

```
map.get(key);
```

-   
    
- **Check existence:**
    

```
map.containsKey(key);
map.containsValue(value);
```

-   
    
- Time Complexity: **O(1)** (average), but **O(n)** in worst case (hash collisions).
    

---

### **216. What are the main differences between HashMap and ConcurrentHashMap in Java?**

|**Feature**|**HashMap**|**ConcurrentHashMap**|
|---|---|---|
|Thread Safety|No|Yes|
|Performance|Fast (non-synchronized)|Scalable with thread safety|
|Null Keys/Values|One null key, many null values|No null key or value|
|Locking Mechanism|Not applicable|Segment/Node level locking (before Java 8), synchronized blocks post Java 8|

Use ConcurrentHashMap in multithreaded environments.

---

### **217. What is the increasing order of performance for following collection classes in Java?**

  

Assuming normal access:

  

**Vector < Stack < Hashtable < SynchronizedList < ArrayList < HashMap < ConcurrentHashMap < CopyOnWriteArrayList**

  

However, **performance depends on use case**:

- For reads → CopyOnWriteArrayList may perform best.
    
- For writes → ArrayList or HashMap are fastest.
    
- For concurrency → ConcurrentHashMap wins.
    

---

### **218. Why does Map interface not extend Collection interface in Java?**

- Map represents a **key-value pair**, while Collection represents **a group of elements**.
    
- Conceptually incompatible: Collection<E> has a single element type, Map<K, V> has two.
    Operations like add(E) in Collection don’t make sense for a Map.
    
    To avoid forcing Map to support irrelevant operations, **Map was made separate** from the Collection hierarchy.


---

## **✅ 219. What are the different ways to iterate elements of a list in Java?**

```
List<String> list = Arrays.asList("A", "B", "C");
```

|**Method**|**Example**|**Notes**|
|---|---|---|
|**For loop (index-based)**|for (int i = 0; i < list.size(); i++) { list.get(i); }|Allows accessing index|
|**Enhanced for loop**|for (String item : list) { System.out.println(item); }|Simpler syntax|
|**Iterator**|Iterator<String> it = list.iterator(); while(it.hasNext())|Can remove elements|
|**ListIterator**|ListIterator<String> it = list.listIterator();|Bi-directional|
|**Streams (Java 8)**|list.stream().forEach(System.out::println);|Functional, concise|
|**forEach method (Java 8)**|list.forEach(System.out::println);|Internal iteration|

> ✅ **ListIterator** is the only one that can iterate backwards (hasPrevious()).

---

## **✅ 220. What is CopyOnWriteArrayList? How is it different from ArrayList in Java?**

  

CopyOnWriteArrayList is a thread-safe variant of ArrayList in the java.util.concurrent package.

  

### **🚀 Differences:**

|**Feature**|**ArrayList**|**CopyOnWriteArrayList**|
|---|---|---|
|**Thread-safe**|❌ No|✅ Yes (via copy-on-write)|
|**Read performance**|Fast|Fast (read is lock-free)|
|**Write performance**|Fast|Slower (copies whole array on mutation)|
|**Use case**|Single-threaded or external sync|Frequent reads, infrequent writes|

```
CopyOnWriteArrayList<String> list = new CopyOnWriteArrayList<>();
list.add("A");
list.remove("A");
```

> ✅ Ideal when iteration is more frequent than mutation. Iterators do **not** throw ConcurrentModificationException.

---

## **✅ 221. How is remove() method implemented in a HashMap?**

```
public V remove(Object key) {
    Node<K,V> node = removeNode(hash(key), key, null, false, true);
    return (node == null) ? null : node.value;
}
```

Internally:

1. **Calculates hash** of the key.
    
2. **Finds the correct bucket** via (hash & (n - 1)).
    
3. Traverses the linked list or tree within the bucket.
    
4. Removes the node if key matches.
    
5. Returns value or null.
    

  

> ✅ If the bucket is a red-black tree (after threshold), removal follows tree balancing logic.

---

## **✅ 222. What is BlockingQueue in Java Collections?**

  

A BlockingQueue supports **thread-safe insertion and retrieval**, blocking if necessary.

```
BlockingQueue<String> queue = new ArrayBlockingQueue<>(10);

// Producer
queue.put("data");

// Consumer
String data = queue.take();
```

|**Feature**|**Description**|
|---|---|
|**put()**|Blocks if queue is full|
|**take()**|Blocks if queue is empty|
|**poll(timeout)**|Waits for timeout if empty|

### **🧠 Popular Implementations:**

- ArrayBlockingQueue
    
- LinkedBlockingQueue
    
- PriorityBlockingQueue
    
- DelayQueue
    
- SynchronousQueue
    

  

> ✅ Used in **producer-consumer** problems and **thread pools** (ExecutorService).

---

## **✅ 223. How is TreeMap class implemented in Java?**

  

TreeMap is a **Red-Black Tree** implementation of the NavigableMap interface.

  

### **🧱 Properties:**

- **Sorted** by natural order or a custom Comparator.
    
- Guarantees **log(n)** time for put, get, remove.
    

```
TreeMap<String, Integer> map = new TreeMap<>();
map.put("apple", 10);
map.put("banana", 5);
```

### **⚙️ Internal Structure:**

```
Red-Black Tree:
- Self-balancing BST
- Ensures O(log n) height
- No two consecutive red nodes
- Root is always black
```

> ✅ Use TreeMap when you need sorted keys or range-based operations (subMap, headMap, tailMap).

---

## **✅ 224. What is the difference between Fail-fast and Fail-safe iterator in Java?**

|**Feature**|**Fail-Fast**|**Fail-Safe**|
|---|---|---|
|**Throws Exception**|Yes – ConcurrentModificationException|No|
|**Underlying Copy**|No|Yes (usually clone or snapshot)|
|**Examples**|ArrayList, HashMap|CopyOnWriteArrayList, ConcurrentHashMap|
|**Safe in Concurrency**|❌|✅|

```
// Fail-Fast
List<String> list = new ArrayList<>();
Iterator<String> it = list.iterator();
list.add("new"); // ❌ ConcurrentModificationException

// Fail-Safe
CopyOnWriteArrayList<String> safeList = new CopyOnWriteArrayList<>();
for (String item : safeList) {
    safeList.add("new"); // ✅ No exception
}
```

---

## **✅ 225. How does ConcurrentHashMap work in Java?**

  

It is a **highly concurrent** map implementation introduced in java.util.concurrent.

  

### **⚙️ Internal Mechanics:**

- Pre-Java 8: Segment locking (16 segments)
    
- Java 8+: Uses **synchronized blocks** and **CAS (Compare-And-Swap)** with Node[] table
    

```
ConcurrentHashMap<String, Integer> map = new ConcurrentHashMap<>();
map.put("A", 1);
map.computeIfAbsent("B", k -> 2);
```

|**Feature**|**Details**|
|---|---|
|**Thread-safe**|✅ Uses fine-grained locking|
|**Null keys/values**|❌ Not allowed|
|**Iterators**|Weakly consistent (no ConcurrentModificationException)|

> ✅ Perfect for multi-threaded environments with high read-write performance needs.

---

## **✅ 226. What is the importance of hashCode() and equals() methods?**

  

These methods define **object equality** and are critical for using objects in **Hash-based collections**.

  

### **Example:**

```
@Override
public boolean equals(Object o) {
    // Logical equality
}

@Override
public int hashCode() {
    // Consistent hash code
}
```

> ✅ Used in HashMap, HashSet, Hashtable, etc. Incorrect implementations cause **data loss**, **wrong lookups**, and **performance issues**.

---

## **✅ 227. What is the contract of hashCode() and equals() methods in Java?**

  

### **🔐 Contract of equals():**

- Reflexive: x.equals(x) is true
    
- Symmetric: x.equals(y) ⇒ y.equals(x)
    
- Transitive: x.equals(y) and y.equals(z) ⇒ x.equals(z)
    
- Consistent: Multiple invocations ⇒ same result
    
- Null: x.equals(null) must return false
    

  

### **🔐 Contract of hashCode():**

- Equal objects must return same hash code
    
- Unequal objects can have same or different hash codes
    

  

> ✅ If you override one, **you must override both**.

---

## **✅ 228. What is an EnumSet in Java?**

  

A **high-performance Set** for use with **Enums** only.
```
enum Day { MON, TUE, WED }

EnumSet<Day> days = EnumSet.of(Day.MON, Day.WED);
```


| **Feature**           | **Value** |
| --------------------- | --------- |
| Backed by bit vectors | ✅         |
| Null not allowed      | ✅         |
| Fast iteration        | ✅         |
| Space-efficient       | ✅         |
 > ✅ Much faster and compact than HashSet<Enum>.


  



