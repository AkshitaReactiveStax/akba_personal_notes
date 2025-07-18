
You’re on 🔥 Akshita — and here’s your **final boss-level OAuth 2.0 + OIDC Interview Checklist** ✅

Perfectly structured for **Java/Spring Security + backend engineering interviews**, this covers **OAuth 2.0 flows**, **JWT**, **Spring implementation**, **PKCE**, **token validation**, and **real-world system integration** with Okta, Keycloak, Auth0, etc.

---

## **✅ OAUTH 2.0 + OIDC INTERVIEW MASTER LIST**

  

_Everything you must know — protocol, flows, Spring integration, JWT, and security edge cases_

---

### **🔹 1.** 

### **OAuth 2.0 Basics**

- What is OAuth 2.0? Why is it needed?
    
- Roles in OAuth 2.0:
    
    - **Resource Owner** (user)
        
    - **Client** (frontend/backend app)
        
    - **Authorization Server** (e.g., Keycloak, Okta)
        
    - **Resource Server** (your backend API)
        
    
- Authorization vs Authentication (why OAuth ≠ Auth by default)
    
- OAuth vs SAML vs OpenID Connect (OIDC)
    

  

🧠 _Q_: Can OAuth be used for authentication?

---

### **🔹 2.** 

### **OAuth 2.0 Grant Types (Flows)**

  

#### **🟢** 

#### **1. Authorization Code Flow (with PKCE)**

- Most secure, used by web and mobile apps
    
- Steps:
    
    1. Client → Auth server (get code)
        
    2. Client → Auth server (exchange code for token)
        
    
- **PKCE** (Proof Key for Code Exchange):
    
    - Adds security for public clients (mobile, SPA)
        
    - code_verifier, code_challenge
        
    

  

🧠 _Q_: Why is PKCE important even for SPAs?

---

#### **🟡** 

#### **2. Client Credentials Flow**

- Machine-to-machine (M2M) communication
    
- No user involved
    
- Uses client ID & secret
    
- Common for microservices or backend tasks
    

  

🧠 _Q_: When would you use client credentials flow in microservices?

---

#### **🔵** 

#### **3. Password Grant (deprecated)**

- Directly exchanging user credentials for tokens
    
- High risk, discouraged (only for internal apps)
    
- Deprecated in OAuth 2.1
    

  

🧠 _Q_: Why is password grant discouraged?

---

#### **🟣** 

#### **4. Implicit Flow (deprecated)**

- Used in SPAs (tokens returned in redirect URL)
    
- No refresh token → less secure
    
- Replaced by Authorization Code Flow + PKCE
    

  

🧠 _Q_: Why was implicit flow removed in OAuth 2.1?

---

#### **🟤** 

#### **5. Refresh Token Flow**

- Keeps user logged in without re-authentication
    
- Client stores refresh token securely
    
- Exchange refresh token for new access token
    

  

🧠 _Q_: Can a refresh token be reused multiple times?

---

### **🔹 3.** 

### **Tokens in OAuth 2.0**

- **Access Token**:
    
    - Short-lived, used to access APIs
        
    - Typically a JWT
        
    
- **Refresh Token**:
    
    - Long-lived, used to get new access token
        
    
- **ID Token** (from OIDC):
    
    - Contains user identity claims (for authentication)
        
    

  

🧠 _Q_: What’s the difference between an ID token and an access token?

---

### **🔹 4.** 

### **JWT (JSON Web Token)**

- Structure: Header, Payload, Signature
    
- Claims: sub, iss, aud, exp, custom claims
    
- Signed with HMAC (symmetric) or RSA (asymmetric)
    
- Validating JWT:
    
    - Signature check
        
    - Expiry (exp)
        
    - Audience and issuer
        
    

  

🧠 _Q_: How does a backend API validate a JWT issued by Auth0 or Okta?

---

### **🔹 5.** 

### **Spring Security + OAuth2**

- Resource server config (@EnableResourceServer)
    
- Using spring-boot-starter-oauth2-resource-server
    
- spring.security.oauth2.resourceserver.jwt.jwk-set-uri
    
- Custom JWT claims mapping (JwtAuthenticationConverter)
    
- Securing endpoints:
    
    - @PreAuthorize("hasAuthority('SCOPE_read')")
        
    
- OAuth2 client config (@EnableOAuth2Client, newer spring.security.oauth2.client.*)
    
- Supporting multiple grant types
    

  

🧠 _Q_: How do you validate a JWT with Spring Boot using JWKS URI?

---

### **🔹 6.** 

### **OpenID Connect (OIDC)**

- Extension of OAuth 2.0 for **authentication**
    
- ID Token → proves identity
    
- Discovery URL (/.well-known/openid-configuration)
    
- Scope: openid, email, profile
    
- Single Sign-On (SSO) & Logout URL
    

  

🧠 _Q_: How does OIDC enable SSO across multiple apps?

---

### **🔹 7.** 

### **Security Concepts & Best Practices**

- Token expiration and refresh rotation
    
- Storing tokens securely (no localStorage for refresh tokens)
    
- Using HTTPS for all token exchanges
    
- Validating issuer, audience, and signature
    
- Avoiding token leakage in URLs
    
- Using state and nonce to prevent replay attacks
    

  

🧠 _Q_: How do you secure a public client (e.g., SPA or mobile app)?

---

### **🔹 8.** 

### **Third-Party OAuth Providers (Real-World Integration)**

- Okta, Auth0, Keycloak, Azure AD, Google Identity
    
- Setting up clients and redirect URIs
    
- Configuring scopes and claims
    
- Using tools like Postman or Swagger with bearer token auth
    

  

🧠 _Q_: What’s the difference between Auth0 and Keycloak in terms of architecture?

---

### **🔹 9.** 

### **Troubleshooting & Debugging**

- Common errors: invalid_grant, invalid_client, unauthorized_client
    
- Expired vs invalid vs malformed token
    
- Misconfigured redirect URIs
    
- Clock skew causing exp validation errors
    

  

🧠 _Q_: Why do I get a 401 with a valid JWT?

---

Would you like a **flow diagram** of all OAuth 2.0 flows, or a **sample Spring Boot + Keycloak/OIDC secure app setup** next?