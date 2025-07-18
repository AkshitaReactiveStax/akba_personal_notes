You’re nailing it, Akshita! Here’s the **complete, blame-proof Generics Interview Checklist** for Java — including all subtle edge cases and advanced topics that interviewers **love** to throw in to test real understanding.

---

## **✅ JAVA GENERICS INTERVIEW MASTER LIST**

  

_Covers syntax, wildcards, type bounds, inheritance issues, and tricky behavior_

---

### **🔹 1.** 

### **Generic Classes and Methods**

- Declaring a generic class: class Box<T> { ... }
    
- Generic constructor vs generic method:
    

```
public <T> void print(T item) { ... }
```

-   
    
- Generic arrays (why T[] is tricky)
    
- Multiple type parameters: <K, V>
    

  

🧠 _Q_: Can you write a generic method in a non-generic class?

---

### **🔹 2.** 

### **Bounded Type Parameters**

- T extends Number → upper bound
    
- Multiple bounds: <T extends Number & Comparable<T>>
    
- T super Integer (invalid – only upper bounds allowed for T)
    
- Use of interfaces in bounds
    

  

🧠 _Q_: Can a generic have both class and interface bounds?

---

### **🔹 3.** 

### **Wildcards (?, ? extends, ? super)**

- <?>: unbounded wildcard
    
- <? extends T>: upper-bounded wildcard (covariance)
    
    - You can **read**, but not **write**
        
    
- <? super T>: lower-bounded wildcard (contravariance)
    
    - You can **write**, but not **read**
        
    
- PECS Principle:
    
    - **P**roducer → extends
        
    - **C**onsumer → super
        
    

  

🧠 _Q_: Why can’t we add elements to a List<? extends Number>?

---

### **🔹 4.** 

### **Type Erasure**

- How generics are implemented (via erasure)
    
- No runtime type information (can’t check if (obj instanceof List<String>))
    
- No generic arrays: new T[] → compile error
    
- Bridge methods (due to erasure + inheritance)
    

  

🧠 _Q_: Can you overload methods that differ only in their generic type?

---

### **🔹 5.** 

### **Generics and Inheritance**

- List<String> is **not** a subtype of List<Object>
    
- Invariance of generic types
    
- Use wildcards to support polymorphism
    

  

🧠 _Q_: Why isn’t List<Integer> assignable to List<Number>?

---

### **🔹 6.** 

### **Generic Interfaces and Abstract Classes**

- Implementing Comparable<T>, Iterator<T>, Supplier<T>
    
- Creating your own generic interfaces
    
- Type parameter inference with interfaces
    

  

🧠 _Q_: How would you implement a custom generic Repository<T, ID>?

---

### **🔹 7.** 

### **Raw Types vs Generic Types**

- What are raw types?
    
- Backward compatibility with pre-Java 5 code
    
- Risks of using raw types (type safety, ClassCastException)
    
- Compiler warnings (unchecked)
    

  

🧠 _Q_: What happens if I assign a List<String> to a raw List?

---

### **🔹 8.** 

### **Generic Constructors**

- Constructor can have its own generic type unrelated to the class:
    

```
class Demo {
    <T> Demo(T val) { ... }
}
```

  

  

🧠 _Q_: Can a generic method define its own type parameter even if the class is already generic?

---

### **🔹 9.** 

### **Generic Utility Methods**

- Swapping elements in an array
    
- Copying from one list to another using wildcards
    
- Creating a typed map from varargs
    

  

🧠 _Q_: Can you write a method to copy one list to another using wildcards?

---

### **🔹 10.** 

### **Advanced Tricky Questions**

- Recursive bounds: <T extends Comparable<T>>
    
- Differences between T[] and List<T>
    
- Wildcards in method return vs argument
    
- Intersection types
    
- Generic method references in streams
    

---

Would you like example questions or real code snippets to explain concepts like **PECS**, **recursive bounds**, or **type erasure behavior**?




https://engineeringdigest.medium.com/generics-b158a743d18f
engineering digest - generics notes link 

https://www.youtube.com/watch?v=UypoeUL4T_U
engineering digest - youtube lecture 