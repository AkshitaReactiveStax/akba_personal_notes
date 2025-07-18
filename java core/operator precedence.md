### **Types of Operators in Java**

|**Category**|**Operators**|
|---|---|
|**Arithmetic**|+, -, *, /, %|
|**Unary**|+, -, ++, --, ~, !|
|**Relational**|==, !=, >, <, >=, <=|
|**Logical**|&&, `|
|**Bitwise**|&, `|
|**Assignment**|=, +=, -=, *=, /=, %=|
|**Ternary**|?:|
|**Instanceof**|instanceof|
|**Type Comparison**|==, != (for objects and primitives)|
|**Lambda/Method Ref**|->, ::|
## **2. Operator Precedence in Java**

**Precedence** determines **which operator is evaluated first** in an expression. **Associativity** resolves **ties** (i.e., when operators have the same precedence).
> 💡 Tip: Always use **parentheses ()** to clarify and avoid surprises!
> 
> ### **Java Operator Precedence Table (Highest to Lowest)**

|**Precedence**|**Operators**|**Associativity**|
|---|---|---|
|1 (Highest)|(), [], ., ::|Left to right|
|2|++, --, + (unary), - (unary), ~, !|Right to left|
|3|*, /, %|Left to right|
|4|+, -|Left to right|
|5|<<, >>, >>>|Left to right|
|6|<, <=, >, >=, instanceof|Left to right|
|7|==, !=|Left to right|
|8|&|Left to right|
|9|^|Left to right|
|10|`|`|
|11|&&|Left to right|
|12|`||
|13|?:|Right to left|
|14|=, +=, -=, *=, /=, etc.|Right to left|
|15 (Lowest)|, (comma)|Left to right|

    