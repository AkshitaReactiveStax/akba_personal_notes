
You got it! Here’s your **Ultimate, Blame-Proof Java Testing Interview Checklist**, covering **JUnit 5**, **Mockito**, and **Spring Boot Testing** — including **Testcontainers**, annotations, and best practices that top companies grill you on.

---

## **✅ JAVA TESTING MASTER LIST**

  

_Includes: Unit Testing, Integration Testing, Mockito, Spring Boot, and Testcontainers_

---

### **🔹 1.** 

### **JUnit 5 Basics (a.k.a. Jupiter)**

- JUnit 5 architecture (Jupiter, Vintage, Platform)
    
- Key annotations:
    
    - @Test, @BeforeEach, @AfterEach
        
    - @BeforeAll, @AfterAll, @DisplayName
        
    
- Assertions:
    
    - assertEquals, assertTrue, assertThrows, assertAll, assertTimeout
        
    
- Nested tests: @Nested
    
- Conditional test execution:
    
    - @EnabledOnOs, @DisabledIfEnvironmentVariable, etc.
        
    
- Parameterized tests:
    
    - @ParameterizedTest, @ValueSource, @CsvSource, @MethodSource
        
    

  

🧠 _Q_: What’s the difference between @BeforeEach and @BeforeAll?

---

### **🔹 2.** 

### **Mockito (Mocking Framework)**

- Creating mocks:
    
    - @Mock, mock(), @Spy, @InjectMocks
        
    
- Stubbing behavior:
    
    - when().thenReturn(), thenThrow()
        
    - doReturn().when() for spies
        
    
- Verifying interactions:
    
    - verify(), verifyNoInteractions(), verifyZeroInteractions()
        
    
- Argument matchers:
    
    - any(), eq(), anyString(), argThat()
        
    
- Capturing arguments:
    
    - ArgumentCaptor
        
    
- Mocking void methods:
    
    - doNothing(), doThrow(), doAnswer()
        
    

  

🧠 _Q_: How do you test a method that calls another void method internally?

---

### **🔹 3.** 

### **Testing Exceptions & Edge Cases**

- Using assertThrows() in JUnit 5
    
- Verifying exception messages
    
- Custom exceptions and exception mapping
    
- Boundary value and negative tests
    

  

🧠 _Q_: How do you validate the cause/message of an exception?

---

### **🔹 4.** 

### **Spring Boot Testing Annotations**

|**Annotation**|**Purpose**|
|---|---|
|@SpringBootTest|Full integration test with Spring context|
|@WebMvcTest|For controller layer only (mocked services)|
|@DataJpaTest|For JPA repositories only|
|@MockBean|Spring-context-safe mocking|
|@SpyBean|Spy real bean inside Spring context|
|@TestConfiguration|Define additional beans for test only|
|@AutoConfigureMockMvc|Enables MockMvc for full controller tests|

🧠 _Q_: Why would you prefer @WebMvcTest over @SpringBootTest?

---

### **🔹 5.** 

### **MockMvc (Controller Layer Testing)**

- Standalone setup vs Spring context setup
    
- mockMvc.perform(...)
    
- Testing:
    
    - Status codes
        
    - JSON body assertions (jsonPath)
        
    - Request params, headers, path variables
        
    - Content negotiation
        
    

  

🧠 _Q_: How do you test controller validation errors using MockMvc?

---

### **🔹 6.** 

### **Database Testing**

- In-memory DBs: H2 for test profile
    
- @DataJpaTest with auto-rollback
    
- Testing custom repository methods
    
- SQL script loading: @Sql
    
- Verifying DB state with assertions
    
- Transactional rollback for isolation
    

  

🧠 _Q_: How do you test pagination and sorting in JPA?

---

### **🔹 7.** 

### **Testcontainers (Advanced Integration Testing)**

- What is Testcontainers?
    
- Starting real DBs (PostgreSQL, MySQL), Kafka, Redis in Docker containers
    
- Replacing H2 with real PostgreSQL for integration test
    
- Using @Container and @DynamicPropertySource
    
- Running isolated tests with real services
    

  

🧠 _Q_: Why would you use Testcontainers instead of H2?

---

### **🔹 8.** 

### **Best Practices & Patterns**

- Arrange-Act-Assert (AAA) pattern
    
- Naming conventions: shouldDo_X_When_Y
    
- Keeping tests isolated (no DB/data dependencies)
    
- Avoiding over-mocking
    
- Test coverage tools: JaCoCo
    
- Mutant testing tools (e.g., PIT)
    
- Assertions libraries: AssertJ, Hamcrest
    

  

🧠 _Q_: How do you decide what to mock in a layered architecture?

---

### **🔹 9.** 

### **Testing with Profiles & Configurations**

- @ActiveProfiles("test")
    
- application-test.yml for isolated config
    
- Overriding properties with @TestPropertySource
    
- Disabling beans during test with @ConditionalOnProperty
    

  

🧠 _Q_: How do you avoid hitting external APIs in integration tests?

---

Would you like this in **Excel checklist format** or want to dive into **writing JUnit 5 + Mockito test** for one of your own classes?