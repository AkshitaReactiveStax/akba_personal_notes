### Comparing Inner Class, Nested Class, and Anonymous Class

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture18-java8-features.md#comparing-inner-class-nested-class-and-anonymous-class)

| Feature                 | Inner Class                                               | Nested Class                        | Anonymous Class                                           |
| ----------------------- | --------------------------------------------------------- | ----------------------------------- | --------------------------------------------------------- |
| **Type**                | Non-static                                                | Static                              | Nameless                                                  |
| **Access to Outer**     | Has access to all outer class members (including private) | Can access only static members      | Has access to all outer class members (including private) |
| **Instance Dependency** | Requires outer class instance                             | Independent of outer class instance | Defined and instantiated together                         |
| **Use Case**            | Tied to the outer class's instance behavior               | Helper or utility class             | One-off implementation of interfaces or classes           |
| **Reusability**         | Can be reused across outer class methods                  | Can be reused anywhere              | Cannot be reused                                          |
| **Syntax**              | Explicit class declaration                                | Explicit static class declaration   | Declared inline with instantiation                        |



### Common Functional Interfaces in Java 8

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture18-java8-features.md#common-functional-interfaces-in-java-8)

| **Functional Interface** | **Function Descriptor** | **Primitive Specializations**                                                 |
| ------------------------ | ----------------------- | ----------------------------------------------------------------------------- |
| **Predicate**            | `T -> boolean`          | `IntPredicate`, `LongPredicate`, `DoublePredicate`                            |
| **Consumer**             | `T -> void`             | `IntConsumer`, `LongConsumer`, `DoubleConsumer`                               |
| **Function<T, R>**       | `T -> R`                | `IntFunction<R>`, `IntToDoubleFunction`, `IntToLongFunction`                  |
|                          |                         | `LongFunction<R>`, `LongToDoubleFunction`, `LongToIntFunction`                |
|                          |                         | `DoubleFunction<R>`, `ToIntFunction<T>`, `ToDoubleFunction<T>`                |
|                          |                         | `ToLongFunction<T>`                                                           |
| **Supplier**             | `() -> T`               | `BooleanSupplier`, `IntSupplier`, `LongSupplier`, `DoubleSupplier`            |
| **UnaryOperator**        | `T -> T`                | `IntUnaryOperator`, `LongUnaryOperator`, `DoubleUnaryOperator`                |
| **BinaryOperator**       | `(T, T) -> T`           | `IntBinaryOperator`, `LongBinaryOperator`, `DoubleBinaryOperator`             |
| **BiPredicate<L, R>**    | `(L, R) -> boolean`     | -                                                                             |
| **BiConsumer<T, U>**     | `(T, U) -> void`        | `ObjIntConsumer<T>`, `ObjLongConsumer<T>`, `ObjDoubleConsumer<T>`             |
| **BiFunction<T, U, R>**  | `(T, U) -> R`           | `ToIntBiFunction<T, U>`, `ToLongBiFunction<T, U>`, `ToDoubleBiFunction<T, U>` |
|                          |                         |                                                                               |
|                          |                         |                                                                               |
|                          |                         |                                                                               |

Type inference in Java is a powerful feature introduced with lambda expressions in Java 8, allowing the compiler to deduce the types of lambda parameters and other expressions based on the context. This feature improves code readability and reduces the verbosity of parameter declarations.

Here’s a deeper dive into how type inference works and why it’s useful:

### 1. **Context-Based Deduction of Functional Interfaces**
   When you write a lambda expression, Java doesn’t require you to specify the types of the parameters. Instead, the compiler deduces the types based on the surrounding context, specifically through what’s called the *target type*—the type that Java expects the lambda expression to conform to based on its use.

   Since lambdas work with functional interfaces (interfaces with a single abstract method), the compiler can determine which functional interface a lambda should implement, which in turn provides the type information for its parameters.

   For example:
   
   ```java
   List<Apple> greenApples = filter(inventory, a -> "green".equals(a.getColor()));
   ```
   
   Here, `filter` might be a method expecting a `Predicate<Apple>`. The compiler understands that `a` is of type `Apple` because it’s passed as an argument to a method that takes a `Predicate<Apple>`. Since `Predicate<Apple>` has a method `boolean test(Apple a)`, the compiler infers that `a` must be an `Apple`.

### 2. **Inferring Lambda Parameters**
   Because the compiler knows the expected functional interface and its method, it can also infer the types of parameters within the lambda. In the above example, you don’t need to explicitly declare `a` as an `Apple` because the compiler already deduces this. This reduces boilerplate code, making the lambda shorter and easier to read.

   **Example**:
   ```java
   Comparator<Apple> c = (a1, a2) -> a1.getWeight().compareTo(a2.getWeight());
   ```
   In this example, `a1` and `a2` are inferred to be of type `Apple` because the `Comparator<Apple>` interface’s method `compare` has the signature `int compare(Apple a1, Apple a2)`.

### 3. **Simplified Syntax**
   Java allows additional simplifications when working with single-parameter lambdas. If a lambda has just one parameter, the parentheses around that parameter can be omitted, so the following two lines are equivalent:

   ```java
   inventory.forEach((Apple a) -> System.out.println(a.getColor()));
   inventory.forEach(a -> System.out.println(a.getColor())); // Parentheses omitted
   ```

### 4. **Comparator Creation Example**
   The `Comparator` example you provided illustrates how type inference simplifies code. Without inference, you’d specify the types of the parameters explicitly:

   ```java
   Comparator<Apple> c = (Apple a1, Apple a2) -> a1.getWeight().compareTo(a2.getWeight());
   ```

   With type inference, the types (`Apple`) are automatically deduced, making the code cleaner:

   ```java
   Comparator<Apple> c = (a1, a2) -> a1.getWeight().compareTo(a2.getWeight());
   ```

### 5. **Benefits and Readability**
   - **Readability**: Type inference often makes code more concise and readable, particularly in functional programming styles where lambdas may have multiple parameters.
   - **Selective Type Inclusion**: While inferred types generally improve readability, there are times when explicitly including types can clarify code. Developers can choose when to use explicit types based on readability.

   For example, if the logic within the lambda is complex, showing parameter types might help readers understand the lambda’s purpose more quickly. 

Overall, type inference in Java 8 is about balancing clarity and conciseness, allowing developers to focus on business logic without being distracted by explicit type declarations unless they’re truly necessary.




#ExecuteAroundPattern

   The "Execute Around Pattern" is a way to handle resources (like files, databases, or network connections) while simplifying the setup and cleanup steps so you can focus only on the main processing logic. In Java, this pattern can be applied with the help of lambdas and functional interfaces, making code cleaner and more flexible. Here’s a breakdown of the key ideas to help clarify how this works.

### The Problem

When working with resources, you usually need to:
1. **Open** the resource (like a file).
2. **Process** it (like reading data).
3. **Close** the resource to free up memory.

Here’s an example where we’re reading a line from a file. The setup (opening the file) and cleanup (closing the file) are always the same, but the actual processing logic might vary (reading a line, counting characters, etc.).

### Example of the Execute Around Pattern

Let’s say you want to read the first line from a file, "data.txt":

```java
public static String processFile() throws IOException {
    try (BufferedReader br = new BufferedReader(new FileReader("data.txt"))) {
        return br.readLine(); // This is the main processing step.
    }
}
```

The setup (`new BufferedReader(...)`) and cleanup (the `try-with-resources` block that closes the file) are always the same. The part inside (`br.readLine()`) is where the main processing happens. But this code only reads one line, and if you need to read two lines or change the behavior, you’d have to rewrite it.

### Solution: Using Behavior Parameterization

To make the code more flexible, we can pass different behaviors to the `processFile` method. In other words, we’ll parameterize the behavior of what we want to do with the `BufferedReader`. Instead of hardcoding `br.readLine()`, we can let the caller decide what should be done, like reading the first line, the first two lines, etc.

#### Step 1: Passing Different Behaviors with Lambdas

We want a method that can take a `BufferedReader` and return a `String`. Here’s a sample of how we’d read two lines with a lambda:

```java
String result = processFile((BufferedReader br) -> br.readLine() + br.readLine());
```

The lambda `(BufferedReader br) -> br.readLine() + br.readLine()` defines a specific behavior for reading the first two lines.

#### Step 2: Create a Functional Interface

For lambdas to work, they must match a **functional interface**—an interface with a single abstract method. In this case, we’ll create an interface called `BufferedReaderProcessor` that takes a `BufferedReader` and returns a `String`.

```java
@FunctionalInterface
public interface BufferedReaderProcessor {
    String process(BufferedReader b) throws IOException;
}
```

This interface has a single method `process` that accepts a `BufferedReader` and returns a `String`.

#### Step 3: Update the `processFile` Method

Now, we’ll rewrite `processFile` so it accepts any behavior that matches the `BufferedReaderProcessor` interface. This allows us to pass different lambdas to perform various operations:

```java
public static String processFile(BufferedReaderProcessor p) throws IOException {
    try (BufferedReader br = new BufferedReader(new FileReader("data.txt"))) {
        return p.process(br); // Process the file based on the lambda behavior
    }
}
```

Here, `p.process(br)` executes the specific behavior we pass (e.g., read one line, read two lines, etc.).

#### Step 4: Using Lambdas to Specify Different Behaviors

Now, we can reuse `processFile` with different lambdas to perform various tasks:

```java
// Read just the first line
String oneLine = processFile((BufferedReader br) -> br.readLine());
System.out.println("First Line: " + oneLine);

// Read the first two lines
String twoLines = processFile((BufferedReader br) -> br.readLine() + br.readLine());
System.out.println("First Two Lines: " + twoLines);

// Read the first line in uppercase
String upperCaseLine = processFile((BufferedReader br) -> br.readLine().toUpperCase());
System.out.println("Uppercase First Line: " + upperCaseLine);

// Count the characters in the first line
int charCount = processFile((BufferedReader br) -> br.readLine().length());
System.out.println("Character Count of First Line: " + charCount);
```

In each case, `processFile` handles opening and closing the file, while the lambda provides the custom behavior.

### Benefits of the Execute Around Pattern with Lambdas

1. **Increased Flexibility**: You can pass different behaviors easily, allowing `processFile` to handle a variety of tasks without modification.
2. **Reduced Boilerplate**: The setup and cleanup code only needs to be written once.
3. **Reusability**: The core code of `processFile` remains unchanged, making it useful for many file-processing tasks.

In summary, the Execute Around Pattern with lambdas allows you to separate setup and cleanup from the main logic, letting you focus on what should be done with the resource instead of how to manage it. This makes your code modular, flexible, and concise.

## Optional

When a value is present, the `Optional` class just wraps it. Conversely, the absence of a value is modeled with an "empty" optional returned by the method `Optional.empty`. It’s a static factory method that returns a special singleton instance of the `Optional` class. Semantically, a `null` reference and `Optional.empty()` could be seen as the same thing, but in practice, the difference is huge: trying to dereference `null` will invariably cause a `NullPointerException`, whereas `Optional.empty()` is a valid, workable object of type `Optional` that can be invoked in useful ways.





link to project requirements for movie suggesting system  :
https://chatgpt.com/share/6758a443-3700-8010-a719-d7cd65e43228




notes :

| **Aspect**  <br>             | Comparable                                             | Comparator                            |
| ---------------------------- | ------------------------------------------------------ | ------------------------------------- |
| **Purpose**                  | Used for natural ordering of objects.                  | Used for custom ordering of objects.  |
| **Implementation**           | Implemented by the class of the object to be compared. | Implemented in a separate class.      |
| Method                       | compareTo(Object o)                                    | compare(Object o1, Object o2)         |
| **Method Location**          | Defined in the Comparable interface.                   | Defined in the Comparator interface.  |
| **Single/Multiple Criteria** | Suitable for single sorting logic.                     | Can handle multiple sorting criteria. |
| **Modification**             | Changes the object’s natural order.                    | Does not affect the natural order.    |
**When to Use**

1. **Use** Comparable:

• When the class has a single, natural ordering.

• Example: Sorting numbers, strings, or entities with a clear single sorting logic.

2. **Use** Comparator:

• When you need multiple ways to sort the same objects (e.g., by name, age, or ID).

• When you cannot modify the class whose objects you want to sort (e.g., sorting a third-party class).







