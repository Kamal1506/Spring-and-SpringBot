# 📘 Spring IoC Container Interview Handbook

> **Chapter 3: Spring IoC Container**

The **Spring IoC (Inversion of Control) Container** is the heart of the Spring Framework. It is responsible for creating, configuring, managing, injecting, and destroying Spring Beans. Understanding the IoC Container is essential because it is one of the most frequently discussed topics in Spring interviews.

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand the Spring IoC Container.
- Explain the responsibilities of the IoC Container.
- Describe how the IoC Container works internally.
- Understand Bean creation and Bean Definitions.
- Compare BeanFactory and ApplicationContext.
- Explain Lazy and Eager Initialization.
- Understand Dependency Lookup.
- Learn Component Scanning.
- Answer common IoC Container interview questions confidently.

---

# 📚 Topics Covered

- Spring IoC Container
- Responsibilities of IoC Container
- Internal Working of IoC Container
- Spring Bean
- Bean Definition
- Ways to Define a Bean
- BeanFactory
- ApplicationContext
- BeanFactory vs ApplicationContext
- Lazy Initialization
- Eager Initialization
- Dependency Lookup
- Component Scanning
- Spring Startup Flow
- Bean Dependencies
- Multiple Beans
- Bean Not Found
- Primitive Values in Spring
- Manual Bean Creation
- Scenario-Based Questions
- Frequently Asked Differences

---

# ❓ Interview Questions & Answers

---

## Question 1. What is the Spring IoC Container?

### Interview Definition

The **Spring IoC (Inversion of Control) Container** is the core component of the Spring Framework that creates, configures, manages, injects, and destroys beans throughout the application lifecycle.

### Simple Answer

The IoC Container acts like a manager.

Instead of developers creating and managing objects manually, Spring creates and manages them automatically.

### 💡 Real-World Example

Suppose your application contains:

- Student
- Course
- Teacher
- Database
- EmailService

**Without Spring**

```java
Student student = new Student();
Teacher teacher = new Teacher();
Course course = new Course();
```

Everything is created manually.

**With Spring**

The IoC Container automatically:

- Creates Student
- Creates Teacher
- Creates Course
- Creates Database
- Creates EmailService

### 🎯 Interview Follow-up

**Who creates Beans?**

Spring IoC Container.

**Who injects Dependencies?**

Spring IoC Container.

**Who destroys Beans?**

Spring IoC Container.

---

## Question 2. What are the responsibilities of the IoC Container?

### Answer

The IoC Container is responsible for:

- Creating Beans
- Configuring Beans
- Injecting Dependencies
- Managing Bean Lifecycle
- Handling Bean Scopes
- Performing Autowiring
- Destroying Beans when required

### Easy Way to Remember

```
Create
   ↓
Configure
   ↓
Inject
   ↓
Manage
   ↓
Destroy
```

---

## Question 3. How does the IoC Container work internally?

### Internal Flow

```
Application Starts
        │
        ▼
Read Configuration
(XML / Annotation / Java Config)
        │
        ▼
Create IoC Container
        │
        ▼
Scan Components
        │
        ▼
Create Beans
        │
        ▼
Inject Dependencies
        │
        ▼
Application Ready
```

### Example

```java
@Service
class StudentService {

}
```

Spring starts →

Finds `@Service` →

Creates `StudentService` Bean →

Stores it inside the IoC Container.

---

## Question 4. What is a Bean?

### Interview Definition

A Bean is an object that is instantiated, configured, and managed by the Spring IoC Container.

### Follow-up

**Is every Java object a Bean?**

No.

### Example (Not a Bean)

```java
Student student = new Student();
```

Spring did not create this object.

### Example (Bean)

```java
@Component
class Student {

}
```

Spring manages this object as a Bean.

---

## Question 5. What is a Bean Definition?

### Definition

A Bean Definition contains metadata that tells Spring how to create and manage a Bean.

It includes:

- Bean Class
- Bean Name
- Scope
- Constructor Arguments
- Properties
- Lifecycle Methods

### Example

```xml
<bean
    id="student"
    class="com.demo.Student"/>
```

This is a Bean Definition.

---

## Question 6. What are the ways to define a Bean?

### Three Ways

### XML Configuration

```xml
<bean></bean>
```

### Annotation-Based

```java
@Component
```

### Java Configuration

```java
@Bean
```

### Interview Follow-up

**Which approach is most commonly used today?**

Annotation-Based Configuration along with Java Configuration.

---

## Question 7. What is BeanFactory?

### Definition

BeanFactory is the basic IoC Container responsible for creating and managing Beans.

### Features

- Lightweight
- Lazy Initialization
- Basic Container
- Uses Less Memory

---

## Question 8. What is ApplicationContext?

### Definition

ApplicationContext is an advanced IoC Container that extends BeanFactory and provides additional enterprise features.

### Features

- Event Handling
- Internationalization (i18n)
- Annotation Support
- AOP Integration
- Eager Initialization (Singleton Beans by default)

### Interview Follow-up

**Which one is used in Spring Boot?**

ApplicationContext.

---

## Question 9. Difference between BeanFactory and ApplicationContext

| BeanFactory | ApplicationContext |
|-------------|--------------------|
| Basic Container | Advanced Container |
| Lazy Initialization | Eager Initialization (Singleton Beans by default) |
| Limited Features | Rich Enterprise Features |
| Rarely Used | Mostly Used |

---

## Question 10. What is Lazy Initialization?

### Definition

A Bean is created only when it is requested.

### Flow

```
Application Starts
        │
        ▼
Bean Not Created
        │
        ▼
Request Bean
        │
        ▼
Bean Created
```

### Example

```java
@Lazy
@Component
class Student {

}
```

### Advantages

- Faster Startup
- Lower Initial Memory Usage

### Disadvantages

- First Access is Slower

---

## Question 11. What is Eager Initialization?

### Definition

A Bean is created during application startup.

### Flow

```
Application Starts
        │
        ▼
Bean Created
        │
        ▼
Application Ready
```

ApplicationContext uses eager initialization for singleton beans by default.

---

## Question 12. Difference between Lazy and Eager Initialization

| Lazy Initialization | Eager Initialization |
|---------------------|----------------------|
| Created when required | Created during startup |
| Faster Startup | Slower Startup |
| Lower Initial Memory | Higher Initial Memory |
| Uses `@Lazy` | Default for Singleton Beans |

---

## Question 13. What is Dependency Lookup?

### Definition

Dependency Lookup is a technique where the application explicitly requests a Bean from the IoC Container.

### Example

```java
ApplicationContext context = ...;

Student student = context.getBean(Student.class);
```

### Interview Tip

Modern Spring applications prefer **Dependency Injection** instead of Dependency Lookup because it results in cleaner and less coupled code.

---

## Question 14. What is Component Scanning?

### Definition

Component Scanning is the process where Spring automatically scans packages for classes annotated with:

- `@Component`
- `@Service`
- `@Repository`
- `@Controller`

and registers them as Spring Beans.

---

## Question 15. What happens when Spring starts?

### Internal Startup Flow

```
SpringApplication.run()
        │
        ▼
Create ApplicationContext
        │
        ▼
Scan Components
        │
        ▼
Read Configuration
        │
        ▼
Create Singleton Beans
        │
        ▼
Inject Dependencies
        │
        ▼
Application Ready
```

---

## Question 16. Can one Bean depend on another Bean?

### Answer

Yes.

### Example

```
StudentService
        │
        ▼
StudentRepository
```

Spring automatically injects `StudentRepository` into `StudentService`.

---

## Question 17. Can we create multiple Beans of the same class?

### Answer

Yes.

### Example

```java
@Bean
public Student student1() {
    return new Student();
}

@Bean
public Student student2() {
    return new Student();
}
```

Use `@Qualifier` when specifying which Bean should be injected.

---

## Question 18. What happens if a Bean is not found?

### Answer

Spring throws an exception.

Most common exception:

```
NoSuchBeanDefinitionException
```

---

## Question 19. Can the IoC Container manage primitive types?

### Answer

Generally, No.

The IoC Container manages objects (Beans).

Primitive values such as `int`, `String`, and `boolean` are injected into Beans through configuration, but they are not typically managed as standalone Beans.

---

## Question 20. Can we manually create a Bean?

### Answer

Yes.

Using `@Bean` inside a `@Configuration` class.

### Example

```java
@Configuration
class AppConfig {

    @Bean
    public Student student() {
        return new Student();
    }
}
```

---

# 💼 Real-Time Interview Questions

## Why do we need the IoC Container?

### Expected Answer

Because it:

- Eliminates manual object creation.
- Reduces coupling.
- Improves testability.
- Manages the Bean lifecycle.
- Supports Dependency Injection.

---

## Why is ApplicationContext preferred?

Because it provides:

- Event Handling
- Internationalization (i18n)
- Annotation Support
- AOP Integration
- Advanced Bean Management

---

## What happens if the IoC Container is removed?

You must manually:

- Create every object.
- Connect dependencies.
- Manage object lifecycle.
- Handle configuration.

This results in tightly coupled and difficult-to-maintain applications.

---

# 🧠 Scenario-Based Questions

## Scenario 1

### You wrote:

```java
Student student = new Student();
```

Will Spring inject dependencies?

**Answer**

No.

Spring only injects dependencies into objects managed by the IoC Container.

---

## Scenario 2

### You forgot to add `@Component`.

What happens?

**Answer**

Spring does not register the class as a Bean (unless it is defined another way, such as with `@Bean`).

Dependency Injection will not work.

---

## Scenario 3

### Two developers create the same Bean.

What happens?

**Answer**

- If the Bean names are different, both Beans can exist.
- If the Bean names conflict, Spring reports a Bean Definition conflict unless Bean overriding is enabled.

---

# ⚖️ Frequently Asked Differences

## IoC vs Dependency Injection

| IoC | Dependency Injection |
|------|----------------------|
| Principle | Technique used to implement IoC |
| Spring controls object creation | Spring injects dependencies |

---

## Bean vs POJO

| POJO | Bean |
|------|------|
| Plain Java Object | Spring-managed Object |
| Independent of Spring | Managed by IoC Container |

---

## BeanFactory vs ApplicationContext

| BeanFactory | ApplicationContext |
|-------------|--------------------|
| Basic Container | Advanced Container |
| Lazy Initialization | Eager Initialization (Singleton Beans by default) |

---

## Lazy vs Eager Initialization

| Lazy | Eager |
|------|-------|
| Created when needed | Created during startup |
| Faster startup | Slower startup |
| Lower initial memory usage | Higher initial memory usage |

---

# 💡 Key Interview Tips

- Always remember that the **IoC Container is the core of the Spring Framework**.
- Understand the difference between **IoC** and **Dependency Injection**.
- Know when to use **BeanFactory** and **ApplicationContext**.
- Explain **Lazy** and **Eager Initialization** with practical examples.
- Be prepared for scenario-based questions about Bean creation and Dependency Injection.

---

# 📝 Chapter Summary

In this chapter, you learned:

- Spring IoC Container
- Bean Management
- Bean Definitions
- BeanFactory
- ApplicationContext
- Bean Lifecycle
- Component Scanning
- Dependency Lookup
- Lazy & Eager Initialization
- Spring Startup Process
- Real-world Scenarios
- Frequently Asked Interview Differences

These concepts are fundamental to Spring development and are among the most commonly asked topics in Java backend interviews.

---

## 🚀 Next Chapter

**Chapter 4 – Spring Dependency Injection**
