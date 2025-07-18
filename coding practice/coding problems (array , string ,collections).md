https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md

**Problem 1:** Find Maximum in Array Write a Java program to find the maximum value in an array of integers.

**Problem 2:** Palindrome Check Objective Write a Java program to check if a given string is a palindrome. A palindrome is a string that reads the same forward and backward, ignoring spaces, punctuation, and case differences.

Steps to Implement Palindrome Check Input the string: Take a string as input from the user. Normalize the string: Remove non-alphanumeric characters and convert it to lower case. Check for palindrome: Compare characters from the beginning and end of the string moving towards the center. If all corresponding characters match, the string is a palindrome. Output the result: Print whether the string is a palindrome or not.

**Problem 3:** Create a simple calculator that can perform basic arithmetic operations (addition, subtraction, multiplication, division).

Requirements:

Use classes to model the calculator. Use control flow statements to handle invalid operations (e.g., division by zero).

4- Print first 50 odd numbers 

5 Print first 50 even numbers 

6 Add the first 50 even numbers and print the sum 

7 Add the first 50 odd numbers and print the sum 

8 Calculate the factorial of number n (1 >> n <= 12) 

9 Print the first n number in the fibonacci series ( 1 >> n << 100) 

10 Reverse a string without using the inbuilt functions provided by the language 

11 Check if the given string is palindrome or not 

12 Read a given string and count how many times a given alphabet or number is repeated

13 Find first duplicate in an array of numbers 

14 Sum all the numbers in array 15 Sum only the Odd or Even Numbers in array

## String problems

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#string-problems)

### **Problem: Count the Vowels in a String**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#problem-count-the-vowels-in-a-string)

#### **Objective:**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#objective)

Write a Java program that counts the number of vowels in a given string.

#### **Requirements:**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#requirements)

- The program should define a method `countVowels(String input)` that takes a string as input and returns the number of vowels (a, e, i, o, u) in the string.
- The method should be case-insensitive, meaning it should count both uppercase and lowercase vowels (e.g., 'A' and 'a').
- The program should also handle an empty string input by returning 0.

#### **Example Usage:**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#example-usage)

- `countVowels("Hello World")` should return `3`.
- `countVowels("Java Programming")` should return `5`.
- `countVowels("Aeiou")` should return `5`.
- `countVowels("")` should return `0`.

### **Remove Vowels from a String**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#remove-vowels-from-a-string)

- **Objective:** Write a method that removes all vowels from a given string.
- **Requirements:**
    - The method `removeVowels(String input)` should return the string without any vowels.
- **Example Usage:**
    - `removeVowels("Hello World")` should return `"Hll Wrld"`.
    - `removeVowels("Java Programming")` should return `"Jv Prgrmmng"`.
- **Hints:**
    - Use a loop to iterate through the string and build a new string that excludes vowels.
    

### **Find the Longest Word in a String**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#find-the-longest-word-in-a-string)

- **Objective:** Write a method that finds and returns the longest word in a string.
- **Requirements:**
    - The method `findLongestWord(String input)` should return the longest word in the string.
    - If there are multiple words of the same length, return the first one.
- **Example Usage:**
    - `findLongestWord("I love programming in Java")` should return `"programming"`.
    - `findLongestWord("The quick brown fox jumps over the lazy dog")` should return `"jumps"`.
- **Hints:**
    - Use the `split(" ")` method to split the string into words and then iterate through to find the longest one.

### **Capitalize the First Letter of Each Word**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#capitalize-the-first-letter-of-each-word)

- **Objective:** Write a method that capitalizes the first letter of each word in a string.
    
- **Requirements:**
    
    - The method `capitalizeWords(String input)` should return the string with each word's first letter capitalized.
- **Example Usage:**
    
    - `capitalizeWords("hello world")` should return `"Hello World"`.
    - `capitalizeWords("java programming language")` should return `"Java Programming Language"`.
- **Hints:**
    
    - Split the string into words, capitalize each word, and then join them back together.

## Array problems

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#array-problems)

### **Check if an Array is Sorted**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#check-if-an-array-is-sorted)

- **Objective:** Write a method that checks if an array is sorted in ascending order.
- **Requirements:**
    - The method `isSorted(int[] array)` should return `true` if the array is sorted and `false` otherwise.
- **Example Usage:**
    - `isSorted(new int[]{1, 2, 3, 4})` should return `true`.
    - `isSorted(new int[]{4, 3, 2, 1})` should return `false`.
- **Hints:**
    - Compare each element with the next one to ensure the order is non-decreasing.

### **Merge Two Arrays**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#merge-two-arrays)

- **Objective:** Write a method that merges two arrays into one.
- **Requirements:**
    - The method `mergeArrays(int[] array1, int[] array2)` should return a new array containing all elements of `array1` followed by all elements of `array2`.
- **Example Usage:**
    - `mergeArrays(new int[]{1, 2}, new int[]{3, 4})` should return `[1, 2, 3, 4]`.
    - `mergeArrays(new int[]{10, 20}, new int[]{30})` should return `[10, 20, 30]`.
- **Hints:**
    - Create a new array of the combined length and copy elements from both arrays into it.

### **Find the Duplicate Elements in an Array**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#find-the-duplicate-elements-in-an-array)

- **Objective:** Write a method that finds and returns any duplicate elements in an array.
- **Requirements:**
    - The method `findDuplicates(int[] array)` should return an array of duplicates found in the input array.
- **Example Usage:**
    - `findDuplicates(new int[]{1, 2, 3, 2, 4, 3})` should return `[2, 3]`.
    - `findDuplicates(new int[]{5, 5, 5, 5})` should return `[5]`.
- **Hints:**
    - Use nested loops to compare each element with every other element.

### **Shift Elements in an Array**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#shift-elements-in-an-array)

- **Objective:** Write a method that shifts all elements of an array to the right by a specified number of positions.
- **Requirements:**
    - The method `shiftArray(int[] array, int positions)` should shift the array elements and handle wrap-around.
- **Example Usage:**
    - `shiftArray(new int[]{1, 2, 3, 4}, 2)` should modify the array to `[3, 4, 1, 2]`.
    - `shiftArray(new int[]{10, 20, 30}, 1)` should modify the array to `[30, 10, 20]`.
- **Hints:**
    - Consider how to handle the wrap-around when shifting elements.

### **Find the Smallest and Largest Elements in an Array**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#find-the-smallest-and-largest-elements-in-an-array)

- **Objective:** Write a method that finds both the smallest and largest elements in an array.
- **Requirements:**
    - The method `findMinMax(int[] array)` should return an array where the first element is the smallest and the second element is the largest.
- **Example Usage:**
    - `findMinMax(new int[]{1, 2, 3, 4, 5})` should return `[1, 5]`.
    - `findMinMax(new int[]{10, -3, 7, 2})` should return `[-3, 10]`.
- **Hints:**
    - Iterate through the array, keeping track of the smallest and largest values encountered.

### **Simple Calculator with String Expressions and Memory Operations Using Arrays**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#simple-calculator-with-string-expressions-and-memory-operations-using-arrays)

#### 1. **Basic Arithmetic Operations with String Expressions**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#1-basic-arithmetic-operations-with-string-expressions)

- **Objective:** Implement basic arithmetic operations using a single string expression that includes numbers and operators.
- **Requirements:**
    - Implement a method `calculate(String expression)` that takes a string expression like `"3.5 + 2.1"` and returns the result.
    - The method should:
        - Parse the string to identify the numbers and the operator.
        - Perform the corresponding arithmetic operation based on the operator (`+`, `-`, `*`, `/`).
        - Return the result as a `double` or an appropriate error message if the operation is invalid.
    - Handle basic operations:
        - `calculate("3.5 + 2.1")` should return `5.6`.
        - `calculate("10 - 4")` should return `6.0`.
        - `calculate("6 * 7")` should return `42.0`.
        - `calculate("8 / 2")` should return `4.0`.
    - If the expression is invalid (e.g., `"10 / 0"`), return an error message like `"Division by zero is not allowed."` or `"Invalid expression."`.

#### 2. **Handling Multiple Operations in a Single String**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#2-handling-multiple-operations-in-a-single-string)

- **Objective:** Allow the calculator to process a more complex string containing multiple arithmetic operations.
- **Requirements:**
    - Extend the `calculate(String expression)` method to handle expressions with multiple operations, like `"3 + 5 * 2 - 4 / 2"`.
    - Parse the expression and break it down into individual numbers and operators.
    - Handle operator precedence, ensuring that multiplication and division are performed before addition and subtraction.
    - Example:
        - `calculate("3 + 5 * 2 - 4 / 2")` should return `10.0`.

#### 3. **Support for Parentheses**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#3-support-for-parentheses)

- **Objective:** Enhance the calculator to support operations involving parentheses.
- **Requirements:**
    - Modify the `calculate(String expression)` method to correctly evaluate expressions with parentheses, such as `"3 + (2 * 4) - 5"`.
    - Ensure that operations within parentheses are evaluated first.
    - Example:
        - `calculate("3 + (2 * 4) - 5")` should return `6.0`.

#### 4. **Advanced Mathematical Operations with String Expressions**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#4-advanced-mathematical-operations-with-string-expressions)

- **Objective:** Extend the calculator to support advanced operations using string expressions.
- **Requirements:**
    - Implement support for functions like square root and power within string expressions.
    - Example:
        - `calculate("sqrt(16)")` should return `4.0`.
        - `calculate("2 ^ 3")` should return `8.0`.
        - Use `"^"` for exponentiation and `"sqrt"` for square root in the string expressions.

#### 5. **Memory Functionality**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#5-memory-functionality)

- **Objective:** Implement memory functions to store, recall, and clear values, including the ability to work with string expressions.
- **Requirements:**
    - Implement the following methods:
        - **Store a value in memory:** `storeInMemory(double value)`: Stores the provided `value` in a static variable.
        - **Store the result of an expression:** Modify the `calculate(String expression)` method to optionally store the result in memory if a specific command is given (e.g., `"M+"` at the end of the expression).
            - Example: `calculate("3 + 5 M+")` should calculate the result `8.0` and store it in memory.
            - implement this using stack of size 5
        - **Recall the stored value:** `recallMemory()`: Returns the last value stored in memory.
        - **Clear the stored value:** `clearMemory()`: Clears all the values stored in memory.
    - Implement a method `recallAllMemory()` if multiple memory slots are used:
        - Store up to 5 recent values in memory using an array, and return them as a string when requested.
        - `calculate("3 + 5 M+")`
        - `calculate("5 * 5 M+")`
        - `calculate("4 - 2 M+")`
        - `calculate("2 / 1 M+")`
        - `calculate("5 * 2 M+")`
        - `recallAllMemory()`
        - Example: `recallAllMemory()` could return `"Stored values: 8.0, 15.5, 42.0"`.

#### 6. **Error Handling and Input Validation**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#6-error-handling-and-input-validation)

- **Objective:** Ensure robust error handling and input validation for string expressions and memory operations.
- **Requirements:**
    - If the string contains invalid syntax (e.g., `"3 + * 2"`), return an error message like `"Invalid expression."`.
    - If the operation is not supported (e.g., `"2 ^ -3"`), return a message like `"Operation not supported."`.
    - For division by zero, square roots of negative numbers, or any invalid memory operation (e.g., recalling memory when empty), return appropriate error messages.
    - Example:
        - `calculate("10 / 0")` should return `"Division by zero is not allowed."`
        - `calculate("sqrt(-9)")` should return `"Square root of a negative number is not allowed."`
        - `recallMemory()` when memory is empty should return `"No value stored in memory."`

### Example Usage

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#example-usage-1)

- `calculate("3 + 5")` → `8.0`
- `calculate("10 - 2 * 3")` → `4.0`
- `calculate("(10 + 2) * 3")` → `36.0`
- `calculate("sqrt(25) + 3 ^ 2")` → `14.0`
- `calculate("10 / 0")` → `"Division by zero is not allowed."`
- `calculate("3 + 5 M+")` → Stores `8.0` in memory
- `recallMemory()` → Returns the stored value, e.g., `8.0`
- `clearMemory()` → Clears the stored value

### Summary

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-strings-arrays-oops.md#summary)

This enhanced **Simple Calculator** will:

- Use **String expressions** to perform operations, allowing users to input full arithmetic expressions like `"3 + 5 * 2"`.
- Handle **operator precedence** and **parentheses** to ensure correct calculation order.
- Incorporate **memory functionality**, allowing users to store, recall, and clear values, as well as perform operations that automatically store results.
- Provide **error handling** and **input validation** to manage incorrect or unsupported operations and ensure smooth operation.




https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md

### **Problem Statement: Bracket Matching without Using a Stack**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#problem-statement-bracket-matching-without-using-a-stack)

#### **Objective:**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#objective)

Design and implement a Java program that checks whether an expression containing various types of brackets (parentheses `()`, square brackets `[]`, and curly braces `{}`) is properly balanced. The challenge is to accomplish this without using a stack data structure.

#### **Requirements:**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#requirements)

1. **Bracket Types:**
    
    - The expression will contain three types of brackets: parentheses `()`, square brackets `[]`, and curly braces `{}`.
2. **Balanced Expression Criteria:**
    
    - A balanced expression is one in which every opening bracket has a corresponding closing bracket of the same type, and the brackets are correctly nested. For example, `{[()]}` is balanced, while `{[(])}` is not.
3. **Input:**
    
    - The program should accept a string consisting of only these three types of brackets.
4. **Output:**
    
    - The program should return `true` if the input string is balanced according to the standard rules, and `false` otherwise.
5. **Constraints:**
    
    - **No Stack**: The solution must be implemented without using a stack. Instead, consider alternative approaches, such as using counters.
6. **Core Functionalities:**
    
    - **Bracket Matching Logic**: Implement logic to match opening and closing brackets without relying on a stack. You may use counters for each type of bracket or simulate the stack behavior using other methods.
    - **Correct Nesting**: Ensure that the solution can correctly handle nested brackets, not just counting them but ensuring they are properly ordered.
    - **Edge Cases**: Handle edge cases such as an empty string, single bracket, and mismatched brackets correctly.
7. **Examples:**
    
    - Input: `{[()]}`, Output: `true` (balanced)
    - Input: `{[(])}`, Output: `false` (not balanced)
    - Input: `[]`, Output: `true` (balanced)
    - Input: `{[}`, Output: `false` (not balanced)
8. **Scenario Example:**
    

Imagine you are tasked with developing a simple syntax checker for a custom configuration language where brackets are used to group settings. Due to certain constraints, you are not allowed to use a stack to validate the grouping. You need to ensure that all groupings are correctly nested and balanced using an alternative method.

9. **Outcome:**

Students should be able to:

- Implement a solution to the bracket matching problem without relying on a stack.
- Explore alternative data structures or algorithms to achieve the same goal.
- Ensure the solution correctly identifies balanced and unbalanced bracket sequences and handles various edge cases effectively.

---

### **Problem Statement: Custom Balanced Brackets Validator with Stack**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#problem-statement-custom-balanced-brackets-validator-with-stack)

#### **Objective:**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#objective-1)

Design and implement a Java program that uses a stack to validate expressions containing various types of brackets. Unlike the standard balanced bracket problem, this problem allows certain "twisted" bracket sequences that would traditionally be considered unbalanced. Specifically, the sequences `{[(])}`, `{[()]}`, and other similar patterns should be considered valid.

#### **Requirements:**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#requirements-1)

1. **Bracket Types:**
    
    - The expression will contain three types of brackets: parentheses `()`, square brackets `[]`, and curly braces `{}`.
2. **Valid Sequences:**
    
    - The standard rules for balanced brackets apply, where every opening bracket must have a corresponding closing bracket, and they must be properly nested.
    - However, in this twist, certain "twisted" sequences like `{[(])}` and `{[()]}` are also considered valid.
    - Any expression that doesn't follow these patterns or is unbalanced (e.g., `{[}`) should be considered invalid.
3. **Input:**
    
    - The program should accept a string consisting of only these three types of brackets.
4. **Output:**
    
    - The program should return `true` if the input string is considered valid according to the custom rules, and `false` otherwise.
5. **Core Functionalities:**
    
    - **Stack Usage**: Use a stack to process the brackets. Push opening brackets onto the stack. For closing brackets, check for a valid match or an allowed "twist" sequence.
    - **Custom Validation Rules**: Implement logic to recognize and validate both standard and twisted sequences.
    - **Edge Cases**: Handle edge cases such as an empty string, single bracket, and mismatched brackets correctly.
6. **Examples:**
    
    - Input: `{[(])}`, Output: `true` (valid due to the custom rule)
    - Input: `{[()]}`, Output: `true` (valid due to standard balancing)
    - Input: `{[}`, Output: `false` (invalid, not balanced)
    - Input: `{[(])}()`, Output: `true` (valid, combination of twisted and standard sequences)
    
7. **Scenario Example:**
    

Imagine you are developing a tool that parses and validates complex mathematical or logical expressions. The expressions may contain different types of brackets used for grouping. However, due to certain legacy systems or specific mathematical notations, some traditionally unbalanced sequences like `{[(])}` are considered acceptable and must be recognized as valid by your validation tool.

8. **Outcome:**

Students should be able to:

- Implement a stack-based solution to validate both standard and twisted bracket sequences.
- Develop a custom validation logic that recognizes and allows specific sequences that would otherwise be considered unbalanced.
- Handle edge cases and ensure that the solution is both efficient and correct for a variety of input scenarios.

### Problem Statement: Implement a Custom `ArrayList` in Java Using Arrays

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#problem-statement-implement-a-custom-arraylist-in-java-using-arrays)

You are required to implement a custom version of the `ArrayList` in Java, called `MyArrayList`. This custom list should provide basic CRUD (Create, Read, Update, Delete) operations, dynamic resizing of the underlying array, and other commonly used list features. Your implementation must closely follow the behavior of Java's `ArrayList`, but it will use a plain Java array to store the elements internally.

### Requirements:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#requirements-2)

#### 1. Class Design:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#1-class-design)

You need to create a class named `MyArrayList` that should work with generic types (i.e., it can hold any type of object). This class must have the following functionalities:

#### 2. Constructor:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#2-constructor)

- `MyArrayList()`: Initializes the list with a default capacity (e.g., 10).
- `MyArrayList(int capacity)`: Initializes the list with a user-defined capacity.

#### 3. Methods:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#3-methods)

You must implement the following methods in `MyArrayList`:

1. **`add(T element)`**:
    
    - Adds an element to the end of the list.
    - If the internal array is full, the list should automatically double its size to accommodate more elements.
2. **`get(int index)`**:
    
    - Returns the element at the specified index.
    - If the index is out of bounds (less than 0 or greater than or equal to the size of the list), throw an `IndexOutOfBoundsException`.
3. **`remove(int index)`**:
    
    - Removes the element at the specified index.
    - After removing the element, shift all the subsequent elements to fill the gap.
    - If the index is out of bounds, throw an `IndexOutOfBoundsException`.
    - Return the element that was removed.
4. **`size()`**:
    
    - Returns the current number of elements in the list.
5. **`clear()`**:
    
    - Clears the list by removing all elements and resetting the internal array to the default capacity.
6. **`isEmpty()`**:
    
    - Returns `true` if the list contains no elements; otherwise, returns `false`.
7. **`toString()`**:
    
    - Override the `toString()` method to return a string representation of the list in the format: `[element1, element2, ...]`.
8. **`resize()`** (Helper Method):
    
    - A private method to dynamically resize the internal array when it's full. The array should grow by doubling its size when capacity is reached.

#### 4. Constraints:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#4-constraints)

- The `MyArrayList` should only use Java arrays (e.g., `Object[]`) internally to store the elements.
- Do not use any Java collection classes such as `ArrayList` or `LinkedList` to implement your solution.
- Use generics (`<T>`) so that `MyArrayList` can hold any type of object.
- Ensure that the `remove(int index)` and `get(int index)` methods perform boundary checks to prevent accessing or removing elements at invalid indices.
- Ensure efficient use of memory by resizing the array only when necessary.

### Example:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#example)

```java
public class Main {
    public static void main(String[] args) {
        MyArrayList<String> list = new MyArrayList<>();

        // Adding elements
        list.add("Apple");
        list.add("Banana");
        list.add("Cherry");

        // Print the list
        System.out.println("List: " + list); // Output: [Apple, Banana, Cherry]

        // Get an element
        System.out.println("Element at index 1: " + list.get(1)); // Output: Banana

        // Remove an element
        list.remove(1);
        System.out.println("After removal: " + list); // Output: [Apple, Cherry]

        // Check the size
        System.out.println("Size: " + list.size()); // Output: 2

        // Clear the list
        list.clear();
        System.out.println("After clear: " + list.isEmpty()); // Output: true
    }
}
```

### Additional Requirements:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#additional-requirements)

- **Resizing**: When the array reaches its capacity, the array should automatically double in size.
- **Error Handling**: Properly handle cases where invalid indices are used for the `get` or `remove` methods by throwing `IndexOutOfBoundsException`.
- **Efficiency**: Focus on making the addition of elements efficient in terms of memory and performance by resizing the array only when needed.

### Submission:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#submission)

Submit the following:

- The source code for your `MyArrayList` class with all methods properly implemented.
- A test class that demonstrates all the CRUD operations on `MyArrayList` and validates its correctness by adding, retrieving, updating, and removing elements from the list.

---

This problem requires you to understand how to manage a dynamic array manually, which is a fundamental concept in data structures. You'll learn how to handle capacity changes, manage array elements, and implement the basic operations that make Java's `ArrayList` so powerful.

### Updated Problem Statement: Implement a LinkedList in Java

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#updated-problem-statement-implement-a-linkedlist-in-java)

You are required to implement a custom **LinkedList** class in Java that mimics the behavior of a singly linked list. A singly linked list is a data structure where each element (node) points to the next element in the sequence, with the last node pointing to `null`.

Your implementation should:

1. **Support dynamic resizing**: The list should be able to grow dynamically as elements are added.
    
2. **Implement basic linked list operations**: These operations should be available:
    
    - **Add an element to the end of the list**.
    - **Add an element to the start of the list**.
    - **Remove an element from the start of the list**.
    - **Remove an element from the end of the list**.
    - **Print all elements in the list**.
3. **Handle edge cases**:
    
    - The list should be able to handle cases where operations are attempted on an empty list (e.g., removing from an empty list).
4. **Track the size of the list**: The size of the list should be maintained and returned when requested.
    
5. **Check if the list is empty**: Provide a method to check whether the list is empty.
    

### Detailed Requirements:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#detailed-requirements)

1. **Node Class**:
    - Each element in the list should be represented by a **Node** object that stores:
        - The data (integer value).
        - A reference (pointer) to the next node in the list.
2. **LinkedList Class**:
    - Should manage the head of the list (the first node) and maintain the size of the list.
    - Implement methods to manipulate the list, as specified.
3. **Error Handling**:
    - If an operation such as `removeFirst` or `removeLast` is attempted on an empty list, an appropriate error (exception) should be thrown.

### Example Scenario:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#example-scenario)

You are tasked with creating a custom linked list to store a sequence of integers. You will need to:

- Add numbers 10, 20, and 30 to the end of the list.
- Add a number 5 to the start of the list.
- Remove the first element, check the size of the list, and confirm that the correct value was removed.
- Print all the values in the list after these operations, ensuring the order of elements is maintained as expected.

### Constraints:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#constraints)

- The solution should use **singly linked list** structure.
- The list should not use any built-in collection classes like `ArrayList` or `LinkedList`.

### Problem Statement: Implement a Custom `HashMap` in Java

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#problem-statement-implement-a-custom-hashmap-in-java)

You are tasked with implementing a custom version of the `HashMap` class in Java, called `MyHashMap`. This class will store key-value pairs and provide basic operations such as adding, retrieving, removing, and checking for keys. Additionally, you are required to implement collision resolution using **chaining with linked lists**. The internal structure will use an array of buckets where each bucket is a linked list that stores key-value pairs in the event of a hash collision.

### Detailed Problem Breakdown

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#detailed-problem-breakdown)

1. **Basic Structure**: The `MyHashMap` class will have the following components:
    
    - **Array of Buckets**: Internally, the `HashMap` will use an array where each element (bucket) is a linked list of key-value pairs. Each key-value pair is stored as a node in the linked list.
    - **Node Class**: A helper class (called `Node`) will represent a key-value pair and contain a reference to the next node, allowing you to chain key-value pairs in case of collisions.
2. **Core Operations**:
    
    - **Put (Add/Update)**: Insert a key-value pair into the map. If the key already exists, update its value.
    - **Get (Retrieve)**: Retrieve the value associated with a given key.
    - **Remove**: Remove the key-value pair from the map based on the key.
    - **ContainsKey**: Check if the map contains a specific key.
    - **Size**: Return the number of key-value pairs in the map.
3. **Collision Resolution with Chaining**:
    
    - **Hash Collision**: When two keys hash to the same index in the bucket array, store the key-value pairs in a linked list at that bucket index.
    - **Chaining**: Use a linked list to handle collisions. Multiple key-value pairs that hash to the same index will be linked together.
4. **Dynamic Resizing (Optional)**: You can optionally resize the bucket array when the load factor (number of elements relative to bucket array size) exceeds a certain threshold. For simplicity, this resizing step is optional for the base implementation.
    
5. **Hash Function**:
    
    - **`hashCode()`**: Use the `hashCode()` method provided by Java's `Object` class to generate a hash value for the key.
    - **Modulo Operation**: Use the modulo operator (`%`) to map the hash code to a valid index in the bucket array (to ensure the index falls within the array's bounds).
6. **Null Key Handling** (Optional): Optionally, allow `null` as a key, which will always be stored at a specific bucket index (e.g., index `0`).
    
    ### Explanation of Key Components:
    
    [](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#explanation-of-key-components)
    
    1. **`Node<K, V>` Class**:
        - Represents an individual key-value pair (node) in a linked list.
        - Each node contains a `key`, `value`, and `next` pointer to the next node (to handle collisions using chaining).
    2. **Bucket Array**:
        - The `buckets` array is an array of `Node<K, V>` references, where each element is the head of a linked list.
        - Each bucket represents a slot in the `HashMap` that can hold one or more key-value pairs (in case of collisions).
    3. **Collision Handling Using Chaining**:
        - When a collision occurs (i.e., two keys hash to the same bucket index), the key-value pairs are stored in a linked list within the same bucket.
        - If a key already exists in the linked list (within the same bucket), its value is updated.
    4. **`hashCode()` and Bucket Indexing**:
        - The `hashCode()` method of the key is used to generate a hash value.
        - The modulo operation (`%`) is used to map the hash value to a bucket index in the array.
    5. **Operations**:
        - **Put**: Adds a key-value pair to the `HashMap`. If a collision occurs, the new node is added to the linked list.
        - **Get**: Retrieves the value associated with the key by traversing the linked list in the appropriate bucket.
        - **Remove**: Removes a key-value pair from the map by unlinking the node in the linked list (if it exists).
        - **ContainsKey**: Checks whether a key is present in the map.
        - **Size**: Returns the current number of key-value pairs in the map.
    
    ### Handling Collisions with Chaining:
    
    [](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#handling-collisions-with-chaining)
    
    - When a key is inserted, the hash code is computed, and the corresponding bucket index is determined.
        
    - If a key-value pair already exists in the bucket, a new node is added to the linked list (chaining).
        
    - When retrieving or removing a key, the linked list is traversed to find the correct node.
        
    - ### Key Notes:
        
        [](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems-collections.md#key-notes)
        
        1. **Chaining**: When multiple keys hash to the same index, chaining is used to resolve collisions.
        2. **HashCode Calculation**: The `hashCode()` function is crucial for determining the correct bucket index.
        
        This implementation provides a basic `HashMap` functionality with key features like handling collisions, chaining, and dynamic insertion/removal of elements.