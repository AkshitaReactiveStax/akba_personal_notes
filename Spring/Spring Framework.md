
The Spring Framework is a powerful and versatile framework for building Java applications, offering solutions for enterprise-level development. It simplifies the development process by providing tools to manage application components (beans) and their dependencies, which is called Dependency Injection (DI). Spring also enables seamless integration with databases, web services, and messaging systems, making it easier to create robust and scalable applications. With built-in modules for web development (Spring MVC), data access (Spring Data), and security (Spring Security), it eliminates boilerplate code and provides flexibility. Beginners find it helpful as it standardizes development practices and reduces complexity, enabling a more modular and maintainable codebase.


### What is DEPENDANCY INJECTION?

Dependency Injection (DI) is a design principle in software development where an object’s dependencies (other objects it needs to function) are provided to it from an external source rather than the object creating them itself. This makes the code more modular, testable, and flexible.

  

In simpler terms:

• **Without DI**: Each object creates and manages its own dependencies, leading to tight coupling between objects.

• **With DI**: Dependencies are injected into an object by an external framework or configuration, decoupling the object from the creation of its dependencies.

  

For example:

Suppose you have a Car class that needs an Engine to run:


```
class Car {

    private Engine engine;

  

    public Car() {

        this.engine = new Engine(); _// Car is tightly coupled to Engine

    }

}

```
  

With Dependency Injection:

  
```

class Car {

    private Engine engine;

  

    public Car(Engine engine) { // Engine is injected into Car_

        this.engine = engine;

    }

}
```

  

Here, an external framework like Spring would create and inject the Engine into the Car, allowing you to easily swap out the Engine implementation or unit-test the Car class with a mock Engine. This promotes loose coupling and better maintainability.


### What is the use of IOC Container ?

An **IOC (Inversion of Control) container** is a core concept in frameworks like Spring that manages the lifecycle, configuration, and dependencies of objects (beans) in an application. The container inverts the control of object creation and dependency management from the developer to the framework. Here’s what it offers and why it’s useful:

  

**Key Uses of the IOC Container:**

1. **Dependency Injection (DI):**

The IOC container is responsible for injecting dependencies into beans, eliminating the need for manual wiring of objects. This makes the code loosely coupled and easier to maintain.

2. **Bean Lifecycle Management:**

The container creates, initializes, and manages the lifecycle of beans. It ensures that beans are properly set up before being used and cleaned up when no longer needed.

3. **Centralized Configuration:**

The IOC container allows you to define bean configurations in one place (e.g., XML, annotations, or Java configuration), making the application structure more organized.

4. **Scalability:**

It supports advanced features like scopes (singleton, prototype, etc.) and lazy initialization, enabling applications to scale efficiently.

5. **Integration:**

The container seamlessly integrates with other parts of the Spring ecosystem, like Spring MVC, Spring Data, and Spring Security, to provide a cohesive development experience.

  

**How It Works:**

• The container reads configuration metadata (e.g., XML, annotations, or Java classes).

• It scans and identifies beans to manage.

• It wires dependencies and ensures beans are ready for use.

• It provides beans to the application as needed.

  

**Example:**

  

Suppose you have a Car class that depends on an Engine class. You can use the Spring IOC container to manage these:

  

**Configuration (Annotation-Based):**

  
```

@Component
class Engine {

    _// Engine implementation_

}

  

@Component
class Car {

    private final Engine engine;

  

    @Autowired

    public Car(Engine engine) {

        this.engine = engine;

    }

}

```
  



**Spring Boot Application:**
  
```

@SpringBootApplication

public class Application {

    public static void main(String[] args) {

        ApplicationContext context = SpringApplication.run(Application.class, args);

        Car car = context.getBean(Car.class); _// Get the Car bean from the container_

    }

}

  
```

The IOC container automatically manages the creation and wiring of the Engine and Car objects, reducing boilerplate code and improving flexibility.


### what is ApplicationContext?

Yes, ApplicationContext is one of the core implementations of the **IOC container** in the Spring Framework. It provides an advanced and feature-rich way to manage the lifecycle of beans and their dependencies in a Spring application.

**Relation Between ApplicationContext and the IOC Container**

• The **IOC container** is a concept in Spring for managing object creation and dependency injection.

• ApplicationContext is an implementation of the IOC container. It extends another basic IOC container interface in Spring called BeanFactory, providing additional enterprise-level features.

  

**What is ApplicationContext?**

ApplicationContext is a central interface in Spring that:

1. **Manages Beans:** It creates, wires, and manages beans defined in your Spring configuration.

2. **Provides Additional Features:**

• **Internationalization (i18n):** Support for message localization.

• **Event Propagation:** Ability to publish and listen to application events.

• **Integration with AOP:** Seamless integration with Spring’s Aspect-Oriented Programming (AOP) features.

• **Resource Management:** Access to various file and classpath resources.

  

**Key Responsibilities of ApplicationContext**

1. **Bean Lookup:**

Allows retrieving beans by their name or type:

```
  
ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);

MyBean bean = context.getBean(MyBean.class);

```
  

  

2. **Bean Lifecycle Management:**

Ensures beans are initialized, dependencies are injected, and they are destroyed properly.

3. **Event Handling:**

Publishes application events that listeners can react to, like context refresh or custom events.

4. **Message Resolution:**

Helps resolve messages for internationalization using a MessageSource.

5. **Autowiring and Dependency Injection:**

Manages dependency injection between beans defined in the context.

  

**Common Implementations of ApplicationContext**

1. ClassPathXmlApplicationContext**:**

Loads bean definitions from an XML file in the classpath.

2. FileSystemXmlApplicationContext**:**

Loads bean definitions from an XML file in the file system.

3. AnnotationConfigApplicationContext**:**

Loads bean definitions using Java-based annotations.

4. WebApplicationContext**:**

A specialized version for web applications, often used with Spring MVC.

  

**Example**

Suppose you have a configuration class like this:

```
  

@Configuration

@ComponentScan("com.example")

public class AppConfig {}

  
```

You can initialize the ApplicationContext as follows:

  
```

public static void main(String[] args) {

    ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);

    MyService myService = context.getBean(MyService.class);

    myService.performAction();

}

```
  

Here, ApplicationContext serves as the IOC container by managing the lifecycle and dependencies of beans defined in AppConfig.

  

In summary, ApplicationContext **is indeed an implementation of the IOC container** in Spring, offering more advanced features compared to the simpler BeanFactory.

### Types of Dependancy Injection?

In Spring, there are **three main types of Dependency Injection (DI)**, based on how dependencies are provided to an object:

  

**1. Constructor Injection**

• Dependencies are provided through the class constructor.

• Ensures that an object is created with all its required dependencies.

• Promotes immutability by making dependencies final.

  

**Example:**

  
```

@Component

class Car {

    private final Engine engine;

  

    @Autowired

    public Car(Engine engine) { _// Dependency is injected through the constructor_

        this.engine = engine;

    }

}

```
  

**Advantages:**

• Mandatory dependencies are enforced at object creation time.

• Ideal for dependencies that are required for the object’s proper functioning.

  

**2. Setter Injection**

• Dependencies are injected via public setter methods after the object is constructed.

• Useful for optional dependencies or when you want to reconfigure dependencies after object creation.

  

**Example:**

```
  

@Component

class Car {

    private Engine engine;

  

    @Autowired

    public void setEngine(Engine engine) { _// Dependency is injected through the setter_

        this.engine = engine;

    }

}

```
  

**Advantages:**

• Flexible: Dependencies can be modified post-construction.

• Good for optional or reconfigurable dependencies.

  

**Disadvantages:**

• No guarantee that all dependencies are set before the object is used, which could lead to runtime errors.

  

**3. Field Injection**

• Dependencies are injected directly into fields using annotations like @Autowired.

• Simplest form of DI, but less flexible and harder to test compared to constructor injection.

  

**Example:**

  
```

@Component

class Car {

    @Autowired

    private Engine engine; _// Dependency is injected directly into the field_

}

```
  

**Advantages:**

• Requires less boilerplate code (no constructor or setter methods needed).

  

**Disadvantages:**

• Makes testing harder since dependencies cannot be injected easily without reflection.

• Breaks the principle of encapsulation as fields are directly modified by the framework.

  

**Which One Should You Use?**

• **Constructor Injection:** Preferred for mandatory dependencies; promotes immutability and testability.

• **Setter Injection:** Best for optional dependencies or those that might change post-construction.

• **Field Injection:** Convenient but less recommended due to testing and maintainability concerns.

  

Most modern Spring applications prefer **Constructor Injection** because it enforces immutability and ensures that dependencies are properly provided at runtime.



## Understanding the xml configuration 

Certainly! Let me break down the **XML configuration** and explain each part of it.

  

**XML Configuration:**

```
  

<beans xmlns="http://www.springframework.org/schema/beans"

       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

       xsi:schemaLocation="http://www.springframework.org/schema/beans https://www.springframework.org/schema/beans/spring-beans-3.0.xsd">

  

    _<!-- Define Foo bean with constructor injection -->_

    <bean id="foo" class="io.reactivestax.spring.beans.Foo">

        <constructor-arg index="0" value="fooBean"/>

    </bean>

  

    _<!-- Define Bar bean with constructor and property injection -->_

    <bean id="bar" class="io.reactivestax.spring.beans.Bar">

        <constructor-arg index="0" value="BrijeshBar"/>

        <constructor-arg index="1" value="45"/>

        <property name="foo" ref="foo"/>

    </bean>

  

</beans>

```
  

**Explanation**

  

**1. Root <beans> Tag**

  



<beans xmlns="http://www.springframework.org/schema/beans"
```

       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

       xsi:schemaLocation="http://www.springframework.org/schema/beans https://www.springframework.org/schema/beans/spring-beans-3.0.xsd">




• xmlns: Declares the XML namespace for Spring beans. This tells Spring that the XML file is for bean configuration.

• xmlns:xsi: Specifies the XML Schema instance namespace used for validation.

• xsi:schemaLocation: Provides the location of the XML Schema Definition (XSD) file for Spring beans. This helps the XML parser validate the syntax of the configuration.

  

**2. Defining a Bean**

  

```
<bean id="foo" class="io.reactivestax.spring.beans.Foo">

    <constructor-arg index="0" value="fooBean"/>

</bean>

```
  

• <bean>: Declares a bean.

• id: The unique identifier for this bean in the Spring container.

• class: The fully qualified name of the class that this bean represents (e.g., io.reactivestax.spring.beans.Foo).

• <constructor-arg>: Used to pass arguments to the bean’s constructor during its creation.

• index: Specifies the position of the argument in the constructor (starting from 0).

• value: The value of the argument (here, "fooBean").

  

**What happens**:

The Spring container creates an instance of the Foo class using the constructor Foo(String name) and passes "fooBean" as the value for the name parameter.

  

**3. Defining Another Bean with Multiple Injections**

  
```
<bean id="bar" class="io.reactivestax.spring.beans.Bar">

    <constructor-arg index="0" value="BrijeshBar"/>

    <constructor-arg index="1" value="45"/>

    <property name="foo" ref="foo"/>

</bean>

```

  

• <bean>: Declares another bean.

• id: Identifies the bean as bar.

• class: Specifies the class name (io.reactivestax.spring.beans.Bar).

• <constructor-arg>: Passes arguments to the Bar class constructor:

• The first argument (index="0") passes "BrijeshBar" for the name parameter in Bar(String name, int age).

• The second argument (index="1") passes 45 for the age parameter.

• <property>: Injects a dependency into the Bar bean via its setter method.

• name: The name of the property in the Bar class (foo in this case).

• ref: Refers to another bean defined in the same XML file (here, the foo bean).

  

**What happens**:

1. Spring creates an instance of Bar using the constructor Bar(String name, int age), passing "BrijeshBar" and 45 as arguments.

2. It then sets the foo property of Bar by calling the setFoo(Foo foo) method and passing the foo bean as the argument.

  

**Dependency Injection Types Used in the XML**

1. **Constructor Injection**

• The arguments for the constructors of the Foo and Bar classes are specified using <constructor-arg>.

• For example, the Foo bean gets "fooBean" via its constructor, and the Bar bean gets "BrijeshBar" and 45.

2. **Setter/Property Injection**

• The foo property of the Bar class is set using the <property> tag.

• The ref="foo" attribute links the foo bean to the Bar bean’s foo property.

  

**Visual Representation of Bean Wiring**

  

Foo Object

  - name = "fooBean"

  

Bar Object

  - name = "BrijeshBar"

  - age = 45

  - foo = Foo Object (dependency injected)

  

**Benefits of XML Configuration**

1. **Decoupled Code**: The Bar and Foo classes don’t depend on each other directly; the configuration is externalized in XML.

2. **Flexibility**: You can easily change or replace dependencies without modifying Java code.

3. **Clear Dependency Management**: XML explicitly shows how beans are connected.

  
 ## creating new project using apache maven for using spring framework ioc

To use Spring Framework (IoC), we need to create a new project using Apache Maven or Gradle. Here we will use apache maven to create a new project using **mvn archetype** plugin

- run the command `mvn archetype:generate` to trigger the project creation and select the plug-in to create a new project. We use maven plugin `org.apache.maven.archetypes:maven-archetype-quickstart` from the list. To select a given archetype one needs to enter a given archetype plug-in **number** and select the latest version of the plug-in and provide the project coordinates
    
    - groupId [e.g io.reactivestax]
    - artifactId [e.g. spring-app]
    - version [key the default version selected]
- once the new project is created, make sure we update the java compiler in the pom.xm; by updating the property`<maven.compiler.release>1.8</maven.compiler.release>`.


 ## Application Context

In order to use the **ClassPathXmlApplicationContext and FileSystemXmlApplicationContext** we need to include `spring-context` dependecy in the pom.xml

```
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-context</artifactId>
  <version>${spring.version}</version>
</dependency>
```



ApplicationContext has further implementations to use :
1.**ClassPathXmlApplicationContext**

ClassPathXmlApplicationContext is a class in the Spring Framework used to load a Spring application context from one or more XML configuration files located in the classpath. It is ideal when your configuration files are packaged within your application, such as in src/main/resources in a Maven or Gradle project.

**Key Features:**

- _Classpath Dependency_: It resolves the configuration files using the classpath. This is suitable when your configuration files are packaged inside your application JAR/WAR.
    
- **Easy to Use**: Requires minimal configuration since it automatically searches the classpath for the XML file(s).
    
- **XML-based Configuration**: Supports the legacy Spring XML-based bean configuration.


2.**FileSystemXmlApplicationContext:** FileSystemXmlApplicationContext is another class in the Spring Framework used to load a Spring application context from one or more XML configuration files located in the file system (outside the classpath). It allows you to specify absolute or relative file paths.

**Key Features:**

- **File System Dependency**: It resolves the configuration files from the file system. This is suitable when configuration files are stored externally, allowing for easier modification without rebuilding the application.
    
- **Flexible Path Handling**: Supports absolute file paths or relative paths (relative to the current working directory of the JVM process).
    
- **XML-based Configuration**: Similar to ClassPathXmlApplicationContext, it supports legacy XML-based configuration.


example code :
```
```
 File projectHome = new File(System.getProperty("user.dir"));
        ApplicationContext context = new FileSystemXmlApplicationContext("file:"+projectHome.getAbsolutePath()+"/src/main/resources/applicationContext.xml");
```

```

Please note the **"file:"** Plain paths will always be interpreted as relative to the current VM working directory, even if they start with a slash. **Use an explicit "file:" prefix to enforce an absolute file path.**




## - very important 

### **Singleton Beans with Prototype-bean Dependencies**

[](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/lecture22-spring-framework.md#singleton-beans-with-prototype-bean-dependencies)

When you use singleton-scoped beans with dependencies on prototype beans, be aware that dependencies are resolved at instantiation time. Thus, if you dependency-inject a prototype-scoped bean into a singleton-scoped bean, a new prototype bean is instantiated and then dependency-injected into the singleton bean. The prototype instance is the sole instance that is ever supplied to the singleton-scoped bean.

However, suppose you want the singleton-scoped bean to acquire a new instance of the prototype-scoped bean repeatedly at runtime. **You cannot dependency-inject a prototype-scoped bean into your singleton bean, because that injection occurs only once, when the Spring container instantiates the singleton bean and resolves and injects its dependencies.**

If you need a new instance of a prototype bean at runtime more than once, see [Method Injection](https://docs.spring.io/spring-framework/reference/core/beans/dependencies/factory-method-injection.html).


When a **singleton-scoped bean** depends on a **prototype-scoped bean**, Spring’s default behavior injects the prototype bean **only once**, during the instantiation of the singleton bean. This behavior arises because singleton beans are created once and managed for the lifecycle of the application context, while prototype beans are designed to produce a new instance every time they are requested.

  

**Problem**

• **Default Behavior**:

• The singleton bean receives a single instance of the prototype bean when the container initializes it.

• Subsequent calls within the singleton bean to use the prototype dependency will reuse the same instance.

• **Requirement**:

• If you want the singleton bean to always retrieve a **new instance of the prototype bean** at runtime, you cannot rely on traditional dependency injection since it occurs only once.


**Solution: Method Injection**

**Method injection** allows a singleton-scoped bean to dynamically request new instances of a prototype bean at runtime.

**Approaches for Method Injection:**

1. **Using** @Lookup **Annotation** _(Preferred for Simplicity)_:

• Spring provides the @Lookup annotation for beans requiring new instances of prototype-scoped dependencies at runtime.

2. **Using** ObjectFactory **or** Provider **Interface**:

• These interfaces provide programmatic control over retrieving beans from the container.

