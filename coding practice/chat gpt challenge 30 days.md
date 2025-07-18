response template 

|**Field**|**Your Entry**|
|---|---|
|**Problem Number**|(e.g., Problem 3 — Inverted Stars)|
|**Your Code**|(Paste your full code for that problem)|
|**Time Taken**|(How many minutes you took to solve it)|
|**Any Struggles?**|(Where you got stuck or confused, even if solved later)|




---

# **📅 DAY 1 — PATTERN TRAINING**

  

✅ **Theme today:**

Simple right-angled triangle patterns — basic loops warmup.

---

### **1️⃣ Right-angled Star Triangle**

```
Print this:
*
**
***
****
*****
```

**Hints:**

- Outer loop for rows.
    
- Inner loop for columns (stars).
    
- No fancy spacing needed yet.
    

---

### **2️⃣ Right-angled Number Triangle**

```
Print this:
1
12
123
1234
12345
```

**Hints:**

- Outer loop: rows.
    
- Inner loop: print 1 to row number.
    

---

### **3️⃣ Inverted Right-angled Star Triangle**

```
Print this:
*****
****
***
**
*
```

**Hints:**

- Think: starting from max stars and **decreasing**.
    

---

### **4️⃣ Inverted Right-angled Number Triangle**

```
Print this:
12345
1234
123
12
1
```

**Hints:**

- Start with full numbers and **reduce**.
    

---

### **5️⃣ Continuous Number Triangle**

```
Print this:
1
2 3
4 5 6
7 8 9 10
11 12 13 14 15
```

**Hints:**

- Need a currentNum that **keeps increasing** after each print.
    
- Each row prints +1 number than previous.
    

---

### **6️⃣ Bonus Challenge (If you have time) ✨**

  

**Right-angled Alphabets**

```
A
AB
ABC
ABCD
ABCDE
```

**Hints:**

- Understand how to move from char value (like 'A') to next.
    
- Use character arithmetic.
    

---
#QUESTION how will you print 5 spaces and 5 stars on the same line ?


---

# **📅 DAY 2 — PATTERN TRAINING**

  

✅ **Theme today:**

Mastering **Center Alignments, Spaces**, and **Shape Building**.

  

✅ **Focus:**

- Controlling **spaces before stars/numbers**.
    
- Thinking in “**2 parts**”: (Spaces + Stuff).
    
- Introducing **hollow patterns** (a little bit).
    
- **More visualization, less guessing.**
    

---

# **📜 DAY 2 Problems List**

  

(Ordered from easier ➡ harder ➡ spicier)

---

### **1️⃣ Left-Aligned Star Pyramid**

  

(soft warmup)

```
*
**
***
****
*****
```

✅ Very simple, just like Day 1, to warm your brain up.

---

### **2️⃣ Centered Star Pyramid**

  

(starts brain workout)

```
    *
   ***
  *****
 *******
*********
```

✅ Now you need to **print spaces first**, then stars.

  

(Hint: Spaces decrease, stars increase.)

---

### **3️⃣ Centered Number Pyramid**

  

(getting spicier)

```
    1
   121
  12321
 1234321
123454321
```

✅ Centered with numbers — notice the **symmetry**.

  

(Hint: Two parts: increasing numbers → decreasing numbers.)

---

### **4️⃣ Hollow Centered Star Pyramid**

  

(🔥 spice level increasing)

```
    *    
   * *   
  *   *  
 *     * 
*********
```

✅ Like Problem 2, but now stars are **only on edges** — inside is **spaces**.

  

(Hint: if (j == 1 || j == last) print star, else print space.)

---

### **5️⃣ Inverted Centered Star Pyramid**

  

(Boss battle for today)

```
*********
 *******
  *****
   ***
    *
```

✅ Reverse of Problem 2 —

Less stars, more spaces each line.

  

(Hint: Spaces increase, stars decrease.)

---

### **6️⃣ Bonus Challenge ✨**

  

**Diamond Pattern (Full day boss fight if you want)**

```
    *
   ***
  *****
 *******
*********
 *******
  *****
   ***
    *
```

✅ Combine Problem 2 + Problem 5.



**DAY 2 DONEEEE 🔥🔥🔥!!**

Officially locking it in the books:

You didn’t just finish Day 2 — you **leveled up massively** in real problem-solving skill. 🧠💥

---

# **📜 DAY 2 Achievements**

|**Skill**|**Status**|
|---|---|
|Center alignments|Mastered ✅|
|Space-star control|Mastered ✅|
|Hollow pyramids|Mastered ✅|
|Full diamonds|Mastered ✅|
|Debugging and fixing patterns|Strong ✅|
|Asking optimization questions|✅ (Next-level thinking)|

  

---

# **🧠 Here’s your** 

# **Day 2 Cheat Sheet**

#  **— quick** 

# **brain tattoo**

#  **🧠**

---

## **⭐ Pyramid (Normal Centered)**

- Spaces: n - i
    
- Stars: 2*i - 1
    
- Loops:
    
    1. Print spaces
        
    2. Print stars
        
    

---

## **⭐ Inverted Pyramid (Centered)**

- Spaces: i
    
- Stars: 2*(n - i) + 1
    
- Loops:
    
    1. Print spaces
        
    2. Print stars
        
    

---

## **⭐ Hollow Pyramid (Centered)**

- Print * if:
    
    - First column
        
    - Last column
        
    - Last row
        
    
- Else print space.
    

  

**if condition inside stars printing:**

```
if (col == 1 || col == totalCols || row == n)
```

  

---

## **⭐ Diamond**

- Upper half: Normal Pyramid
    
- Lower half: Inverted Pyramid
    

  

**(2 triangles glued at the center)**

---

✅ **ALWAYS DRAW first, then code.**

✅ **Center patterns = think spaces separately first.**

✅ **Hollow = think borders.**

✅ **Symmetry = think left and right stars balance.**



---

# **📅 DAY 3 — PATTERN TRAINING**

  

✅ **Theme Today:**

- Hollow Diamonds
    
- Hollow Half-Pyramids
    
- Mixed Number Patterns
    
- Logical Twists (easy-medium)
    
- Little bit more **brainy conditions inside loops** 🧠
    

  

✅ **Focus:**

- Master hollow pattern logic everywhere
    
- Get more comfortable using **if-else** conditions inside loops
    
- Practice **thinking in mirror images** and **dynamic conditions**.
    

---

# **📜 DAY 3 Problems List**

  

(Ordered from easier ➡ harder ➡ spicy)

---

### **1️⃣ Hollow Half Pyramid (Right-angled)**

```
*
* *
*   *
*     *
* * * * *
```

✅ Right-angled hollow triangle.

✅ Last row = full stars.

✅ Inside = spaces.

---

### **2️⃣ Hollow Inverted Half Pyramid (Right-angled, upside-down)**

```
* * * * *
*     *
*   *
* *
*
```

✅ Same as 1️⃣ but **upside-down**.

✅ Think carefully about spaces and stars.

---

### **3️⃣ Hollow Full Diamond**

```
    *    
   * *   
  *   *  
 *     * 
*       *
 *     * 
  *   *  
   * *   
    *    
```

✅ Like a full diamond, but hollow inside.

✅ Only borders have stars.

---

### **4️⃣ Centered Number Pyramid (Slightly Twisted)**

```
    1
   121
  12321
 1234321
123454321
```

✅ Same as Day 2 centered number pyramid —

✅ BUT now you’ll add one small “shift” that I’ll explain after you attempt if needed.

---

### **5️⃣ Inverted Number Pyramid (Special)**

```
123454321
 1234321
  12321
   121
    1
```

✅ Stars replaced by numbers decreasing.

✅ Think about both spaces and numbers decreasing.






---

# **📅 DAY 4 — Welcome to Phase 2 🚀**

  

✅ **Theme Today:**

- **Arrays** and **Strings** basic-to-medium problems
    
- Heavy practice of **loops**, **if-else**, and **logic building**
    
- Slowly starting to touch **edge cases** and **interview problem styles**
    

---

# **📜 DAY 4 Problem Set (10 Problems)**

---

### **1️⃣ Find the Maximum Number in an Array**

- Input: An array of integers.
    
- Task: Find and print the maximum number.
    

---

### **2️⃣ Find the Minimum Number in an Array**

- Input: An array of integers.
    
- Task: Find and print the minimum number.
    

---

### **3️⃣ Reverse an Array**

- Input: An array of integers.
    
- Task: Print the array elements in reverse order.
    

---

### **4️⃣ Check if Array is Sorted (Ascending)**

- Input: An array of integers.
    
- Task: Print “YES” if sorted in ascending order, otherwise “NO”.
    

---

### **5️⃣ Find the Sum of Elements in an Array**

- Input: An array of integers.
    
- Task: Calculate and print the sum.
    

---

### **6️⃣ Find Duplicates in an Array**

- Input: An array of integers.
    
- Task: Print the duplicate elements (if any).
    

---

### **7️⃣ Count Even and Odd Numbers**

- Input: An array of integers.
    
- Task: Print the count of even numbers and odd numbers separately.
    

---

### **8️⃣ Reverse a String**

- Input: A String.
    
- Task: Print the string in reverse.
    

  

Example:

Input → “coding”

Output → “gnidoc”

---

### **9️⃣ Check if String is Palindrome**

- Input: A String.
    
- Task: Check and print “YES” if it’s a palindrome, otherwise “NO”.
    

  

Example:

Input → “racecar”

Output → “YES”

---

### **🔟 Count Vowels and Consonants in a String**

- Input: A String.
    
- Task: Count and print number of vowels and consonants separately.
    

--


---

# **📅 DAY 5 — Arrays & Strings (Level-Up)**

  

✅ **Theme Today:**

- Slightly trickier array problems
    
- Real-world string manipulations
    
- Introduction to hash map-style logic (without using Map yet)
    

  

✅ **Focus Areas:**

- Clean loop logic
    
- Element frequency
    
- Word/character manipulation
    
- Thinking in **data processing steps**
    

---

# **📜 DAY 5 Problem Set**

---

### **1️⃣ Print All Even Numbers in Array**

- Input: An array of integers
    
- Task: Print all even elements in order
    

---

### **2️⃣ Remove All Duplicates from Array (Without Using Set or List)**

- Input: {1, 2, 3, 2, 1, 4}
    
- Output: {1, 2, 3, 4}
    
    _(Preserve order)_
    

---

### **3️⃣ Count Frequency of Each Element in Array**

- Input: {1, 2, 1, 3, 2, 1}
    
- Output:
    
    1 -> 3
    
    2 -> 2
    
    3 -> 1
    

---

### **4️⃣ Find the First Non-Repeating Element in Array**

- Input: {9, 2, 3, 2, 6, 6}
    
- Output: 9
    

---

### **5️⃣ Check if Two Strings are Anagrams**

- Input: "listen", "silent"
    
- Output: YES
    
    _(Assume lowercase and no spaces)_
    

---

### **6️⃣ Remove Vowels from a String**

- Input: "Akshita Bajaj"
    
- Output: "ksht Bjj"
    

---

### **7️⃣ Reverse the Words in a Sentence**

- Input: "i love java"
    
- Output: "java love i"
    

---

### **8️⃣ Capitalize First Letter of Each Word**

- Input: "akshita is learning"
    
- Output: "Akshita Is Learning"
    

---

### **9️⃣ Count Occurrence of Each Character in String**

- Input: "aabcc"
    
- Output:
    
    a -> 2
    
    b -> 1
    
    c -> 2
    

---

### **🔟 Move All Zeros to End of Array**

- Input: {0, 1, 0, 3, 12}
    
- Output: {1, 3, 12, 0, 0}
    

