
![[Screenshot 2025-06-25 at 2.31.04 PM.png]]![[Screenshot 2025-06-25 at 2.31.55 PM.png]]
![[Screenshot 2025-06-25 at 2.32.35 PM.png]]

# Configuration Classes

Spring Boot favors Java-based configuration. Although it is possible to use [`SpringApplication`](https://docs.spring.io/spring-boot/3.5.3/api/java/org/springframework/boot/SpringApplication.html) with XML sources, we generally recommend that your primary source be a single [`@Configuration`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/context/annotation/Configuration.html) class. Usually the class that defines the `main` method is a good candidate as the primary [`@Configuration`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/context/annotation/Configuration.html).

|     |                                                                                                                                                                                                                                              |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|     | Many Spring configuration examples have been published on the Internet that use XML configuration. If possible, always try to use the equivalent Java-based configuration. Searching for `Enable*` annotations can be a good starting point. |

## [](https://docs.spring.io/spring-boot/reference/using/configuration-classes.html#using.configuration-classes.importing-additional-configuration)Importing Additional Configuration Classes

You need not put all your [`@Configuration`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/context/annotation/Configuration.html) into a single class. The [`@Import`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/context/annotation/Import.html) annotation can be used to import additional configuration classes. Alternatively, you can use [`@ComponentScan`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/context/annotation/ComponentScan.html) to automatically pick up all Spring components, including [`@Configuration`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/context/annotation/Configuration.html) classes.

## [](https://docs.spring.io/spring-boot/reference/using/configuration-classes.html#using.configuration-classes.importing-xml-configuration)Importing XML Configuration

If you absolutely must use XML based configuration, we recommend that you still start with a [`@Configuration`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/context/annotation/Configuration.html) class. You can then use an [`@ImportResource`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/context/annotation/ImportResource.html) annotation to load XML configuration files.
@SpringbootApllication annotation -> 
consists of 3 annotations behind the scenes 

1. @ComponentScan
2. @EnableAutoConfiguration
3. @SpringBootConfiguration


# **1. @SpringBootApplication**


This is the **main annotation** that bootstraps your Spring Boot application.
### **✅ What it does:**

It is a **meta-annotation**, which combines:

```
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan
public @interface SpringBootApplication {
}
```

### **✅ Meaning of each:**

|**Annotation**|**Purpose**|
|---|---|
|@SpringBootConfiguration|A specialized version of @Configuration. It marks the class as a source of bean definitions|
|@EnableAutoConfiguration|Enables Spring Boot’s **auto-configuration mechanism** based on classpath scanning|
|@ComponentScan|Tells Spring to scan the **current package and subpackages** for Spring components (@Component, @Service, @Repository, @Controller, etc.)|

### **✅ Typical usage:**

```
@SpringBootApplication
public class MyApp {
    public static void main(String[] args) {
        SpringApplication.run(MyApp.class, args);
    }
}
```

---

# **✅** 

# **2. @Component, @Service, @Repository, @Controller, @RestController**

  

All of these are **stereotype annotations** — used to tell Spring that a class is a **Spring-managed bean**, and to **autowire** it wherever needed.

| **Annotation**  | **Layer**            | **Purpose**                                                                                                          |
| --------------- | -------------------- | -------------------------------------------------------------------------------------------------------------------- |
| @Component      | Generic              | Marks any class as a Spring bean                                                                                     |
| @Service        | Business logic layer | Specialized version of @Component — indicates service logic                                                          |
| @Repository     | Data access layer    | Specialized version of @Component, adds **persistence exception translation**                                        |
| @Controller     | Web layer (MVC)      | Used to define a controller class that handles HTTP requests using ModelAndView (view templates like JSP, Thymeleaf) |
| @RestController | Web layer (REST API) | Combines @Controller and @ResponseBody — JSON or XML response                                                        |

---

# **✅** 

# **3. @Autowired**

  

### **Purpose:**

  

Used for **dependency injection**. Spring injects the required bean **automatically** into this field, constructor, or setter.

  

### **Example:**

```
@Service
public class UserService {
    @Autowired
    private UserRepository userRepository;
}
```

> 🔍 Behind the scenes, Spring uses reflection + BeanFactory to inject dependencies.

---

# **✅** 

# **4. @Configuration**

  

### **Purpose:**

  

Marks a class as a **source of bean definitions** using the @Bean annotation inside it.

  

### **Example:**

```
@Configuration
public class AppConfig {
    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
}
```

> ✅ Beans created here are part of the Spring ApplicationContext.

---

# **✅** 

# **5. @Bean**

  

### **Purpose:**

  

Defines a **method-level bean** in a @Configuration class. The return value of the method becomes a Spring-managed bean.

---

# **✅** 

# **6. @Value, @ConfigurationProperties**

  

### **@Value**

  

Injects values from **application.properties** or **environment variables**.

```
@Value("${app.name}")
private String appName;
```

### **@ConfigurationProperties**

  

Binds a **whole group** of properties into a POJO.

```
@ConfigurationProperties(prefix = "app")
public class AppConfig {
    private String name;
    private int timeout;
    // getters/setters
}
```

---

# **✅** 

# **7. @EnableAutoConfiguration**

  

This is the **heart of Spring Boot’s magic**.

  

### **Purpose:**

  

Scans the classpath for libraries (e.g., H2, Tomcat, Spring Data JPA) and **automatically configures** beans based on spring.factories.

  

> 🔥 When you add spring-boot-starter-web, it auto-configures:

- > DispatcherServlet
    
- > Tomcat
    
- > Jackson
    
- > MessageConverters
    
- > And more…
    


## Disabling Specific Auto-configuration Classes

If you find that specific auto-configuration classes that you do not want are being applied, you can use the exclude attribute of [`@SpringBootApplication`](https://docs.spring.io/spring-boot/3.5.3/api/java/org/springframework/boot/autoconfigure/SpringBootApplication.html) to disable them, as shown in the following example:

- Java
    
- Kotlin
    

```java
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration;

@SpringBootApplication(exclude = { DataSourceAutoConfiguration.class })
public class MyApplication {

}
```

If the class is not on the classpath, you can use the `excludeName` attribute of the annotation and specify the fully qualified name instead. If you prefer to use [`@EnableAutoConfiguration`](https://docs.spring.io/spring-boot/3.5.3/api/java/org/springframework/boot/autoconfigure/EnableAutoConfiguration.html) rather than [`@SpringBootApplication`](https://docs.spring.io/spring-boot/3.5.3/api/java/org/springframework/boot/autoconfigure/SpringBootApplication.html), `exclude` and `excludeName` are also available. Finally, you can also control the list of auto-configuration classes to exclude by using the `spring.autoconfigure.exclude` property.



## Auto-configuration Packages

Auto-configuration packages are the packages that various auto-configured features look in by default when scanning for things such as entities and Spring Data repositories. The [`@EnableAutoConfiguration`](https://docs.spring.io/spring-boot/3.5.3/api/java/org/springframework/boot/autoconfigure/EnableAutoConfiguration.html) annotation (either directly or through its presence on [`@SpringBootApplication`](https://docs.spring.io/spring-boot/3.5.3/api/java/org/springframework/boot/autoconfigure/SpringBootApplication.html)) determines the default auto-configuration package. Additional packages can be configured using the [`@AutoConfigurationPackage`](https://docs.spring.io/spring-boot/3.5.3/api/java/org/springframework/boot/autoconfigure/AutoConfigurationPackage.html) annotation.

---

# **✅** 

# **8. @RequestMapping, @GetMapping, @PostMapping, etc.**

  

Used in controllers to map HTTP routes:

|**Annotation**|**Purpose**|
|---|---|
|@RequestMapping|Generic, supports all HTTP methods|
|@GetMapping|Maps HTTP GET|
|@PostMapping|Maps HTTP POST|
|@PutMapping|Maps HTTP PUT|
|@DeleteMapping|Maps HTTP DELETE|

```
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public User getUser(@PathVariable Long id) { ... }

    @PostMapping
    public User saveUser(@RequestBody User user) { ... }
}
```

---

# **✅** 

# **9. @PathVariable, @RequestParam, @RequestBody, @ResponseBody**

|**Annotation**|**Purpose**|
|---|---|
|@PathVariable|Extracts variable from URL path|
|@RequestParam|Extracts query param|
|@RequestBody|Converts JSON body to Java object|
|@ResponseBody|Converts Java object to JSON body (used with @Controller)|

---

# **✅** 

# **10. @Entity, @Table, @Id, @GeneratedValue, etc. (JPA Annotations)**

|**Annotation**|**Purpose**|
|---|---|
|@Entity|Marks a class as a JPA entity|
|@Table|Maps the class to a specific DB table|
|@Id|Declares the primary key|
|@GeneratedValue|Auto-generates primary key values|
|@Column|Specifies column properties (name, nullable, etc.)|

```
@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false)
    private String username;
}
```

---

# **✅** 

# **11. @Transactional**

  

Manages database transactions.

```
@Transactional
public void updateAccount() {
    // If any exception occurs, this method will rollback.
}
```

- Can be used at class or method level.
    
- Integrates with Spring AOP behind the scenes.
    

---

# **✅** 

# **12. @Enable* Annotations**

  

These are **feature enablers** in Spring Boot:

|**Annotation**|**Enables**|
|---|---|
|@EnableScheduling|Enables scheduling (cron jobs, etc.)|
|@EnableCaching|Enables Spring’s caching abstraction|
|@EnableJpaRepositories|Enables Spring Data JPA repository scanning|
|@EnableWebSecurity|Enables Spring Security|
|@EnableConfigurationProperties|Enables binding to POJOs using @ConfigurationProperties|

---

# **✅ Summary Table**

|**Annotation**|**Layer**|**Description**|
|---|---|---|
|@SpringBootApplication|App Bootstrapping|Main entrypoint with auto-config + scanning|
|@Component, @Service, etc.|Core|Mark beans for DI|
|@Autowired|Core|Inject dependencies|
|@Configuration, @Bean|Config|Define beans manually|
|@Value, @ConfigurationProperties|Config|Read from properties|
|@RestController, @GetMapping, etc.|Web|HTTP request handlers|
|@Transactional|Data|Transaction boundary|
|@Entity, @Repository|JPA|ORM mappings|
|@Enable*|Feature toggle|Enable scheduling, caching, etc.|

---

Would you like me to:

  

✅ Generate a **cheat sheet diagram** for all of these annotations for quick memorization?

✅ Explain how Spring handles annotations behind the scenes using proxies and reflection?

✅ Or go deeper into **custom annotations** in Spring?

  

Let me know what you’d like to tackle next!


\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\

# Spring Beans and Dependency Injection

You are free to use any of the standard Spring Framework techniques to define your beans and their injected dependencies. We generally recommend using constructor injection to wire up dependencies and [`@ComponentScan`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/context/annotation/ComponentScan.html) to find beans.

If you structure your code as suggested above (locating your application class in a top package), you can add [`@ComponentScan`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/context/annotation/ComponentScan.html) without any arguments or use the [`@SpringBootApplication`](https://docs.spring.io/spring-boot/3.5.3/api/java/org/springframework/boot/autoconfigure/SpringBootApplication.html) annotation which implicitly includes it. All of your application components ([`@Component`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/stereotype/Component.html), [`@Service`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/stereotype/Service.html), [`@Repository`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/stereotype/Repository.html), [`@Controller`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/stereotype/Controller.html), and others) are automatically registered as Spring Beans.

The following example shows a [`@Service`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/stereotype/Service.html) Bean that uses constructor injection to obtain a required `RiskAssessor` bean:


If a bean has more than one constructor, you will need to mark the one you want Spring to use with [`@Autowired`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/beans/factory/annotation/Autowired.html):

```java
import java.io.PrintStream;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class MyAccountService implements AccountService {

	private final RiskAssessor riskAssessor;

	private final PrintStream out;

	@Autowired
	public MyAccountService(RiskAssessor riskAssessor) {
		this.riskAssessor = riskAssessor;
		this.out = System.out;
	}

	public MyAccountService(RiskAssessor riskAssessor, PrintStream out) {
		this.riskAssessor = riskAssessor;
		this.out = out;
	}

	// ...

}
```

|   |   |
|---|---|
||Notice how using constructor injection lets the `riskAssessor` field be marked as `final`, indicating that it cannot be subsequently changed.|





Excellent — let’s now dive into **how Spring Boot’s Auto-Configuration works behind the scenes**, including:

- The **auto-configuration mechanism**
    
- The role of @Conditional, @ConditionalOnXxx
    
- The spring.factories / spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports
    
- EnvironmentPostProcessor
    
- Smart enabling/disabling based on classpath, beans, properties, etc.
    

---

## **🌟 What Is Auto-Configuration?**

  

Auto-configuration is Spring Boot’s magic that **automatically configures beans** based on:

  

✅ Classpath dependencies

✅ Configuration properties

✅ Missing or existing beans

✅ Environment variables

  

This makes Spring Boot **opinionated** — it auto-configures sensible defaults unless you explicitly override them.

---

## **🔑 Step-by-Step: How Auto-Configuration Works Internally**

---

### **🔹 1.** 

### **@EnableAutoConfiguration**

###  **(part of** 

### **@SpringBootApplication**

### **)**

  

This annotation triggers **Spring Boot’s auto-configuration mechanism** using:

```
@AutoConfigurationPackage
@Import(AutoConfigurationImportSelector.class)
public @interface EnableAutoConfiguration {
}
```

#### **✅** 

#### **AutoConfigurationImportSelector**

#### **:**

- Scans META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports
    
- Earlier, it used spring.factories → now Spring Boot 3+ uses the AutoConfiguration.imports format.
    

```
# Located inside spring-boot-autoconfigure.jar
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
com.example.H2AutoConfiguration,\
com.example.WebMvcAutoConfiguration,...
```

---

### **🔹 2. Filtering AutoConfigs with** 

### **@Conditional**

###  **Annotations**

  

Each auto-configuration class is guarded by **@Conditional... annotations**, which determine **whether or not to apply** a specific configuration.

  

#### **🔍 Common** 

#### **@Conditional**

####  **Variants:**

|**Annotation**|**Condition Checked**|
|---|---|
|@ConditionalOnClass|Class is present on classpath|
|@ConditionalOnMissingBean|Bean is not already defined|
|@ConditionalOnBean|Bean is already defined|
|@ConditionalOnProperty|Property exists or has value|
|@ConditionalOnWebApplication|Only configure if web environment|
|@ConditionalOnExpression|SpEL condition evaluates to true|
|@ConditionalOnResource|Resource (e.g., file) exists|
|@ConditionalOnJava|Java version check|

#### **✅ Example:** 

#### **DataSourceAutoConfiguration**

```
@Configuration
@ConditionalOnClass({ DataSource.class })
@ConditionalOnProperty(prefix = "spring.datasource", name = "url")
@EnableConfigurationProperties(DataSourceProperties.class)
public class DataSourceAutoConfiguration {
    
    @Bean
    @ConditionalOnMissingBean
    public DataSource dataSource(DataSourceProperties props) {
        return new HikariDataSource(props);
    }
}
```

→ This configures a DataSource only if:

- DataSource.class is present on classpath
    
- Property spring.datasource.url is defined
    
- No other DataSource bean is defined
    

---

### **🔹 3.** 

### **EnvironmentPostProcessor**

  

Used to **hook into the environment before the context is refreshed** (even before @ConfigurationProperties are bound).

  

#### **✅ Use Cases:**

- Set default properties
    
- Customize profiles
    
- Externalize properties dynamically
    

  

#### **Example:**

```
public class MyEnvProcessor implements EnvironmentPostProcessor {
    @Override
    public void postProcessEnvironment(ConfigurableEnvironment env, SpringApplication app) {
        env.getPropertySources().addFirst(new MapPropertySource(
            "my-defaults", Map.of("app.name", "DefaultApp")));
    }
}
```

#### **Register in:**

```
META-INF/spring.factories
org.springframework.boot.env.EnvironmentPostProcessor=com.example.MyEnvProcessor
```

---

## **💡 How Does Spring Avoid Conflicts?**

- By using @ConditionalOnMissingBean, Spring ensures **you can override beans** easily.
    
- @Primary can be used when multiple candidates exist.
    
- Profiles and properties allow dynamic control (application-dev.yml, application-prod.yml).
    
- Beans are loaded lazily and only if their conditions pass.
    

---

## **📦 Summary: Auto-Config Internals Flow**

```
@SpringBootApplication →
@EnableAutoConfiguration →
@Import(AutoConfigurationImportSelector) →
Scan AutoConfiguration.imports →
Filter using @Conditional annotations →
Register matching @Bean definitions →
Load additional properties via EnvironmentPostProcessor
```

---

## **🧠 Bonus: What Happens When You Add a New Dependency?**

  

Example: You add spring-boot-starter-data-jpa.

- Spring Boot sees JPA and Hibernate on classpath (@ConditionalOnClass)
    
- It sees a DB URL (@ConditionalOnProperty)
    
- It registers:
    
    - EntityManagerFactory
        
    - JpaTransactionManager
        
    - Repositories
        
    

  

All without writing a single line of config code.

---

Great questions! Let’s break this down clearly and thoroughly.

---

## **🚀 What Are Spring Boot DevTools?**

  

**Spring Boot DevTools** is a **developer productivity** toolset provided by Spring Boot that enhances your development workflow.

  

It’s included by adding this dependency:

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <scope>runtime</scope> <!-- Automatically excluded from production builds -->
</dependency>
```

---

## **🎁 Features Provided by Spring Boot DevTools**

|**Feature**|**Description**|
|---|---|
|**Hot Reloading (Automatic Restart)**|Automatically restarts your Spring Boot app when classpath files change (e.g., editing .java, .class, or .properties)|
|**LiveReload**|Works with browsers like Chrome to automatically refresh the page when resources like HTML/CSS change|
|**Caching Disabled**|Disables template (Thymeleaf/Freemarker), static resource, and Groovy template caching for faster feedback|
|**Automatic Property Override**|DevTools loads application-dev.properties or application.properties in a dev-specific way|
|**Global Settings Support**|Reads settings from ~/.spring-boot-devtools.properties|
|**Remote Debugging (Optional)**|You can set up DevTools for debugging in remote environments (but not recommended for prod)|

---

## **🔥 What Is Hot Reloading?**

  

### **✅ Definition:**

  

**Hot Reloading (or Automatic Restart)** means **your application restarts automatically whenever files in the classpath change**, especially during development.

  

### **👩‍💻 Example:**

  

You change a controller or service class and save the file — Spring Boot DevTools automatically restarts the app with the new changes without you manually stopping and starting the server.

  

### **🧠 Behind the Scenes:**

- DevTools uses **two classloaders**:
    
    - One for the static classes (e.g., 3rd party libs)
        
    - One for your changing classes (your code)
        
    
- It restarts only the classloader holding your code to make the restart fast.
    

---

## **🔐 Why Disable DevTools in Production?**

  

### **✅ Reason 1:** 

### **Performance Overhead**

- DevTools keeps watching file changes and uses additional memory for dual classloaders.
    
- Unnecessary in production where code doesn’t change dynamically.
    

  

### **✅ Reason 2:** 

### **Security Risk**

- DevTools enables features like **remote debug tunnel**, **LiveReload**, and **weaker cache policies**, which can be **exploited** if exposed.
    

  

### **✅ Risky Scenarios:**

|**Risk**|**Explanation**|
|---|---|
|**LiveReload**|May reload browser content remotely or be used as an attack vector|
|**Open Debug Tunnel**|If misconfigured, attackers could use it to run remote code|
|**Relaxed Security**|DevTools disables some security configurations in dev mode|
|**Hot-reload agent misuse**|Could lead to unwanted application restarts if file watching is exploited|

---

## **🚫 How to Disable DevTools in Production?**

  

Spring Boot takes care of it automatically — **DevTools is not included in production build** because of its runtime scope.

  

But if you want to **explicitly disable it**, use one of the following:

  

### **✅ Option 1: Set the property**

```
-Dspring.devtools.restart.enabled=false
```

### **✅ Option 2: In** 

### **application.properties**

```
spring.devtools.restart.enabled=false
```

### **✅ Option 3: Exclude from production build (Maven/Gradle)**

  

Remove the dependency or set:

```
<scope>runtime</scope> <!-- ensures it's not in the final artifact -->
```

---

## **🧾 Summary**

|**Feature**|**DevTools Provides**|
|---|---|
|Automatic Restart|Hot reloading on classpath changes|
|LiveReload|Auto browser refresh|
|Dev Settings|Disables cache, simplifies debugging|
|Restart ClassLoader|Only reloads application code, not full app|

|**Topic**|**Reason**|
|---|---|
|Why disable in prod?|Performance, security, no file watching needed|
|Risk?|Dev tunnels, LiveReload, relaxed security|
|How to disable?|Remove dependency or set restart to false|



---

## **✅ GOAL: Understand What Happens When You Use** 

## **application.properties**

  

When you write something like:

```
server.port=9090
spring.datasource.url=jdbc:h2:mem:testdb
```

You want Spring Boot to:

- Pick up these values
    
- Use them to configure beans (like the embedded server or DataSource)
    
- Let you override them by profile or command-line
    

---

## **🧭 COMPLETE FLOW – STEP BY STEP (Simplified)**

---

### **🔹** 

### **STEP 1: App Starts**

```
SpringApplication.run(MyApp.class, args);
```

This bootstraps the Spring Boot application.

  

✅ Creates:

- SpringApplication instance
    
- Spring **ApplicationContext**
    
- **Environment** object
    

---

### **🔹** 

### **STEP 2: Spring Searches for Configuration Files**

  

Spring Boot looks for:

```
application.properties
application.yml
```

In locations like:

```
/config/
/resources/
/src/main/resources/
```

And loads both:

- **Default file** → application.properties
    
- **Profile-based file** → application-dev.properties if spring.profiles.active=dev
    

---

### **🔹** 

### **STEP 3: Config File is Loaded via ConfigDataEnvironmentPostProcessor**

  

This internal class is responsible for:

- Finding config files
    
- Loading properties
    
- Adding them to the **Environment**
    

  

📌 It’s triggered early during app startup, even before beans are created.

---

### **🔹** 

### **STEP 4: Properties Are Stored in the Environment**

  

Spring creates a layered structure called:

```
ConfigurableEnvironment
```

It holds multiple **PropertySources** like:

|**Priority**|**Source**|
|---|---|
|1️⃣|Command-line args|
|2️⃣|SPRING_APPLICATION_JSON|
|3️⃣|OS Environment variables|
|4️⃣|application.properties and application.yml|
|5️⃣|Profile-specific config|
|6️⃣|Default values from code|

So if you define the same property in multiple places, Spring will use the **highest-priority** value.

---

### **🔹** 

### **STEP 5: Spring Uses These Properties in Two Main Ways**

  

#### **🟩 (A)** 

#### **Binding values into your beans**

- ✅ @Value("${server.port}")
    
- ✅ @ConfigurationProperties(prefix = "spring.datasource")
    
- ✅ Environment.getProperty("some.key")
    

  

Spring uses its **Binder API** to convert and inject values into:

- int, String, List, Map, etc.
    

---

#### **🟩 (B)** 

#### **Driving Conditional Configuration**

  

Auto-configurations check these properties to decide **what to enable or skip**.

  

Example:

```
@ConditionalOnProperty(name = "spring.datasource.url")
```

Spring only creates a DataSource if this property exists.

---

### **🔹** 

### **STEP 6: AutoConfiguration Uses the Loaded Properties**

  

Auto-config classes like:

```
DataSourceAutoConfiguration
WebMvcAutoConfiguration
SecurityAutoConfiguration
```

Use:

- @ConditionalOnClass
    
- @ConditionalOnProperty
    
- @ConditionalOnMissingBean
    

  

To read Environment and decide:

  

> “Should I create this bean?”

---

## **🧾 VISUAL FLOW**

```
                ┌────────────────────────────┐
                │ SpringApplication.run()    │
                └────────────┬───────────────┘
                             ↓
            ┌────────────────────────────────────┐
            │ Load Config: application.properties│
            └────────────────────────────────────┘
                             ↓
        ┌───────────────────────────────────────────────┐
        │ ConfigDataEnvironmentPostProcessor loads files│
        └───────────────────────────────────────────────┘
                             ↓
           ┌────────────────────────────────────────┐
           │ Values added to Environment (in layers)│
           └────────────────────────────────────────┘
                             ↓
       ┌─────────────────────────────────────────────────┐
       │ Properties injected into beans or used in logic │
       └─────────────────────────────────────────────────┘
                             ↓
     ┌────────────────────────────────────────────────────────┐
     │ AutoConfiguration checks values to enable/disable beans│
     └────────────────────────────────────────────────────────┘
```

---

## **🧠 Summary Table**

|**Component**|**Role**|
|---|---|
|application.properties|Holds your app config|
|ConfigDataEnvironmentPostProcessor|Loads and parses the config|
|Environment|Stores all resolved config|
|@Value, @ConfigurationProperties|Inject values into beans|
|@ConditionalOnProperty, etc.|Enable/disable auto-configs|
|AutoConfiguration|Uses config to auto-wire beans|

---

## **💡 Tip to Remember It:**

Just say to yourself:

> “Spring Boot reads config → stores in Environment → injects into beans → uses for auto-config.”

  

## Lazy Initialization

[`SpringApplication`](https://docs.spring.io/spring-boot/3.5.3/api/java/org/springframework/boot/SpringApplication.html) allows an application to be initialized lazily. When lazy initialization is enabled, beans are created as they are needed rather than during application startup. As a result, enabling lazy initialization can reduce the time that it takes your application to start. In a web application, enabling lazy initialization will result in many web-related beans not being initialized until an HTTP request is received.

A downside of lazy initialization is that it can delay the discovery of a problem with the application. If a misconfigured bean is initialized lazily, a failure will no longer occur during startup and the problem will only become apparent when the bean is initialized. Care must also be taken to ensure that the JVM has sufficient memory to accommodate all of the application’s beans and not just those that are initialized during startup. For these reasons, lazy initialization is not enabled by default and it is recommended that fine-tuning of the JVM’s heap size is done before enabling lazy initialization.

Lazy initialization can be enabled programmatically using the `lazyInitialization` method on [`SpringApplicationBuilder`](https://docs.spring.io/spring-boot/3.5.3/api/java/org/springframework/boot/builder/SpringApplicationBuilder.html) or the `setLazyInitialization` method on [`SpringApplication`](https://docs.spring.io/spring-boot/3.5.3/api/java/org/springframework/boot/SpringApplication.html). Alternatively, it can be enabled using the `spring.main.lazy-initialization` property as shown in the following example:

- Properties
    
- YAML
    

```properties
spring.main.lazy-initialization=true
```

|     |                                                                                                                                                                                                                         |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|     | If you want to disable lazy initialization for certain beans while using lazy initialization for the rest of the application, you can explicitly set their lazy attribute to false using the `@Lazy(false)` annotation. |
![[Screenshot 2025-06-26 at 2.36.40 PM.png]]



## Exception Handling in Spring Boot 

---

## **✅ GOAL**

  

Handle exceptions in a way that:

- Provides meaningful error messages
    
- Maps to correct HTTP status codes
    
- Is reusable and centralized
    
- Logs technical errors (but hides them from clients)
    
- Returns structured JSON in REST APIs
    

---

## **🧭 ALL WAYS TO HANDLE EXCEPTIONS IN SPRING BOOT**

---

### **🔹 1.** 

### **Try-Catch Block (Local Handling)**

  

#### **✅ Usage:**

  

Inside a method, usually for handling very specific exceptions.

```
@GetMapping("/user/{id}")
public ResponseEntity<?> getUser(@PathVariable int id) {
    try {
        return ResponseEntity.ok(userService.getById(id));
    } catch (UserNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(ex.getMessage());
    }
}
```

#### **❌ Not scalable — only good for one-off cases.**

---

### **🔹 2.** 

### **Using @ExceptionHandler (Per-Controller or Shared)**

  

#### **✅ Usage:**

  

Use this inside a controller class or a shared base controller.

```
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<?> handleUserNotFound(UserNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND)
                .body(Map.of("error", ex.getMessage()));
    }
}
```

#### **✅ Advantages:**

- Clean
    
- Reusable across multiple controllers
    
- Easy to test
    

---

### **🔹 3.** 

### **Using @ControllerAdvice (Global Exception Handler)**

  

@ControllerAdvice = Global error interceptor for all controllers.

```
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleGeneric(Exception ex) {
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR)
                .body(new ErrorResponse("Something went wrong", ex.getMessage()));
    }

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<?> handleValidation(MethodArgumentNotValidException ex) {
        var errors = ex.getBindingResult().getFieldErrors()
            .stream().collect(Collectors.toMap(FieldError::getField, FieldError::getDefaultMessage));
        return ResponseEntity.badRequest().body(errors);
    }
}
```

---

### **🔹 4.** 

### **Using ResponseStatusException (Quick and declarative)**

  

#### **✅ Usage:**

  

Throw this manually when you want to return an HTTP error with status and reason.

```
@GetMapping("/user/{id}")
public User getUser(@PathVariable int id) {
    return userRepo.findById(id)
        .orElseThrow(() -> new ResponseStatusException(
            HttpStatus.NOT_FOUND, "User not found"));
}
```

---

### **🔹 5.** 

### **Custom Exception + @ResponseStatus**

  

#### **✅ Define a custom exception with status code directly:**

```
@ResponseStatus(HttpStatus.NOT_FOUND)
public class UserNotFoundException extends RuntimeException {
    public UserNotFoundException(String message) {
        super(message);
    }
}
```

No need for controller advice if all you want is status code and message.

---

### **🔹 6.** 

### **Custom Exception Class + Global Handler**

  

This is best for real-world APIs. Example:

```
public class ApiError {
    private String message;
    private String details;
    private int status;
}
```

Then in your global handler:

```
@ExceptionHandler(CustomAppException.class)
public ResponseEntity<ApiError> handleAppException(CustomAppException ex) {
    ApiError error = new ApiError(ex.getMessage(), "Custom error", 400);
    return ResponseEntity.status(HttpStatus.BAD_REQUEST).body(error);
}
```

---

### **🔹 7.** 

### **Validation Exception Handling (@Valid, @Validated)**

  

When using:

```
@PostMapping("/user")
public ResponseEntity<?> create(@Valid @RequestBody User user) { ... }
```

If validation fails, Spring throws:

- MethodArgumentNotValidException for @Valid
    
- ConstraintViolationException for @Validated
    

  

Handle it like this:

```
@ExceptionHandler(MethodArgumentNotValidException.class)
public ResponseEntity<?> handleValidationErrors(MethodArgumentNotValidException ex) {
    Map<String, String> errors = new HashMap<>();
    ex.getBindingResult().getFieldErrors().forEach(error ->
        errors.put(error.getField(), error.getDefaultMessage()));
    return ResponseEntity.badRequest().body(errors);
}
```

---

### **🔹 8.** 

### **Customizing Spring Boot Error Response (Advanced)**

  

Override the default /error behavior using ErrorController:

```
@RestController
public class CustomErrorController implements ErrorController {

    @RequestMapping("/error")
    public ResponseEntity<?> handleError(HttpServletRequest request) {
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR)
            .body("Custom error page");
    }
}
```

But this is rarely used in REST APIs — better to stick with @ControllerAdvice.

---

## **🧾 Summary Table**

|**Method**|**Scope**|**Use Case**|
|---|---|---|
|Try-Catch|Local|One-off exception|
|@ExceptionHandler|Per-controller or shared|Controller-level logic|
|@ControllerAdvice|Global|Clean, reusable global handler|
|ResponseStatusException|Inline|Simple error throw with status|
|@ResponseStatus|Annotation-based|Declarative exception mapping|
|Validation exceptions|Global|Handle @Valid errors|
|ErrorController|Advanced|Custom default error page/logic|

---

## **💡 Best Practices**

- Use **@ControllerAdvice + custom exceptions** for large projects.
    
- Return **structured error responses** (e.g., JSON with message, timestamp, status).
    
- Log **full stack traces**, but don’t expose them to clients.
    
- Always handle **validation errors** and provide field-level feedback.
    

---
