You got it, Akshita — here’s your **Blame-Proof Docker & Containers Interview Checklist** ✅

Built specifically for **Java/Spring Boot backend engineers**, this covers **everything** interviewers expect: containers, Dockerfiles, networking, Docker Compose, volumes, and real-world DevOps use.

---

## **✅ DOCKER & CONTAINERS INTERVIEW MASTER LIST**

  

_For backend interviews involving microservices, DevOps, or containerized deployments_

---

### **🔹 1.** 

### **What is Docker? Why Use It?**

- What is a container?
    
- Benefits of Docker:
    
    - Lightweight, fast startup
        
    - Consistent environment
        
    - Portable and reproducible builds
        
    
- Differences:
    
    - Docker vs Virtual Machine (VM)
        
    - Docker vs Kubernetes (basic)
        
    - Image vs Container vs Layer
        
    

  

🧠 _Q_: How does Docker ensure the “works on my machine” issue is solved?

---

### **🔹 2.** 

### **Dockerfile & Image Fundamentals**

- Dockerfile instructions:
    
    - FROM, RUN, COPY, ADD, CMD, ENTRYPOINT, ENV, EXPOSE, WORKDIR
        
    
- CMD vs ENTRYPOINT
    
- Multi-stage builds (build + slim runtime)
    
- Layer caching (Docker image build optimization)
    
- Base images (openjdk, alpine, distroless, etc.)
    

  

🧠 _Q_: Why is ENTRYPOINT used for Spring Boot apps over CMD?

---

### **🔹 3.** 

### **Building & Running Containers**

- docker build -t myapp .
    
- docker run options:
    
    - -d, -p, --name, -v, -e, --rm
        
    
- Viewing logs: docker logs <container>
    
- Inspecting containers: docker ps, docker inspect, docker exec
    

  

🧠 _Q_: How do you debug a failing container?

---

### **🔹 4.** 

### **Ports, Environment Variables & Volumes**

- Exposing internal ports (EXPOSE 8080) vs publishing ports (-p 8080:8080)
    
- Passing environment variables:
    
    - ENV in Dockerfile
        
    - -e flag or .env file at runtime
        
    
- Volumes:
    
    - Anonymous vs named
        
    - Bind mounts vs volumes
        
    - Persisting data across restarts
        
    - Mounting config files (e.g., application.yml)
        
    

  

🧠 _Q_: When would you use a volume over a bind mount?

---

### **🔹 5.** 

### **Docker Compose**

- docker-compose.yml structure:
    
    - services, build, image, ports, volumes, depends_on, environment
        
    
- Starting multi-container setups (Spring Boot + PostgreSQL + Redis)
    
- Lifecycle: up, down, logs, exec, restart
    
- Override with .env or docker-compose.override.yml
    

  

🧠 _Q_: How do you bring up a Spring Boot app with PostgreSQL using Docker Compose?

---

### **🔹 6.** 

### **Docker Networking**

- Default bridge network vs custom user-defined network
    
- container_name hostname resolution in Compose
    
- Exposing services to host vs other containers
    
- Isolating environments (dev, test, prod)
    

  

🧠 _Q_: How do two containers communicate without exposing ports to host?

---

### **🔹 7.** 

### **Docker Images: Tagging, Pushing & Pulling**

- Tagging with :latest, :v1.0, git SHA
    
- Pushing to DockerHub / GitHub Container Registry / ECR
    
- docker push, docker pull
    
- Image layering and digest SHA
    

  

🧠 _Q_: What happens when you rebuild the same Dockerfile with no changes?

---

### **🔹 8.** 

### **Docker in CI/CD**

- Using Docker in Jenkins/GitHub Actions
    
- Building + pushing images in pipelines
    
- Replacing Dockerized services using versioned images
    
- Docker login and secrets management
    

  

🧠 _Q_: How do you avoid exposing credentials in Docker build or push steps?

---

### **🔹 9.** 

### **Security, Optimization & Best Practices**

- Don’t run containers as root
    
- Use alpine or distroless images for minimal attack surface
    
- Keep images small (multi-stage builds)
    
- Use .dockerignore to reduce image size
    
- Regularly scan images (e.g., Trivy, Snyk)
    

  

🧠 _Q_: How can you secure a Docker image for production use?

---

### **🔹 10.** 

### **Docker vs Virtual Machine**

|**Feature**|**Docker**|**Virtual Machine**|
|---|---|---|
|Boot time|Seconds|Minutes|
|Resource usage|Lightweight|Heavy|
|Isolation|Process-level|Full OS-level|
|Portability|High|Medium|
|Use-case|Microservices, Dev/Test|OS-specific apps, legacy|

🧠 _Q_: Why are containers preferred for microservices?

---

### **🔹 11.** 

### **Common Use Cases**

- Containerize a Spring Boot application
    
- Run a local Redis or Kafka container for testing
    
- Override properties via environment variables
    
- Bind application.yml or secrets into container
    
- Log rotation and volume-based logging
    

---

Would you like a **sample Dockerfile + docker-compose.yml** for a Spring Boot app, or want this in a **progress checklist format** to track your mastery?