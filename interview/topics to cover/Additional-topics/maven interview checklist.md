You got it, Akshita — here’s your **Blame-Proof Apache Maven Interview Checklist** ✅

Designed for **Java/Spring Boot backend interviews**, this covers **everything** from lifecycle phases and dependencies to multi-module projects, plugins, and profiles — no fluff, no gaps.

---

## **✅ MAVEN INTERVIEW MASTER LIST**

  

_For Java devs using Spring Boot, REST APIs, and CI/CD pipelines_

---

### **🔹 1.** 

### **What is Maven? Why use it?**

- Build automation tool for Java
    
- Manages project structure, dependencies, plugins, and lifecycle
    
- Compared to Gradle and Ant
    
- Convention over configuration principle
    
- XML-based configuration (pom.xml)
    

  

🧠 _Q_: What’s the main difference between Maven and Gradle?

---

### **🔹 2.** 

### **Maven Project Structure**

- Standard directory layout:
    

```
src/
  main/java
  main/resources
  test/java
  test/resources
target/
```

-   
    
- pom.xml sections:
    
    - <groupId>, <artifactId>, <version>
        
    - <dependencies>, <plugins>, <build>, <profiles>
        
    

  

🧠 _Q_: Where would you define a build plugin or resource filter?

---

### **🔹 3.** 

### **Maven Lifecycle Phases**

- **Three core lifecycles**:
    
    - _default_ (build): validate → compile → test → package → verify → install → deploy
        
    - _clean_: pre-clean → clean → post-clean
        
    - _site_: site, site-deploy
        
    
- Frequently used phases:
    
    - mvn clean install
        
    - mvn package
        
    - mvn test
        
    - mvn deploy (for CI/CD)
        
    

  

🧠 _Q_: What happens during mvn install?

---

### **🔹 4.** 

### **Maven Coordinates & Repositories**

- Maven coordinates: groupId + artifactId + version (GAV)
    
- Types of repositories:
    
    - Local (~/.m2/repository)
        
    - Central (Maven Central)
        
    - Remote/Private Nexus or Artifactory
        
    
- Repository order and lookup strategy
    

  

🧠 _Q_: What happens if a dependency is not found in any repository?

---

### **🔹 5.** 

### **Dependencies Management**

- Declaring dependencies
    
- Scopes:
    
    - compile, provided, runtime, test, system, import
        
    
- Transitive dependencies
    
- Dependency conflict resolution (nearest-wins strategy)
    
- exclusions tag
    
- Optional dependencies
    

  

🧠 _Q_: What’s the difference between provided and runtime scope?

---

### **🔹 6.** 

### **Plugins & Build Customization**

- What are Maven plugins?
    
- Commonly used plugins:
    
    - maven-compiler-plugin (Java version)
        
    - maven-surefire-plugin (unit testing)
        
    - maven-failsafe-plugin (integration testing)
        
    - maven-jar-plugin, maven-war-plugin, maven-shade-plugin
        
    
- Executing plugins with mvn <plugin>:<goal>
    

  

🧠 _Q_: When would you use maven-shade-plugin over spring-boot-maven-plugin?

---

### **🔹 7.** 

### **Profiles & Environments**

- What are Maven profiles?
    
- Defining profiles for:
    
    - Different environments (dev, prod)
        
    - Custom properties or plugin configs
        
    
- Activate profiles:
    
    - Via CLI: -Pprod
        
    - Based on JDK or OS
        
    

  

🧠 _Q_: How do you pass different DB configs for dev vs prod?

---

### **🔹 8.** 

### **Multi-Module Projects**

- Parent <modules> section
    
- Inheritance of dependencies and plugins
    
- Version management with <dependencyManagement>
    
- Aggregator vs Inherited POM
    
- Building all modules together: mvn clean install
    

  

🧠 _Q_: What’s the use of dependencyManagement in a parent POM?

---

### **🔹 9.** 

### **Effective POM & Debugging**

- Viewing effective POM: mvn help:effective-pom
    
- Dependency tree: mvn dependency:tree
    
- Forcing updates: mvn clean install -U
    
- Skipping tests: mvn install -DskipTests
    

  

🧠 _Q_: How do you resolve a version conflict in transitive dependencies?

---

### **🔹 10.** 

### **Integration with Tools**

- Maven + IDEs (IntelliJ, Eclipse): auto-import POM
    
- Maven + Jenkins: pipeline steps with Maven goals
    
- Maven + Docker (dockerfile-maven-plugin, Jib)
    
- Maven + SonarQube (static analysis plugin)
    

  

🧠 _Q_: How do you build and push a Docker image from a Maven build?

---

### **🔹 11.** 

### **Best Practices**

- Pin dependency versions (no floating versions)
    
- Separate test-only dependencies
    
- Lock Java version via compiler plugin
    
- Use BOMs for dependency consistency (e.g., Spring Boot BOM)
    
- Use dependencyManagement over duplicate <dependencies>
    

  

🧠 _Q_: How do you ensure consistent versions for Spring dependencies across modules?

---

Would you like this checklist exported or want to walk through a **sample POM for a Spring Boot + multi-module + profile-aware Maven project**?