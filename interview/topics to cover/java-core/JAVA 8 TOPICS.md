
https://testbook.com/interview/java-stream-api-interview-questions

link to read for interview questions based on java 8 .

https://www.youtube.com/playlist?list=PLA3GkZPtsafZR6arC1A3N0i968gk9RvMv

java 8 - engineering digest full course

https://www.youtube.com/playlist?list=PL63BDXJjNfTElajNCfg_2u_pbe1Xi7uTy

stream API 60 questions

https://medium.com/@bhangalekunal2631996/java-stream-api-coding-interview-questions-and-answers-2a212505e1c6

stream API 50 questions

https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture18-java8-features.md

reactivestax notes on java 8 





- Collecting elements into a single value: You can use the Collectors.summingInt(), Collectors.averagingInt(), Collectors.maxBy(), and Collectors.minBy() methods to collect the elements of a Stream into a single value.


HARD coding questions streams :

Here are three challenging coding problems involving Java's **Stream API**, designed to test your understanding and problem-solving skills:

---

### **1. Grouping and Transforming Data**

Given a list of `Employee` objects with fields `id`, `name`, `department`, and `salary`, write a program to:

- Group employees by their department.
- For each department, calculate the total salary of all employees.
- Return a `Map<String, Double>` where the key is the department name and the value is the total salary.

**Solution Outline:**

`Map<String, Double> departmentSalaryMap = employees.stream()     .collect(Collectors.groupingBy(         Employee::getDepartment,         Collectors.summingDouble(Employee::getSalary)     ));`

---

### **2. Find the Second-Highest Number**

Given a list of integers, find the second-highest number using the Stream API. If the list has fewer than two distinct numbers, return `Optional.empty()`.

**Solution Outline:**

`Optional<Integer> secondHighest = numbers.stream()     .distinct()     .sorted(Comparator.reverseOrder())     .skip(1)     .findFirst();`

---

### **3. Flatten and Sort Nested Lists**

You are given a list of lists of integers (e.g., `List<List<Integer>>`). Write a program to:

- Flatten the nested lists into a single list.
- Sort the resulting list in ascending order.
- Remove duplicates.

**Solution Outline:**

`List<Integer> flattenedSortedList = nestedLists.stream()     .flatMap(List::stream)     .distinct()     .sorted()     .collect(Collectors.toList());`

---

These problems require a solid understanding of **Stream operations** like `map`, `flatMap`, `groupingBy`, `distinct`, and `sorted`. They also test your ability to chain operations effectively.