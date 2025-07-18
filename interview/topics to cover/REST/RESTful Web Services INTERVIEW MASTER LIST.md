
Blame-proof REST checklist coming up 🔥 — this is your **Ultimate RESTful Web Services Interview Syllabus**, covering **everything you need to know** to ace REST API interviews (especially when paired with Spring Boot).

---

## **✅ RESTful Web Services INTERVIEW MASTER LIST**

  

_For Java/Spring Boot Developers – enterprise and startup-ready_

---

### **🔹 1.** 

### **REST Architectural Principles**

- What is REST?
    
- Six constraints of REST:
    
    1. **Statelessness**
        
    2. **Client-server separation**
        
    3. **Uniform interface**
        
    4. **Cacheability**
        
    5. **Layered system**
        
    6. **Code on demand (optional)**
        
    
- Why statelessness is important in REST
    

  

🧠 _Interview Question_: Why is REST stateless and what does it imply?

---

### **🔹 2.** 

### **HTTP Methods (Verbs)**

- GET: retrieve resource
    
- POST: create resource
    
- PUT: update (replace) resource
    
- PATCH: partial update
    
- DELETE: remove resource
    
- OPTIONS, HEAD
    

  

🧠 _Q_: When should you use PUT vs PATCH? Is GET idempotent?

---

### **🔹 3.** 

### **HTTP Status Codes**

- 2xx: Success
    
    - 200 OK
        
    - 201 Created
        
    - 204 No Content
        
    
- 4xx: Client Errors
    
    - 400 Bad Request
        
    - 401 Unauthorized
        
    - 403 Forbidden
        
    - 404 Not Found
        
    - 409 Conflict
        
    
- 5xx: Server Errors
    
    - 500 Internal Server Error
        
    - 502 Bad Gateway
        
    - 503 Service Unavailable
        
    

  

🧠 _Q_: When would you return 204 vs 200? Difference between 401 and 403?

---

### **🔹 4.** 

### **Idempotency & Safety**

- Safe methods: GET, HEAD, OPTIONS
    
- Idempotent methods: GET, PUT, DELETE, HEAD, OPTIONS
    
- Non-idempotent: POST, PATCH
    
- Importance in retries and network failures
    

  

🧠 _Q_: Is DELETE really idempotent? Why does it matter?

---

### **🔹 5.** 

### **Request/Response Design**

- REST URI conventions: /resources, /resources/{id}
    
- Naming resources (nouns, not verbs)
    
- HTTP headers: Content-Type, Accept, Authorization, ETag
    
- Proper use of request bodies and query parameters
    
- Response structure: consistent JSON, status + data + errors
    

  

🧠 _Q_: Should you include verbs in URI? What if you need custom actions?

---

### **🔹 6.** 

### **Pagination, Filtering, Sorting**

- Pagination:
    
    - ?page=0&size=10
        
    - Link header (RFC 5988)
        
    
- Sorting: ?sort=name,asc
    
- Filtering: ?status=active&category=tech
    
- Spring Data REST + Pageable
    

  

🧠 _Q_: How do you implement pagination in REST? How to avoid over-fetching?

---

### **🔹 7.** 

### **Versioning REST APIs**

- URI versioning: /api/v1/resource
    
- Header versioning: Accept: application/vnd.company.v1+json
    
- Query parameter versioning (least preferred)
    
- Content negotiation with Accept header
    

  

🧠 _Q_: Which versioning strategy is most RESTful?

---

### **🔹 8.** 

### **Error Handling**

- Standard error structure: timestamp, status, message, path
    
- @ControllerAdvice + @ExceptionHandler in Spring
    
- HTTP status + descriptive error body
    
- RFC 7807 – Problem Details for HTTP APIs
    

  

🧠 _Q_: How would you structure an API error response for a bad request?

---

### **🔹 9.** 

### **HATEOAS (Hypermedia as the Engine of Application State)**

- What is HATEOAS in REST?
    
- Adding self, next, prev links to resources
    
- Spring HATEOAS library (EntityModel, CollectionModel)
    
- Practical usage vs overengineering
    

  

🧠 _Q_: When is HATEOAS useful? Is it overkill for modern frontend apps?

---

### **🔹 10.** 

### **REST vs SOAP**

- Protocol: REST over HTTP, SOAP over multiple protocols (HTTP, SMTP)
    
- Message format: JSON (REST) vs XML (SOAP)
    
- Standards: SOAP has WSDL, WS-Security, etc.
    
- Flexibility, readability, learning curve
    
- REST is lighter and more web-native
    

  

🧠 _Q_: Why would a bank still use SOAP instead of REST?

---

### **🔹 11.** 

### **Security in REST APIs**

- Basic Authentication (Authorization header)
    
- Bearer Tokens (JWT)
    
- Role-based access control
    
- CSRF protection in stateful APIs
    
- CORS handling
    
- HTTPS requirement
    

  

🧠 _Q_: How do you secure public vs internal REST endpoints?

---

### **🔹 12.** 

### **OpenAPI/Swagger Documentation**

- What is Swagger/OpenAPI 3.0?
    
- Auto-generation in Spring Boot using springdoc-openapi
    
- Annotations: @Operation, @ApiResponse, @Schema, @Parameter
    
- Try-it-out UI for testing
    

  

🧠 _Q_: How would you document a secured endpoint in Swagger?

---

### **🔹 13.** 

### **Best Practices**

- Don’t expose internal DB IDs if not needed
    
- Version APIs early
    
- Consistent naming and casing
    
- Always return proper status codes
    
- Avoid over-fetching; use filtering, pagination
    
- Separate error vs validation response formats
    
- Include ETag or caching headers when needed
    

---

Would you like this turned into a checklist or start with mock questions from any of these sections (like pagination, idempotency, or status codes)?