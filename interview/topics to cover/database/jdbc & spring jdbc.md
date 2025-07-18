https://docs.oracle.com/javase/tutorial/jdbc/basics/processingsqlstatements.html
read this link by Oracle - jdbc basics .

- **MySQL: com.mysql.cj.jdbc.Driver**
    
- **PostgreSQL: org.postgresql.Driver**
    
- **Oracle: oracle.jdbc.OracleDriver**
  
  **pure java thin driver examples which has direct DB access, no middleware server !!!!!!!!!!**




### **🔁** 

### **Typical Flow Recap**

1. Java App → asks DriverManager for a DB connection.
    
2. DriverManager → uses a driver (e.g., Oracle, ODBC) to connect.
    
3. You get a Connection object.
    
4. Use Connection to create a Statement, PreparedStatement, or CallableStatement.
    
5. Execute SQL → get a ResultSet if it’s a query.
    
6. Read data → close everything (ResultSet, Statement, Connection).



---

## **🔍** 

## **JDBC Driver Architecture – All 4 Types Explained**

  

The diagram breaks down **how a Java application communicates with a database** using JDBC, through different types of drivers.

---

### **✅** 

### **Top Layer: Common Flow for All Types**

- **Java Application**
    
    This is your main program, written in Java.
    
- **JDBC API**
    
    Your app uses JDBC interfaces like Connection, Statement, ResultSet.
    
- **JDBC DriverManager**
    
    Selects the correct driver implementation based on your JDBC URL (jdbc:mysql://..., jdbc:oracle:thin:@..., etc.).
    

  

From here, control goes into one of **4 driver types**, each with a different architecture.

---

## **🔢** 

## **Type 1: JDBC-ODBC Bridge Driver**

  

**(Legacy, Deprecated)**

- Uses the **ODBC API** internally.
- Requires native **ODBC drivers** and **DB client libraries**.
- Not pure Java (needs native code).

> Example: sun.jdbc.odbc.JdbcOdbcDriver (Removed in Java 8)

  

🔴 **Disadvantages**:

- Platform-dependent
- Slow due to multiple layers
- Not recommended or supported anymore
    

---

## **🔢** 

## **Type 2: Native-API Driver (Partial Java Driver)**

- Converts JDBC calls into native DB client library calls.
- Needs **vendor-supplied DB libraries** (Oracle, Sybase, etc.).
> Example: oracle.jdbc.driver.OracleDriver

  
⚠️ **Disadvantages**:

- Requires native DB client software to be installed
- Platform-dependent

  

✅ **Better than Type 1** but not ideal for distributed apps

---

## **🔢** 

## **Type 3: Network Protocol Driver (Pure Java + Middleware)**

- JDBC calls go through a **Java driver** → to a **middleware server** → to DB.
- The **middleware translates JDBC to DB-specific calls**.

> Example: IDS Server by Progress Software

  

✅ **Advantages**:

- Pure Java
- Good for connecting multiple DB types from one source
- Centralized management


⚠️ **Disadvantage**:

- Middleware server adds complexity and latency
    

---

## **🔢** 

## **Type 4: Thin Driver (Pure Java, Direct DB Access) — BEST!**

- Directly translates JDBC calls into DB-specific protocol (no middleware, no native libs).
- Pure Java, lightweight, fast.
    

> Examples:

  

- MySQL: com.mysql.cj.jdbc.Driver
- PostgreSQL: org.postgresql.Driver
- Oracle: oracle.jdbc.OracleDriver

  

✅ **Advantages**:

- Best performance
- Cross-platform
- No external libs or middleware

🔥 **Most used in modern apps**

### **📝 Summary Table**

|**Type**|**Description**|**Pure Java**|**Middleware**|**Client Libs Needed**|**Performance**|
|---|---|---|---|---|---|
|1|JDBC-ODBC Bridge|❌|❌|✅|❌ (slow)|
|2|Native-API|❌|❌|✅|⚠️ Moderate|
|3|Network Protocol|✅|✅|❌|⚠️ Good|
|4|Thin Driver|✅|❌|❌|✅ Best|

  

---

## **✅ 1.** 

## **Statement vs PreparedStatement vs CallableStatement**

|**Interface**|**Use Case**|**SQL Type**|**Prevents SQL Injection**|**Caching**|
|---|---|---|---|---|
|Statement|Simple static queries|Hardcoded|❌|❌|
|PreparedStatement|Repeated or dynamic queries|Parametrized|✅|✅|
|CallableStatement|Calling stored procedures/functions|Stored procedures only|✅|✅|

## **✅ Using** 

## **Statement**

The Statement class allows executing SQL via 3 methods:
### **🔹** 

### **executeQuery()**
###  **→ For** SELECT statements

```
Statement stmt = conn.createStatement();
String selectSql = "SELECT * FROM employees WHERE employee_id = " + employee_id;
ResultSet resultSet = stmt.executeQuery(selectSql);

// ❌ Prone to SQL Injection
String selectSql2 = "SELECT * FROM employees WHERE employee_id = (SELECT 1 FROM dual)";
ResultSet rs2 = stmt.executeQuery(selectSql2);
```

### **🔹** 

### **executeUpdate()**

###  **→ For DML & DDL (INSERT** , UPDATE, DELETE , ALTER etc)

```
String insertSql = "INSERT INTO employees(name, position, salary) VALUES('John', 'Developer', 2000)";
int inserted = stmt.executeUpdate(insertSql);  // returns number of affected rows
```

### **🔹** 

### **execute()**

###  **→ For any unknown type of query**

```
String tableSql = """
    CREATE TABLE IF NOT EXISTS employees (
        emp_id INT PRIMARY KEY AUTO_INCREMENT,
        name VARCHAR(30),
        position VARCHAR(30),
        salary DOUBLE
    )
""";
boolean hasResultSet = stmt.execute(tableSql);

if (!hasResultSet) {
    int affectedRows = stmt.getUpdateCount(); // 0 for DDL
} else {
    ResultSet rs = stmt.getResultSet();
}
```

  

---

## **✅ Using** 

## **PreparedStatement**

  

PreparedStatement is precompiled and supports parameters marked with ?.

  

### **🔹 Example: Updating employee position**

```
String updateSql = "UPDATE employees SET position = ? WHERE emp_id = ?";
PreparedStatement pstmt = conn.prepareStatement(updateSql);

pstmt.setString(1, "Lead Developer");
pstmt.setInt(2, 1);

int rowsAffected = pstmt.executeUpdate();  // returns rows updated
```

### **🔹 Benefits:**

- Prevents **SQL injection**
    
- Supports **parameter binding**
    
- Better **performance** for repeated use
    

---

## **✅ Using** 

## **CallableStatement**
CallableStatement is used to call stored procedures.

### **🔹 Example: Stored procedure to insert employee**

```
String preparedSql = "{call insertEmployee(?, ?, ?, ?)}";
CallableStatement cstmt = conn.prepareCall(preparedSql);

// Input parameters
cstmt.setString(2, "Ana");
cstmt.setString(3, "Tester");
cstmt.setDouble(4, 2000);

// Output parameter (e.g., auto-generated employee ID)
cstmt.registerOutParameter(1, Types.INTEGER);

// Execute and retrieve output
cstmt.execute();
int newId = cstmt.getInt(1);
```

### **🔹 Points to remember:**

- Output params must be **registered before execution**
    
- Use getX() methods to retrieve output after execute()
    
Would you like a quick **mock quiz round** on these now to test your recall before your interview?
  

---




## **✅ 2.** 

## **ResultSet Navigation**
The ResultSet object holds the result of a query. You can iterate through rows via the next() and extract column values via getX() methods where `X` represents the type of the cell data .

### **🔸 Key Methods:**

```
while (rs.next()) {
    int id = rs.getInt("id");
    String name = rs.getString("name");
}
```

#### 🔸Updatable `ResultSet`

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#2-updatable-resultset)

By default, a `ResultSet` is forward-only and read-only. To modify data and traverse it in both directions, create the `Statement` object with additional parameters:

```java
stmt = con.createStatement(ResultSet.TYPE_SCROLL_INSENSITIVE, ResultSet.CONCUR_UPDATABLE);
```

You can navigate through this type of `ResultSet` using the following methods:

- `first()`, `last()`, `beforeFirst()`, `beforeLast()`
- `next()`, `previous()`
- `getRow()`
- `moveToInsertRow()`, `moveToCurrentRow()`
- `absolute(int row)`, `relative(int nrRows)`

To update a `ResultSet`, use methods with the format `updateX()` where `X` is the type of the cell data. To persist these changes, use:

- `updateRow()`, `insertRow()`, `deleteRow()`
- `refreshRow()`, `cancelRowUpdates()
`
### **🔸 Pro Tip:**
By default, a `ResultSet` is forward-only and read-only. To modify data and traverse it in both directions, create the `Statement` object with additional parameters:

```java
stmt = con.createStatement(ResultSet.TYPE_SCROLL_INSENSITIVE, ResultSet.CONCUR_UPDATABLE);
```

If asked about cursor types:

- TYPE_FORWARD_ONLY (default)
    
- TYPE_SCROLL_INSENSITIVE
    
- TYPE_SCROLL_SENSITIVE




### Parsing Metadata

#### 1. `DatabaseMetaData`

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#1-databasemetadata)

This interface provides general information about the database (tables, stored procedures, SQL dialect, etc.).

#### 2. `ResultSetMetaData`

This interface allows you to find information about a `ResultSet`, such as the number and names of its columns.
    

---

## **✅ 3.** 

## **Why PreparedStatement is Better** than Statement
### 1. **Security (Prevention of SQL Injection)**:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#1-security-prevention-of-sql-injection)

- **`PreparedStatement`**: Helps prevent **SQL injection attacks** by separating SQL logic from data. The SQL query is precompiled, and the input values are bound to the query at runtime. Even if a user inputs malicious SQL code, it is treated as data and not executable SQL.
- **`Statement`**: Vulnerable to SQL injection, as it concatenates user inputs directly into the SQL query. Malicious inputs can alter the query structure and execute unintended commands.

**Example:**

```java
// Vulnerable to SQL injection
String user = "username' OR '1'='1";
Statement stmt = connection.createStatement();
String query = "SELECT * FROM users WHERE username = '" + user + "'";
ResultSet rs = stmt.executeQuery(query);  // Potentially dangerous!
```

**With PreparedStatement**:

```java
String query = "SELECT * FROM users WHERE username = ?";
PreparedStatement pstmt = connection.prepareStatement(query);
pstmt.setString(1, user);  // User input is safely parameterized
ResultSet rs = pstmt.executeQuery();  // Safe from SQL injection
```

### 2. **Performance**:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#2-performance)

- **`PreparedStatement`**: **Precompiles** the SQL query, meaning the database can reuse the query plan across multiple executions. This can significantly improve performance, especially for repeated executions of the same query with different parameters. When you execute a `PreparedStatement`, the database does not need to parse and optimize the SQL statement each time.
- **`Statement`**: Every time a `Statement` is executed, the SQL query is sent to the database and needs to be parsed and compiled again, even if it’s the same query with different parameters. This can lead to a performance penalty in scenarios where the same query is executed frequently.

**Example**:

```java
// PreparedStatement is optimized for repeated execution
String query = "INSERT INTO employees (name, salary) VALUES (?, ?)";
PreparedStatement pstmt = connection.prepareStatement(query);
for (Employee emp : employeeList) {
    pstmt.setString(1, emp.getName());
    pstmt.setDouble(2, emp.getSalary());
    pstmt.executeUpdate();
}
```

### 3. **Parameter Binding**:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#3-parameter-binding)

- **`PreparedStatement`**: Automatically handles parameter binding, meaning it escapes and binds values safely. This also helps in handling special characters in strings and different data types.
- **`Statement`**: Requires manual concatenation of strings and numbers into SQL queries, which is prone to errors and issues (e.g., mishandling quotes in strings or wrong data formatting).

**Example**:

```java
// With PreparedStatement
String query = "INSERT INTO users (name, age) VALUES (?, ?)";
PreparedStatement pstmt = connection.prepareStatement(query);
pstmt.setString(1, "John");
pstmt.setInt(2, 30);
pstmt.executeUpdate();
```

**With Statement**:

```java
// Manual concatenation (error-prone)
String query = "INSERT INTO users (name, age) VALUES ('John', 30)";
Statement stmt = connection.createStatement();
stmt.executeUpdate(query);
```

### 4. **Code Readability and Maintenance**:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#4-code-readability-and-maintenance)

- **`PreparedStatement`**: Makes the code cleaner and easier to read, especially when working with complex queries. By using placeholders (`?`) for parameters, you separate SQL structure from the data, making it easier to modify queries.
- **`Statement`**: Requires manual construction of SQL queries, which can get messy and hard to read, especially when many parameters are involved. It increases the risk of syntax errors.

**Example**:

```java
// PreparedStatement: Easier to modify and maintain
String query = "UPDATE users SET name = ?, age = ? WHERE id = ?";
PreparedStatement pstmt = connection.prepareStatement(query);
pstmt.setString(1, "John");
pstmt.setInt(2, 30);
pstmt.setInt(3, 1);
pstmt.executeUpdate();
```

**With Statement**:

```java
// Harder to maintain and error-prone
String query = "UPDATE users SET name = 'John', age = 30 WHERE id = 1";
Statement stmt = connection.createStatement();
stmt.executeUpdate(query);
```

### 5. **Handling Complex Queries**:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#5-handling-complex-queries)

- **`PreparedStatement`**: Ideal for handling complex queries, especially when you need to run the same query multiple times with different parameter values.
- **`Statement`**: May require additional string manipulations or concatenations when handling complex queries, which increases the risk of mistakes.

### 6. **Batch Processing**:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#6-batch-processing)

- **`PreparedStatement`**: Supports **batch processing** where you can add multiple sets of parameters to the same query and execute them in a batch. This can further improve performance when executing multiple similar queries.
- **`Statement`**: Does not have built-in support for batch processing. You would need to execute individual queries for each data set, which increases overhead.

**Example** (Batch with `PreparedStatement`):

```java
String query = "INSERT INTO employees (name, salary) VALUES (?, ?)";
PreparedStatement pstmt = connection.prepareStatement(query);
for (Employee emp : employeeList) {
    pstmt.setString(1, emp.getName());
    pstmt.setDouble(2, emp.getSalary());
    pstmt.addBatch();  // Add to batch
}
pstmt.executeBatch();  // Execute all at once
```

### 7. **Flexibility**:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#7-flexibility)

- **`PreparedStatement`**: Supports dynamic parameterization, making it easier to change the input values for the same query without modifying the SQL itself.
- **`Statement`**: Requires a new SQL string for every query that has different parameters.

### When to Use Each:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#when-to-use-each)

- **Use `PreparedStatement`**:
    
    - When you have queries that are executed multiple times with different parameters.
    - When you want to prevent SQL injection and ensure security.
    - When you need better performance for frequent queries.
    - When dealing with complex queries with dynamic values.
    - When handling batch processing.
- **Use `Statement`**:
    
    - For simple, **one-off queries** with no parameters.
    - When query performance and security are not primary concerns.
    - When you want to execute raw SQL commands without parameters (though `PreparedStatement` can handle this too).

### Summary of Benefits of `PreparedStatement` Over `Statement`:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#summary-of-benefits-of-preparedstatement-over-statement)

|Feature|`Statement`|`PreparedStatement`|
|---|---|---|
|**Security**|Vulnerable to SQL injection|Safe from SQL injection (parameterized queries)|
|**Performance**|Re-parses the query each time|Precompiled, faster for repeated queries|
|**Space Efficiency**|No specific optimizations|Reuses query plan and reduces overhead|
|**Parameter Handling**|Manual concatenation|Automatic parameter handling|
|**Batch Processing**|Not supported natively|Supported, efficient for multiple similar queries|
|**Readability & Maintenance**|More error-prone and complex|Easier to read, maintain, and modify|
|**Complex Queries**|Harder to manage|Ideal for complex, dynamic queries|

In conclusion, `PreparedStatement` should be your go-to choice in most situations because of its advantages in terms of security, performance, readability, and maintainability. `Statement` is typically reserved for simple, ad-hoc queries where parameterization isn't needed.
  

---

## **✅ 4.** 

## **Transaction Management**

  

By default, JDBC **auto-commits** after each SQL statement. You can control transactions manually:

  

### **🔸 Example:**

```
conn.setAutoCommit(false);
try {
    // Multiple SQL statements
    ps1.executeUpdate();
    ps2.executeUpdate();

    conn.commit(); // ✅ Commit if all successful
} catch (Exception e) {
    conn.rollback(); // ❌ Rollback if any fail
}
```

https://docs.oracle.com/javase/tutorial/jdbc/basics/transactions.html
transaction management - read this link .

------------------------------------------------------------------------
## **✅ 5.** 

## **Batch Processing

#### 1. Using `Statement`

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#1-using-statement)

Add multiple queries to a batch using `addBatch()` and execute them using `executeBatch()`. It returns an `int` array indicating how many records were affected.

**Example:**

```java
Statement statement = connection.createStatement(); 
statement.addBatch("INSERT INTO EMPLOYEE(ID, NAME, DESIGNATION) VALUES ('1','EmployeeName','Designation')"); 
statement.addBatch("INSERT INTO EMP_ADDRESS(ID, EMP_ID, ADDRESS) VALUES ('10','1','Address')"); 
statement.executeBatch();
```

#### 2. Using `PreparedStatement`

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#2-using-preparedstatement)

Reusing SQL statements with `PreparedStatement` and setting new parameters for each update/insert operation.

**Example:**

```java
String[] EMPLOYEES = new String[]{"Zuck", "Mike", "Larry", "Musk", "Steve"}; 
String[] DESIGNATIONS = new String[]{"CFO", "CSO", "CTO", "CEO", "CMO"}; 

String insertEmployeeSQL = "INSERT INTO EMPLOYEE(ID, NAME, DESIGNATION) VALUES (?,?,?)"; 
PreparedStatement employeeStmt = connection.prepareStatement(insertEmployeeSQL); 

for (int i = 0; i < EMPLOYEES.length; i++) { 
    String employeeId = UUID.randomUUID().toString(); 
    employeeStmt.setString(1, employeeId); 
    employeeStmt.setString(2, EMPLOYEES[i]); 
    employeeStmt.setString(3, DESIGNATIONS[i]); 
    employeeStmt.addBatch(); 
} 
employeeStmt.executeBatch();
```

Batching in JDBC is primarily used for **insert**, **update**, and **delete** operations, but **not** for **select** operations. Here's why:
### **Purpose of Batching**:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#1-purpose-of-batching)

- Batching is designed to optimize operations that modify data (inserts, updates, deletes) by reducing the number of round-trips to the database and grouping multiple operations into a single request.
- These operations benefit from batching because they typically don't require immediate feedback on each individual operation.

### 2. **Why Not Batch `SELECT` Statements**:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#2-why-not-batch-select-statements)

- **`SELECT` Statements Return Results**: Unlike `insert`, `update`, or `delete`, a `SELECT` statement returns a result set, which must be processed row by row. Because each `SELECT` produces a different result set, it's not possible to batch multiple `SELECT` statements together in a way that efficiently handles these results in one go.
- **Result Handling**: Inserting multiple rows or updating multiple rows doesn’t return a result set for each operation, but a `SELECT` needs to return data, which could be of varying sizes and formats. Handling multiple result sets from a single batch would make it harder to manage the returned data efficiently.
- **Non-Modifying Operation**: Since `SELECT` doesn’t modify data, the performance optimizations of batching are not as beneficial. The main advantage of batching is reducing the number of trips to the database for modifying operations, but `SELECT` statements typically don’t involve the same kind of repetitive database modifications.

### Alternative for `SELECT` Optimization: **Batch Processing of Results**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#alternative-for-select-optimization-batch-processing-of-results)

While `SELECT` itself isn’t batched, if you’re dealing with large result sets, you can optimize how you **process the results**. Here are some techniques:

1. **Fetching Large Result Sets in Batches**:
    
    - You can fetch large data sets in smaller chunks using `setFetchSize()` to limit the number of rows retrieved in one go. This prevents loading the entire result set into memory at once, which can improve performance when handling large queries.
    
    Example:
    
    ```java
    preparedStatement = connection.prepareStatement("SELECT * FROM large_table");
    preparedStatement.setFetchSize(100);  // Fetch 100 rows at a time
    ResultSet resultSet = preparedStatement.executeQuery();
    ```
    
2. **Pagination**:
    
    - If you need to retrieve large amounts of data from a `SELECT` statement, you can use **pagination** (e.g., `LIMIT` in SQL) to fetch results in smaller chunks.
    
    Example:
    
    ```java
    String query = "SELECT * FROM employees LIMIT ? OFFSET ?";
    preparedStatement = connection.prepareStatement(query);
    preparedStatement.setInt(1, 100); // Limit the number of rows to fetch
    preparedStatement.setInt(2, 0);   // Offset to start fetching
    ```
    

### Conclusion:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#conclusion-1)

- **Batching** is primarily for **insert**, **update**, and **delete** operations in JDBC to optimize performance by reducing round-trips to the database and allowing the database to process multiple modifications at once.
- **`SELECT` statements are not batched** because they return result sets, and managing multiple result sets within a single batch would complicate result handling. Instead, optimization techniques like setting fetch sizes or using pagination are applied to handle large query results efficiently.
---

## **✅ 6.** 

## **JDBC URL Formats**

|**DB**|**JDBC URL Format**|
|---|---|
|MySQL|jdbc:mysql://localhost:3306/mydb|
|PostgreSQL|jdbc:postgresql://localhost:5432/mydb|
|Oracle|jdbc:oracle:thin:@localhost:1521:xe|
|SQL Server|jdbc:sqlserver://localhost:1433;databaseName=mydb|

🧠 **Tip:** Interviewers may ask how JDBC picks the correct driver → it’s based on the **JDBC URL prefix**.

---

## **✅ 7.** 

## **Connection Pooling**

  
Using connection pooling in Java with JDBC helps manage database connections more efficiently, especially in high-load applications. The common approach is to use a connection pool provided by libraries like **HikariCP**, **Apache DBCP**, or **C3P0**. Here’s a basic guide using **HikariCP**, which is widely known for its simplicity and performance.
Connection creation is expensive. Pooling **reuses DB connections** to improve performance.

  

### **🔸 Two Popular Libraries:**

#### **✅** 

#### **HikariCP (preferred)**

- Lightweight, fastest, Spring Boot default
    
- Example:
    

```
import com.zaxxer.hikari.HikariConfig;
import com.zaxxer.hikari.HikariDataSource;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

public class DatabaseConnectionPool {

    private static HikariDataSource dataSource;

    static {
        // Configure the HikariCP connection pool
        HikariConfig config = new HikariConfig();
        config.setJdbcUrl("jdbc:mysql://localhost:3306/yourdatabase");
        config.setUsername("yourusername");
        config.setPassword("yourpassword");
        config.setMaximumPoolSize(10); // Set max connections in pool
        config.setConnectionTimeout(30 000); // Timeout in milliseconds
        config.setIdleTimeout(10  000); // Idle timeout before connection is closed

        // Create the HikariCP data source
        dataSource = new HikariDataSource(config);
    }

    public static Connection getConnection() throws Exception {
        // Fetch a connection from the pool
        return dataSource.getConnection();
    }

    public static void close() {
        // Close the data source (usually when the app shuts down)
        if (dataSource != null) {
            dataSource.close();
        }
    }

    public static void main(String[] args) {
        try (Connection conn = getConnection();
             Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery("SELECT * FROM students")) {

            while (rs.next()) {
                System.out.println("Student ID: " + rs.getInt("id"));
            }

        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            close();
        }
    }
}
```


### Key Points:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#key-points)

1. **HikariConfig**: You configure the JDBC URL, username, password, and other pooling settings.
2. **HikariDataSource**: This is the actual connection pool. You use it to fetch a `Connection` object.
3. **getConnection()**: Instead of creating a new connection every time, this method retrieves one from the pool.
4. **Connection Timeout**: Set the maximum time the pool will wait for a connection.
5. **Idle Timeout**: Controls how long idle connections stay in the pool before being closed.

### Benefits of Connection Pooling:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#benefits-of-connection-pooling)

- **Improved Performance**: Reduces overhead by reusing existing connections instead of constantly opening and closing new ones.
- **Scalability**: Manages a large number of concurrent connections efficiently.
- **Better Resource Management**: Pool size limits the number of simultaneous connections to avoid overloading the database.
- **Handling Concurrent Requests**: When multiple threads or processes request database access, pooling ensures they share a limited number of connections, preventing failures.


#### **✅** 

#### **Apache DBCP (older but stable)**

- Used with legacy applications
    
- Needs manual setup in some cases
    

🧠 **Key Concepts to Know:**

- Max pool size
    
- Idle timeout
    
- Connection leak detection
  
  
## Benefits of Connection Pooling
### 1. **Connection Reuse**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#1-connection-reuse)

- **Without Pooling**: Every time you need a database connection, you have to open a new connection by interacting with the database server (e.g., `DriverManager.getConnection(...)`). This is an expensive operation in terms of time and resources, as it involves network communication, authentication, and establishing a session with the database.
- **With Pooling**: A connection pool maintains a set of pre-established, ready-to-use connections. When your application needs a connection, it simply borrows one from the pool, drastically reducing the time and overhead associated with setting up a connection. Once done, the connection is returned to the pool and can be reused by the next database operation.

### 2. **Efficient Resource Management**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#2-efficient-resource-management)

- **Without Pooling**: If every request opens a new connection and holds it for too long, the database server might quickly exhaust its resources (memory, CPU) due to the sheer number of open connections. Each new connection creates load on the database server.
- **With Pooling**: The pool manages how many connections are simultaneously active, helping prevent excessive database load. The pool reuses connections rather than opening new ones every time, leading to a more efficient use of database resources.

### 3. **Connection Limits and Throttling**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#3-connection-limits-and-throttling)

- **Without Pooling**: Your application can accidentally open too many connections to the database if not controlled, which can overwhelm the database or hit connection limits imposed by the database server.
- **With Pooling**: You can set an upper limit (e.g., `maxConnections` in HikariCP), which ensures that your application never tries to open more than a certain number of connections. If all connections are in use, the pool can block requests until a connection is available or throw an exception after a configurable timeout. This helps throttle your application's database usage.

### 4. **Connection Lifecycle Management**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#4-connection-lifecycle-management)

- **Without Pooling**: Connections that are opened but left idle for too long can consume resources unnecessarily. Additionally, you might run into stale connections, where connections are closed by the database server due to inactivity or network issues.
- **With Pooling**: Connection pools monitor and manage the lifecycle of connections. They can automatically close idle connections after a certain timeout (e.g., `idleTimeout` in HikariCP) and replace broken or stale connections, keeping the pool healthy and your application running smoothly.

### 5. **Connection Validation**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#5-connection-validation)

- **Without Pooling**: If a connection becomes stale or broken due to network issues or database crashes, your application might fail unexpectedly when trying to use it.
- **With Pooling**: Connection pools like HikariCP often provide connection validation mechanisms (e.g., executing a lightweight query like `SELECT 1` or using a "connection test query") to ensure that the connection is still valid before returning it from the pool. This helps avoid runtime errors due to broken connections.

### 6. **Configuration Flexibility**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#6-configuration-flexibility)

- **Without Pooling**: You have limited control over how connections are handled when opening them directly. For example, if you want to apply timeouts, limits, or monitoring, you need to implement it yourself.
- **With Pooling**: Connection pools provide a wide range of configurable options, such as:
    - `maxConnections`: Maximum number of connections in the pool.
    - `connectionTimeout`: Maximum time to wait for a connection before throwing an error.
    - `idleTimeout`: How long a connection can remain idle before being closed.
    - `minIdle`: Minimum number of idle connections to keep in the pool.
    - `maxLifetime`: Maximum lifetime of a connection before it's retired from the pool. This flexibility allows you to fine-tune the performance and resource usage based on your specific application's needs.

### 7. **Concurrency Management**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#7-concurrency-management)

- **Without Pooling**: Manually managing concurrent requests for database access can become complex. Multiple threads might need to open new connections simultaneously, which can result in contention, delays, or excessive resource usage.
- **With Pooling**: Connection pools are designed to handle concurrency efficiently. Multiple threads can acquire and release connections in parallel, and the pool manages the balance between connection reuse and opening new connections when needed.

### Summary: Benefits of Connection Pooling

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#summary-benefits-of-connection-pooling)

|Feature|Without Pooling|With Pooling|
|---|---|---|
|**Connection Overhead**|High, because each request opens a new connection|Low, because connections are reused|
|**Connection Limits**|Can easily exceed database limits|Controlled via configurable `maxConnections`|
|**Connection Lifetime**|Difficult to manage; can lead to resource leaks|Automatically managed (idle, max lifetime)|
|**Handling Stale Connections**|Manually handled or causes errors|Automatically validated before use|
|**Concurrency**|Potential contention, inefficiency|Efficient concurrent connection handling|
|**Configuration**|Limited, requires manual work|Flexible configuration options for performance tuning|

________________________________________________________________________

## ✅ 8** 

## JDBC with Transactions

### 1. **What is a Transaction?**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#1-what-is-a-transaction)

A transaction in SQL is a sequence of one or more SQL operations (e.g., `SELECT`, `INSERT`, `UPDATE`, or `DELETE`) executed as a single logical unit of work. A transaction ensures data consistency and integrity by adhering to the following **ACID** properties:

- **Atomicity**: All operations in the transaction must succeed or fail as a whole. If one part fails, the entire transaction is rolled back, undoing any partial changes.
- **Consistency**: The database moves from one consistent state to another after a transaction.
- **Isolation**: Transactions should not affect each other. One transaction’s changes must be isolated from others until it is complete.
- **Durability**: Once a transaction is committed, its results are permanent and survive even if the system crashes.

### 2. **Transaction Control Statements in SQL**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#2-transaction-control-statements-in-sql)

- **START TRANSACTION** or **BEGIN**: Marks the start of a transaction.
- **COMMIT**: Saves all changes made during the transaction.
- **ROLLBACK**: Undoes all changes made during the transaction.
- **SAVEPOINT**: Sets a point in the transaction to which you can roll back.
- **RELEASE SAVEPOINT**: Removes a savepoint.

#### Steps for a JDBC Transaction:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#steps-for-a-jdbc-transaction)

1. Disable auto-commit mode (`setAutoCommit(false)`).
2. Execute your SQL statements.
3. If all statements execute successfully, call `commit()`.
4. If any statement fails, call `rollback()` to undo the changes.
5. Re-enable auto-commit mode if needed.


 ## BATCHING WITH TRANSACTIONS

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#batching-with-transactions)

Batching in JDBC offers several performance and efficiency benefits compared to executing individual SQL statements one by one. Here's how batching improves performance:

### 1. **Reduced Network Overhead**:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#1-reduced-network-overhead)

- **Without Batching**: Every time you execute an SQL statement, it sends a separate request to the database server and waits for a response. This leads to multiple round-trips between your application and the database.
- **With Batching**: You can send multiple SQL statements in a single request, which reduces the number of round-trips to the database server. This is particularly beneficial when dealing with a large number of inserts, updates, or deletes.

**Benefit**: Fewer network calls mean reduced network latency, resulting in faster execution, especially when you're inserting a large number of rows.

### 2. **Better Resource Management**:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#2-better-resource-management)

- **Without Batching**: Each statement executed independently consumes resources (memory, CPU) on both the client (your application) and the database server. These resources must be managed for every individual statement.
- **With Batching**: Multiple SQL statements are grouped together, which allows the database to process them more efficiently, leading to better resource utilization.

**Benefit**: Database and application performance are optimized, as they are not overloaded with the overhead of managing individual statements.

### 3. **Improved Performance through Optimized Execution**:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#3-improved-performance-through-optimized-execution)

- **Without Batching**: The database has to compile and execute each SQL statement one by one, leading to additional overhead of parsing, planning, and optimizing the execution of each query.
- **With Batching**: The database server can optimize execution by processing the batch as a whole. Some databases can apply internal optimizations to execute batched statements more efficiently compared to executing them individually.

**Benefit**: Processing a batch of operations as a whole is faster than handling them one at a time, allowing databases to take advantage of internal optimizations.

### 4. **Efficient Use of JDBC Driver Resources**:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#4-efficient-use-of-jdbc-driver-resources)

- **Without Batching**: Every individual `executeUpdate()` or `executeQuery()` call incurs the overhead of JDBC driver processing for each statement.
- **With Batching**: The JDBC driver processes multiple statements in a single batch operation, reducing the overhead involved in managing multiple execution calls.

**Benefit**: JDBC driver overhead is reduced, leading to better throughput and performance.

### 5. **Bulk Inserts/Updates**:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#5-bulk-insertsupdates)

- **Without Batching**: Inserting or updating a large number of rows one at a time will lead to slower performance, as each operation is handled individually.
- **With Batching**: You can insert or update a large number of rows in bulk, which significantly improves the speed of these operations.

**Benefit**: Batching allows you to perform bulk inserts or updates efficiently, making it well-suited for situations where large data sets need to be processed. 
  

### Important Notes:

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#important-notes)

- **Batch Size**: It's recommended to limit the batch size, especially when dealing with large data sets, to avoid memory issues.
- **Error Handling**: If a failure occurs while processing the batch, the whole transaction can be rolled back to ensure data integrity.

If you don't explicitly manage the transaction in the above case (i.e., if you don't disable auto-commit and manually commit/rollback), each individual batched insert will be treated as its own transaction, and JDBC will automatically commit each statement after it is executed.

Here’s what will happen:

1. **Auto-Commit Mode**: By default, JDBC operates in auto-commit mode (`connection.setAutoCommit(true)`). In this mode, every SQL statement is treated as a separate transaction and is automatically committed as soon as it is executed.
    
2. **Batch Execution Without Transaction**:
    
    - If you don’t disable auto-commit (`connection.setAutoCommit(false)`), when you call `preparedStatement.executeBatch()`, each batch of inserts is treated as independent transactions. This means that:
        - Each SQL insert in the batch is committed immediately.
        - If one insert fails, the previously executed inserts in the batch are already committed, and they will not be rolled back.
3. **Partial Insert on Failure**: If an error occurs during one of the batch executions:
    
    - Without explicit transaction control (i.e., with auto-commit enabled), the system will only fail for the current batch, and the previous successful inserts will remain committed in the database.
    - This could lead to **inconsistent data** because part of the data might be inserted, and part of it may not be, depending on where the error occurred.


------------------------------------------------------------------------
##  **Transaction Isolation Levels in MySQL**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#6-transaction-isolation-levels-in-mysql)

When working with transactions, you can specify the **isolation level** to control how transactions interact with one another.

1. **READ UNCOMMITTED**: The lowest level of isolation. A transaction can see uncommitted changes made by other transactions, leading to potential issues like dirty reads.
2. **READ COMMITTED**: A transaction can only see committed changes from other transactions, preventing dirty reads, but non-repeatable reads may still occur.
3. **REPEATABLE READ**: Ensures that if a row is read twice in a transaction, it will always return the same result. However, phantom reads (new rows being added by other transactions) can still occur.
4. **SERIALIZABLE**: The highest isolation level. It ensures that transactions are completely isolated from each other, preventing dirty reads, non-repeatable reads, and phantom reads.

You can set the isolation level in JDBC like this:

```java
connection.setTransactionIsolation(Connection.TRANSACTION_SERIALIZABLE);
```

### Configuring Transaction Isolation Levels

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#configuring-transaction-isolation-levels)

You can configure different isolation levels using the `Connection.setTransactionIsolation(int level)` method. The isolation level constants provided by the `Connection` interface are:

- `Connection.TRANSACTION_READ_UNCOMMITTED`
- `Connection.TRANSACTION_READ_COMMITTED`
- `Connection.TRANSACTION_REPEATABLE_READ`
- `Connection.TRANSACTION_SERIALIZABLE`

### Example of Setting Different Isolation Levels

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#example-of-setting-different-isolation-levels)

```java
// Set the isolation level to READ UNCOMMITTED (allows dirty reads)
connection.setTransactionIsolation(Connection.TRANSACTION_READ_UNCOMMITTED);

// Set the isolation level to READ COMMITTED (prevents dirty reads)
connection.setTransactionIsolation(Connection.TRANSACTION_READ_COMMITTED);

// Set the isolation level to REPEATABLE READ (prevents non-repeatable reads)
connection.setTransactionIsolation(Connection.TRANSACTION_REPEATABLE_READ);

// Set the isolation level to SERIALIZABLE (prevents phantom reads)
connection.setTransactionIsolation(Connection.TRANSACTION_SERIALIZABLE);
```

________________________________________________________________________

## Transaction propagation levels

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#transaction-propagation-levels)

Transaction propagation levels determine how transactions behave when a method with an existing transaction calls another method that starts a new transaction. In the context of Spring or Java EE frameworks that provide declarative transaction management (e.g., using `@Transactional` annotation in Spring), different propagation levels define the interaction between the current and the newly created transactions.

Here are the transaction propagation levels in Spring:

1. **REQUIRED**:
    
    - If a transaction already exists, the method joins it.
    - If there’s no existing transaction, a new one is created.
    - This is the default behavior.
2. **REQUIRES_NEW**:
    
    - Always creates a new transaction, suspending the existing one (if any).
    - The new transaction runs independently of the original one, so changes in one transaction don't affect the other.
3. **SUPPORTS**:
    
    - If a transaction exists, the method joins it.
    - If no transaction exists, the method runs without one.
    - It neither forces the creation of a new transaction nor suspends any existing ones.
4. **NOT_SUPPORTED**:
    
    - The method does not execute within a transaction.
    - If an existing transaction is running, it gets suspended for the duration of this method.
5. **MANDATORY**:
    
    - Requires an existing transaction to be present.
    - If no transaction is found, an exception is thrown (`TransactionRequiredException`).
6. **NEVER**:
    
    - The method must not be called within a transaction.
    - If an existing transaction is found, an exception is thrown (`IllegalTransactionStateException`).
7. **NESTED**:
    
    - If a transaction exists, it creates a new nested transaction within the existing one.
    - If there’s no existing transaction, it behaves like `REQUIRED`.
    - Nested transactions allow for committing or rolling back the inner transaction without affecting the outer transaction.

In Spring, the `@Transactional` annotation is used to define the propagation behavior.

```
example :
@Transactional(propagation = Propagation.REQUIRED)
    public void requiredTransaction() {
        // This method will join an existing transaction, or create a new one if none exists
    }
```



### Choosing the Right Propagation Level

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#choosing-the-right-propagation-level)

- Use **REQUIRED** when you want the called method to share the caller's transaction.
- Use **REQUIRES_NEW** when you want a new independent transaction.
- Use **SUPPORTS** when the called method can either participate in an existing transaction or run without one.
- Use **NESTED** when you want to create a sub-transaction that can roll back independently.
- Use **MANDATORY** to ensure that a transaction is always present.
- Use **NEVER** or **NOT_SUPPORTED** when a method must not or should not run in a transaction.


________________________________________________________________________
### Relationship Between **Optimistic/Pessimistic Locking** and **Transaction Isolation Levels**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture8-jdbc-with-java.md#relationship-between-optimisticpessimistic-locking-and-transaction-isolation-levels)

1. **Transaction Isolation Levels**: Control the visibility of data changes between transactions. They determine what one transaction can see of another transaction's work (uncommitted or committed changes) and how transaction boundaries are enforced. The isolation levels include:
    
    - **READ UNCOMMITTED**
    - **READ COMMITTED**
    - **REPEATABLE READ**
    - **SERIALIZABLE**
2. **Optimistic and Pessimistic Locking**: Directly control how **locks** are managed on database records during a transaction to avoid conflicting updates, typically at the application level, independent of the database’s internal isolation mechanisms.
________________________________________________________________________


# Spring JDBC


### Core Components

1. **`JdbcTemplate`:**
    
    - Simplifies JDBC code by handling the boilerplate logic for establishing connections, executing SQL queries, and mapping results to objects.
2. **DAO Support Classes:**
    
    - Spring provides DAO support classes for ORM frameworks (e.g., `HibernateDaoSupport` for Hibernate and `JpaDaoSupport` for JPA).
3. **Exception Hierarchy:**
    
    - A unified exception translation layer converts specific persistence-related exceptions into a common exception hierarchy (`DataAccessException`).

### Example of Spring DAO with `JdbcTemplate`

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture23-spring-jdbc.md#example-of-spring-dao-with-jdbctemplate)

```java
@Repository // Indicates that this class is a DAO
public class EmployeeDAO {

    @Autowired
    private JdbcTemplate jdbcTemplate;

    public List<Employee> getAllEmployees() {
        String sql = "SELECT * FROM employees";
        return jdbcTemplate.query(sql, new BeanPropertyRowMapper<>(Employee.class));
    }

    public int addEmployee(Employee employee) {
        String sql = "INSERT INTO employees (name, age, department) VALUES (?, ?, ?)";
        return jdbcTemplate.update(sql, employee.getName(), employee.getAge(), employee.getDepartment());
    }
}
```

### Benefits

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture23-spring-jdbc.md#benefits)

1. **Reduced Boilerplate Code:**
    - Eliminates the need for repetitive and verbose data access code.
2. **Ease of Integration:**
    - Works with multiple data access technologies (JDBC, Hibernate, JPA, etc.).
3. **Improved Maintainability:**
    - Consistent API and exception handling make code easier to maintain.
4. **Loose Coupling:**
    - Abstracts away the specific implementation details of the persistence layer, allowing for easier technology replacement.

Spring DAO is a vital tool for developers looking to build efficient, maintainable, and scalable data access layers in enterprise applications.

Here’s a step-by-step guide to build a sample **Spring JDBC project using `JdbcTemplate`**. We'll create a simple Employee Management application that allows CRUD operations on an **Employee** table in a database.

---

### **1. Project Setup**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture23-spring-jdbc.md#1-project-setup)

#### **Dependencies**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture23-spring-jdbc.md#dependencies)

Add the following dependencies to your `pom.xml` (if using Maven):

```xml
<dependencies>
    <!-- Spring Context for Core Spring features -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>6.0.2</version>
    </dependency>

    <!-- Spring JDBC for JdbcTemplate -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>6.0.2</version>
    </dependency>

    <!-- MySQL JDBC Driver -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.33</version>
    </dependency>

    <!-- HikariCP (Optional, for connection pooling) -->
    <dependency>
        <groupId>com.zaxxer</groupId>
        <artifactId>HikariCP</artifactId>
        <version>5.0.1</version>
    </dependency>
</dependencies>
```

---

### **2. Database Setup**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture23-spring-jdbc.md#2-database-setup)

Create a database and a table.

```sql
CREATE DATABASE spring_jdbc_demo;

USE spring_jdbc_demo;

CREATE TABLE employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    department VARCHAR(50)
);
```

---

### **3. Application Code**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture23-spring-jdbc.md#3-application-code)

#### **Configuration with Java-based Spring**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture23-spring-jdbc.md#configuration-with-java-based-spring)

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.datasource.DriverManagerDataSource;

import javax.sql.DataSource;

@Configuration
//@ComponentScan("io.reactivestax.repo", "io.reactivestax.service")

public class AppConfig {

  		//DB related 
    @Bean
    public DataSource dataSource() {
        DriverManagerDataSource dataSource = new DriverManagerDataSource();
        dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
        dataSource.setUrl("jdbc:mysql://localhost:3306/spring_jdbc_demo");
        dataSource.setUsername("root"); // Replace with your DB username
        dataSource.setPassword("password"); // Replace with your DB password
        return dataSource;
      
      //HikariCP if you need better connection pooling etc.
      @Bean
      public DataSource dataSource() {
          HikariDataSource dataSource = new HikariDataSource();
          dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
          dataSource.setJdbcUrl("jdbc:mysql://localhost:3306/spring_jdbc_demo");
          dataSource.setUsername("root");
          dataSource.setPassword("password");

          // Connection pooling settings
          dataSource.setMaximumPoolSize(10);
          dataSource.setMinimumIdle(2);
          dataSource.setIdleTimeout(30000); // 30 seconds
          dataSource.setConnectionTimeout(20000); // 20 seconds
          return dataSource;
      }  
    }

    @Bean
    public JdbcTemplate jdbcTemplate(DataSource dataSource) {
        return new JdbcTemplate(dataSource);
    }
  
     //Service layer related 
  
     //Controller layer related
}
```

---

#### **DAO Layer**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture23-spring-jdbc.md#dao-layer)

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.core.RowMapper;
import org.springframework.stereotype.Repository;

import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.List;

@Repository  // (@Component, @Service)
public class EmployeeDAO {

    @Autowired
    private JdbcTemplate jdbcTemplate;

    // Add Employee
    public int addEmployee(Employee employee) {
        String sql = "INSERT INTO employees (name, age, department) VALUES (?, ?, ?)";
        return jdbcTemplate.update(sql, employee.getName(), employee.getAge(), employee.getDepartment());
    }

    // Get All Employees
    public List<Employee> getAllEmployees() {
        String sql = "SELECT * FROM employees";
        return jdbcTemplate.query(sql, new EmployeeRowMapper());
    }

    // Update Employee
    public int updateEmployee(Employee employee) {
        String sql = "UPDATE employees SET name = ?, age = ?, department = ? WHERE id = ?";
        return jdbcTemplate.update(sql, employee.getName(), employee.getAge(), employee.getDepartment(), employee.getId());
    }

    // Delete Employee
    public int deleteEmployee(int id) {
        String sql = "DELETE FROM employees WHERE id = ?";
        return jdbcTemplate.update(sql, id);
    }

    // Custom RowMapper
    private static class EmployeeRowMapper implements RowMapper<Employee> {
        @Override
        public Employee mapRow(ResultSet rs, int rowNum) throws SQLException {
            Employee employee = new Employee();
            employee.setId(rs.getInt("id"));
            employee.setName(rs.getString("name"));
            employee.setAge(rs.getInt("age"));
            employee.setDepartment(rs.getString("department"));
            return employee;
        }
    }
}
```

---

#### **Entity Class**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture23-spring-jdbc.md#entity-class)

```java
public class Employee {
    private int id;
    private String name;
    private int age;
    private String department;

    // Getters and Setters
    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getDepartment() {
        return department;
    }

    public void setDepartment(String department) {
        this.department = department;
    }
}
```

---

#### **Main Application**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture23-spring-jdbc.md#main-application)

```java
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

import java.util.List;

public class SpringJdbcApp {
    public static void main(String[] args) {
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
      //if AppConfig.class was replaced with application-context.xml it can get 
      // loaded with ClassPathXMLApplicationContext instead 
      // you will need to create application-context.xml to replace the AppConfig
        EmployeeDAO employeeDAO = context.getBean(EmployeeDAO.class);

        // Add Employees
        employeeDAO.addEmployee(new Employee(0, "Alice", 30, "HR"));
        employeeDAO.addEmployee(new Employee(0, "Bob", 25, "IT"));

        // Get All Employees
        List<Employee> employees = employeeDAO.getAllEmployees();
        employees.forEach(emp -> System.out.println(emp.getName() + " works in " + emp.getDepartment()));

        // Update Employee
        Employee empToUpdate = employees.get(0);
        empToUpdate.setDepartment("Finance");
        employeeDAO.updateEmployee(empToUpdate);

        // Delete Employee
        employeeDAO.deleteEmployee(employees.get(1).getId());

        context.close();
    }
}
```

run this in a spring boot application . 

==try to write the CRUD for Employee in the DAO layer using jdbc template 




Here’s a table summarizing the division of responsibilities between **Spring JDBC** and the **Developer**:

| **Responsibility**                 | **Spring JDBC**                                                                                           | **Developer**                                                                                          |
| ---------------------------------- | --------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| **Database Connection Management** | Automatically manages database connections, including opening and closing connections.                    | Configures the `DataSource` (e.g., connection details like URL, username, password).                   |
| **SQL Execution**                  | Executes SQL queries (e.g., `SELECT`, `INSERT`, `UPDATE`, `DELETE`) via the `JdbcTemplate` API.           | Writes the SQL queries for specific operations.                                                        |
| **Transaction Management**         | Provides declarative or programmatic transaction management using Spring's transaction abstraction.       | Configures transaction boundaries if needed, such as annotating methods with `@Transactional`.         |
| **Error Handling**                 | Converts database-specific exceptions (e.g., `SQLException`) into Spring’s unified `DataAccessException`. | Implements custom logic for handling application-level errors, using the translated exceptions.        |
| **Resource Management**            | Automatically manages resources like connections, statements, and result sets to prevent leaks.           | No involvement; Spring ensures resources are properly handled and closed.                              |
| **Row Mapping**                    | Provides helper interfaces (`RowMapper`, `ResultSetExtractor`) for mapping database rows to objects.      | Defines mapping logic (e.g., custom `RowMapper` implementation for mapping columns to object fields).  |
| **Prepared Statement Creation**    | Handles the creation and execution of prepared statements transparently.                                  | Passes parameters to prepared statements in queries using Spring’s `JdbcTemplate` methods.             |
| **Connection Pooling**             | Can integrate with third-party connection pools like HikariCP.                                            | Configures the connection pool settings (e.g., max pool size, timeout) if connection pooling is used.  |
| **Logging**                        | Logs SQL queries and execution details (if configured in logging framework).                              | Configures the logging framework (e.g., Log4j, SLF4J) for debugging or monitoring database operations. |
| **Exception Propagation**          | Wraps checked exceptions into unchecked exceptions to avoid verbose try-catch blocks.                     | Writes code to handle exceptions appropriately based on business logic.                                |
| **Performance Optimization**       | Optimizes repetitive tasks like creating prepared statements and managing result sets.                    | Writes efficient SQL queries and indexes database tables for better performance.                       |