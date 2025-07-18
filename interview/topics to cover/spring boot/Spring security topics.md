You’ve got it, Akshita — here is your **Spring Security Deep Dive Master Checklist**, built to ensure **nothing is missed** for any level of backend interview. This list is focused on **real-world enterprise setups**, **interview traps**, and **Spring Boot Security configurations** — including JWT, OAuth2, filters, and annotations.

---

## **✅ SPRING SECURITY INTERVIEW MASTER LIST**

  

_Includes: Filters, JWT, OAuth2, Annotations, Config, CSRF, CORS, and more_

---

### **🔹 1.** 

### **Core Concepts: Authentication vs Authorization**

- **Authentication**: Are you who you say you are?
    
- **Authorization**: What are you allowed to access?
    
- Principals, Credentials, Roles (Authorities)
    
- SecurityContext, Authentication, and GrantedAuthority
    

  

🧠 _Q_: What’s the difference between ROLE_ADMIN and hasAuthority("ADMIN")?

---

### **🔹 2.** 

### **Authentication Providers**

- In-memory authentication (useful for testing)
    
- JDBC authentication (fetching from DB)
    
- Custom UserDetailsService + UserDetails
    
- PasswordEncoder strategies (BCryptPasswordEncoder)
    
- DAO Authentication Provider
    
- AuthenticationManagerBuilder (pre-Spring Security 5.7)
    
- AuthenticationManager bean (post 5.7+)
    

  

🧠 _Q_: How do you hash passwords securely in Spring?

---

### **🔹 3.** 

### **JWT-Based Authentication**

- What is JWT? Structure: Header, Payload, Signature
    
- Stateless security: no session, token passed with each request
    
- Token generation & signing (HMAC/RSA)
    
- Token validation in filter
    
- Using Authorization: Bearer <token> header
    
- Custom OncePerRequestFilter to extract and authenticate user from JWT
    
- Token expiration and refresh
    

  

🧠 _Q_: Where and when should you parse the JWT?

---

### **🔹 4.** 

### **Custom Filters & Stateless Authentication**

- Security filter chain and ordering
    
- Replacing or extending UsernamePasswordAuthenticationFilter
    
- Writing a custom OncePerRequestFilter for JWT
    
- Stateless flow: authenticate on every request
    
- Disabling session creation
    
- Using SecurityContextHolder with Authentication object
    

  

🧠 _Q_: Why do we use OncePerRequestFilter for JWT?

---

### **🔹 5.** 

### **Authorization: Role-Based Access Control**

- @Secured("ROLE_USER")
    
- @PreAuthorize("hasRole('ADMIN')")
    
- @PostAuthorize, @PostFilter
    
- Expression-based access control
    
- Global method security (@EnableGlobalMethodSecurity)
    
- Role hierarchy configuration
    

  

🧠 _Q_: How is @Secured different from @PreAuthorize?

---

### **🔹 6.** 

### **Method-Level Security**

- Enabling with @EnableMethodSecurity (Spring Security 6+)
    
- @PreAuthorize, @PostAuthorize
    
- Security expressions:
    
    - hasRole(), hasAuthority(), isAuthenticated()
        
    - authentication.name == #username
        
    
- Access control based on method arguments
    

  

🧠 _Q_: Can you restrict access to a method based on path variable?

---

### **🔹 7.** 

### **CSRF Protection**

- What is CSRF?
    
- Enabled by default for non-GET requests
    
- Why disable in stateless APIs (e.g., JWT)?
    
- CSRF token generation and validation
    
- CSRF with session-based apps vs REST APIs
    

  

🧠 _Q_: When should you **not** disable CSRF?

---

### **🔹 8.** 

### **CORS Handling**

- What is CORS? Why do we get CORS errors?
    
- Allowing cross-origin requests safely
    
- Configuring CORS globally in Spring Security
    
- CorsConfigurationSource, CorsFilter
    
- CORS + JWT usage scenarios
    

  

🧠 _Q_: What’s the difference between a CORS filter and a Spring filter?

---

### **🔹 9.** 

### **Security Configuration Styles**

- Deprecated: Extending WebSecurityConfigurerAdapter (pre-Spring Security 5.7)
    
- Recommended: SecurityFilterChain bean (post Spring Boot 2.7/Security 6+)
    
- Define:
    
    - AuthenticationManager
        
    - PasswordEncoder
        
    - SecurityFilterChain (authorize requests, CSRF, CORS, session policy)
        
    

  

🧠 _Q_: How do you configure custom authentication without extending WebSecurityConfigurerAdapter?

---

### **🔹 10.** 

### **Spring Security with OAuth2**

- What is OAuth2? (Authorization Code, Client Credentials)
    
- Resource Server vs Authorization Server
    
- Spring Security OAuth2 Client:
    
    - GitHub/Google login with spring.security.oauth2.client.registration
        
    
- Spring Security OAuth2 Resource Server:
    
    - Validating JWTs from external IdP (Okta, Auth0, Keycloak)
        
    - spring.security.oauth2.resourceserver.jwt
        
    

  

🧠 _Q_: What’s the difference between OAuth2 and JWT? Can they be used together?

---

### **🔹 11.** 

### **Form Login, Logout & Remember Me**

- Custom login pages
    
- formLogin() and httpBasic() configuration
    
- Configuring logout URL and redirect
    
- rememberMe() configuration
    

  

🧠 _Q_: How does Spring Security handle session vs remember-me cookies?

---

### **🔹 12.** 

### **Session Management & Concurrency Control**

- Stateless (SessionCreationPolicy.STATELESS) vs stateful
    
- Session fixation protection
    
- Maximum concurrent sessions per user
    
- Logout on session expiration
    

  

🧠 _Q_: Can you prevent multiple logins for the same user?

---

### **🔹 13.** 

### **Security for REST APIs (Best Practices)**

- Stateless security with JWT
    
- Disabling CSRF
    
- Using exception translation filters
    
- Handling 401 vs 403
    
- Using AuthenticationEntryPoint and AccessDeniedHandler
    

---

Would you like this in a progress tracker checklist or want to deep dive into **JWT implementation in Spring Boot**, **OAuth2 flow**, or **Spring Security filter chain customization** next?