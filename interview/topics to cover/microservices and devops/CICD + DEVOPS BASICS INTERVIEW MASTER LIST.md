
You’re on 🔥 — and here’s the **final boss-level CI/CD + DevOps Interview Checklist** for Java/Spring Boot backend roles. This list ensures **you don’t miss a single thing** commonly asked in interviews, whether you’re deploying microservices or setting up pipelines in GitHub Actions or Jenkins.

---

## **✅ CI/CD + DEVOPS BASICS INTERVIEW MASTER LIST**

  

_Focused on backend engineers using Maven, Spring Boot, Docker, and Git-based pipelines_

---

### **🔹 1.** 

### **CI/CD Fundamentals**

- What is CI (Continuous Integration)?
    
- What is CD (Continuous Delivery vs Deployment)?
    
- Benefits of CI/CD (automation, faster feedback, reduced human error)
    
- CI/CD pipeline stages:
    
    - Build
        
    - Test
        
    - Lint/Check
        
    - Package
        
    - Deploy
        
    
- Common tools: **Jenkins**, **GitHub Actions**, **GitLab CI**, **CircleCI**, **Bitbucket Pipelines**
    

  

🧠 _Q_: What’s the difference between Continuous Deployment and Continuous Delivery?

---

### **🔹 2.** 

### **Build Tools & Lifecycle**

  

#### **🛠 Maven:**

- Maven lifecycle phases:
    
    - validate, compile, test, package, verify, install, deploy
        
    
- pom.xml structure: dependencies, plugins, profiles
    
- Running goals: mvn clean install, mvn test, mvn verify
    

  

#### **🛠 Gradle:**

- Task-based vs lifecycle-based
    
- build.gradle structure
    
- Common commands: ./gradlew build, test, clean
    

  

🧠 _Q_: What’s the difference between install and deploy in Maven?

---

### **🔹 3.** 

### **CI Pipeline Design (General Concepts)**

- Triggering pipelines:
    
    - Push, PR, merge, tag
        
    
- Workflow YAML structure (GitHub Actions, GitLab CI)
    
- Running tests:
    
    - mvn test
        
    - Capturing code coverage (JaCoCo)
        
    
- Artifacts:
    
    - Saving .jar or .war for deployments
        
    
- Caching dependencies (Maven/Gradle caches)
    

  

🧠 _Q_: How do you prevent downloading dependencies every pipeline run?

---

### **🔹 4.** 

### **Code Quality & Analysis Tools**

- **Checkstyle**: Java code style checker
    
- **PMD**: Finds programming flaws
    
- **SpotBugs**: Static analysis for bug patterns
    
- **SonarQube**:
    
    - Code smells, bugs, duplications, coverage
        
    - sonar-project.properties
        
    - Integrating with Jenkins/GitHub Actions
        
    
- Coverage tools: **JaCoCo**, **Cobertura**
    

  

🧠 _Q_: How do you fail a build if coverage is too low?

---

### **🔹 5.** 

### **Docker + CI/CD Integration**

- Writing Dockerfiles for Spring Boot:
    
    - Multi-stage builds (builder + runtime)
        
    - EXPOSE, CMD, ENTRYPOINT
        
    
- Building Docker image in CI:
    
    - docker build -t myapp .
        
    
- Docker image naming and tagging (latest, v1.0.0, git SHA)
    
- Pushing to registries:
    
    - DockerHub
        
    - GitHub Container Registry
        
    - AWS ECR, GCP GAR
        
    
- Using secrets for registry auth in pipeline
    

  

🧠 _Q_: What’s the difference between CMD and ENTRYPOINT in Docker?

---

### **🔹 6.** 

### **Jenkins-Specific Concepts**

- Jenkins pipeline types:
    
    - Freestyle job vs Pipeline (declarative vs scripted)
        
    
- Jenkinsfile stages:
    
    - stage('Build'), stage('Test'), stage('Deploy')
        
    
- Jenkins plugins: Git, Docker, SonarQube
    
- Running builds on agents
    
- Polling SCM vs Webhooks
    

  

🧠 _Q_: How do you securely inject secrets into a Jenkins pipeline?

---

### **🔹 7.** 

### **GitHub Actions Basics**

- .github/workflows/*.yml file
    
- Jobs, steps, runners
    
- Reusing workflows with workflow_call
    
- Secrets in GitHub Actions (${{ secrets.MY_SECRET }})
    
- Marketplace actions: setup-java, docker-build-push, sonarcloud
    

  

🧠 _Q_: How do you run tests only when certain files or folders change?

---

### **🔹 8.** 

### **Deployments & Environments**

- Environments: dev, staging, prod
    
- Environment variables per stage
    
- Canary deployments (optional)
    
- Rolling deployments vs Blue/Green
    
- Feature flags (LaunchDarkly, Unleash)
    

  

🧠 _Q_: How do you promote a build to production only after approval?

---

### **🔹 9.** 

### **Monitoring, Alerts, and Rollbacks**

- Adding Slack/email notifications to pipeline
    
- Health check endpoint monitoring
    
- Auto rollback strategy (basic)
    
- Keeping rollbackable Docker images or previous builds
    

  

🧠 _Q_: What happens if a production deployment fails?

---

Would you like to practice with a **GitHub Actions YAML** or **Jenkinsfile** sample for your Spring Boot app? Or want a **progress tracker table** to mark your completion of these topics?