# 📘 Spring Bean Configuration & Dependency Injection Interview Handbook

> **Chapter 4: Bean Configuration & Dependency Injection**

This chapter covers one of the most important areas of the Spring Framework—**Bean Configuration** and **Dependency Injection (DI)**. These concepts form the backbone of Spring applications and are among the most frequently asked topics in Java backend interviews.

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand Bean Configuration in Spring.
- Learn different ways to configure Beans.
- Differentiate XML, Annotation, and Java-based configuration.
- Understand stereotype annotations.
- Learn Component Scanning.
- Master Dependency Injection (DI).
- Compare Constructor, Setter, and Field Injection.
- Understand `@Autowired`, `@Qualifier`, `@Primary`, `@Inject`, and `@Resource`.
- Answer common interview and scenario-based questions confidently.

---

# 📚 Topics Covered

## Bean Configuration

- Bean Configuration
- XML Configuration
- Annotation-Based Configuration
- Java-Based Configuration
- `@Configuration`
- `@Bean`
- `@ComponentScan`
- Component Scanning
- Stereotype Annotations
- `@Component`
- `@Service`
- `@Repository`
- `@Controller`
- `@RestController`

## Dependency Injection

- Dependency Injection
- Types of Dependency Injection
- Constructor Injection
- Setter Injection
- Field Injection
- `@Autowired`
- `@Qualifier`
- `@Primary`
- `@Inject`
- `@Resource`
- Common Differences
- Scenario-Based Questions

---

# ❓ Interview Questions & Answers

---

# Part 1 – Bean Configuration

---

## Question 1. What is Bean Configuration?

### Interview Definition

Bean Configuration is the process of defining how Spring should create, configure, and manage Beans inside the IoC Container.

### Simple Answer

Bean Configuration tells Spring:

- Which class to create
- How to create it
- Which dependencies to inject
- What Bean scope to use

### 💡 Real-World Example

Imagine Spring is a **restaurant**.

Before the chef prepares food, he needs the recipe.

Bean Configuration acts as that recipe by telling Spring exactly how to create and manage the object.

---

## Question 2. What are the ways to configure a Bean?

There are **three ways** to configure Beans.

### 1. XML Configuration

```xml
<bean id="student"
      class="com.demo.Student"/>
```

### 2. Annotation-Based Configuration

```java
@Component
class Student {

}
```

### 3. Java-Based Configuration

```java
@Bean
public Student student() {
    return new Student();
}
```

### Interview Follow-up

**Which configuration style is mostly used today?**

> Annotation-Based Configuration together with Java Configuration.

XML configuration is mainly found in legacy applications.

---

## Question 3. What is XML Bean Configuration?

### Definition

Beans are declared inside an XML configuration file.

### Example

```xml
<bean
    id="student"
    class="com.demo.Student"/>
```

### Advantages

- Easy to modify without changing Java code
- Useful for legacy projects

### Disadvantages

- Verbose
- Hard to maintain
- Rarely used in modern applications

---

## Question 4. What is Annotation-Based Configuration?

### Definition

Beans are created using annotations instead of XML configuration.

### Example

```java
@Component
public class Student {

}
```

Spring automatically detects and registers the Bean.

### Advantages

- Less configuration
- Cleaner code
- Easier maintenance

---

## Question 5. What is Java-Based Configuration?

### Definition

Beans are created using Java methods instead of XML.

### Example

```java
@Configuration
public class AppConfig {

    @Bean
    public Student student() {
        return new Student();
    }
}
```

### Interview Follow-up

**Why use Java Configuration?**

Because it is:

- Type-safe
- Easy to debug
- IDE-friendly
- Better suited for modern Spring applications

---

## Question 6. What is `@Configuration`?

### Definition

`@Configuration` marks a class as a source of Spring Bean definitions.

### Example

```java
@Configuration
class AppConfig {

}
```

Think of it as:

> "This class contains Spring configuration."

---

## Question 7. What is `@Bean`?

### Definition

`@Bean` tells Spring to register the returned object as a Spring Bean.

### Example

```java
@Bean
public Student student() {
    return new Student();
}
```

### Interview Follow-up

**Can `@Bean` exist without `@Configuration`?**

Technically yes, but its intended and recommended use is inside a `@Configuration` class, where Spring ensures proper Bean lifecycle management and singleton behavior.

---

## Question 8. Difference between `@Bean` and `@Component`

| `@Bean` | `@Component` |
|----------|--------------|
| Used on methods | Used on classes |
| Manual Bean creation | Automatic Bean detection |
| Usually inside `@Configuration` | Used with Component Scanning |
| Best for third-party classes | Best for your own classes |

### 💡 Real-World Example

If you wrote the class yourself:

```java
@Component
class Student {

}
```

If you are using a third-party library:

```java
@Bean
public ObjectMapper objectMapper() {
    return new ObjectMapper();
}
```

You cannot modify library classes, so `@Bean` is the preferred approach.

---

## Question 9. What is Component Scanning?

### Definition

Component Scanning is the process where Spring automatically scans packages for annotated classes and registers them as Beans.

### Common Annotations

- `@Component`
- `@Service`
- `@Repository`
- `@Controller`

### Flow

```
Application Starts
        │
        ▼
@ComponentScan
        │
        ▼
Scan Packages
        │
        ▼
Find Components
        │
        ▼
Register Beans
```

---

## Question 10. What is `@ComponentScan`?

### Definition

`@ComponentScan` tells Spring where to search for Components.

### Example

```java
@ComponentScan("com.demo")
```

### Spring Boot

`@SpringBootApplication` already includes `@ComponentScan`, so you usually don't need to add it manually.

---

## Question 11. What are Stereotype Annotations?

### Definition

Stereotype Annotations are specialized versions of `@Component` that indicate the role of a class.

### Common Stereotypes

- `@Component`
- `@Service`
- `@Repository`
- `@Controller`
- `@RestController`

---

## Question 12. What is `@Component`?

### Definition

Marks a generic Java class as a Spring Bean.

### Example

```java
@Component
class Student {

}
```

---

## Question 13. What is `@Service`?

### Definition

Represents the **Service Layer** of an application.

### Example

```java
@Service
class StudentService {

}
```

### Typical Responsibilities

- Business Logic
- Salary Calculation
- Tax Calculation
- Login Validation

---

## Question 14. What is `@Repository`?

### Definition

Represents the **Data Access Layer**.

### Example

```java
@Repository
class StudentRepository {

}
```

### Purpose

Handles database operations.

### Additional Feature

Spring automatically translates certain persistence exceptions into Spring's data access exception hierarchy.

---

## Question 15. What is `@Controller`?

### Definition

Handles HTTP requests and returns **Views**.

Commonly used with:

- JSP
- Thymeleaf

---

## Question 16. What is `@RestController`?

### Definition

Handles REST requests and directly returns data such as JSON or XML.

### Difference

| `@Controller` | `@RestController` |
|---------------|-------------------|
| Returns Views | Returns Data |
| Used in Spring MVC | Used in REST APIs |

---

# Part 2 – Dependency Injection

---

## Question 17. What is Dependency Injection?

### Definition

Dependency Injection (DI) is a design pattern where Spring provides the required dependencies instead of the class creating them manually.

### Example

**Without DI**

```java
Engine engine = new Engine();
```

**With DI**

```java
@Autowired
private Engine engine;
```

---

## Question 18. What are the types of Dependency Injection?

There are three types:

- Constructor Injection
- Setter Injection
- Field Injection

---

## Question 19. What is Constructor Injection?

### Definition

Dependencies are injected through the constructor.

### Example

```java
@Service
public class CarService {

    private final Engine engine;

    public CarService(Engine engine) {
        this.engine = engine;
    }
}
```

### Advantages

- Mandatory dependencies
- Immutable objects
- Easier unit testing
- Recommended by Spring

---

## Question 20. What is Setter Injection?

### Example

```java
@Autowired
public void setEngine(Engine engine) {
    this.engine = engine;
}
```

### Advantages

- Suitable for optional dependencies
- Dependencies can be changed later

### Disadvantages

The object may exist in an incomplete state until the setter is called.

---

## Question 21. What is Field Injection?

### Example

```java
@Autowired
private Engine engine;
```

### Advantages

- Less boilerplate code

### Disadvantages

- Harder to test
- Hidden dependencies
- Cannot make dependencies `final`

### Interview Tip

For modern applications, **Constructor Injection is recommended**.

---

## Question 22. Difference between Constructor and Setter Injection

| Constructor Injection | Setter Injection |
|------------------------|------------------|
| Mandatory dependency | Optional dependency |
| Immutable | Mutable |
| Recommended | Less preferred |
| Better for testing | Easier to reconfigure |

---

## Question 23. What is `@Autowired`?

### Definition

`@Autowired` tells Spring to automatically inject a matching Bean.

### Example

```java
@Autowired
private StudentService service;
```

### Internal Working

```
Application Starts
        │
        ▼
Find @Autowired
        │
        ▼
Search Matching Bean
        │
        ▼
Inject Bean
```

---

## Question 24. How does `@Autowired` work?

Spring first resolves dependencies **by type**.

- If one matching Bean exists → inject it.
- If multiple Beans exist → use `@Qualifier`, `@Primary`, or another mechanism to resolve the ambiguity.

---

## Question 25. What is `@Qualifier`?

Suppose two Beans exist:

- PetrolEngine
- DieselEngine

Both implement:

```java
Engine
```

Specify which Bean to inject.

```java
@Autowired
@Qualifier("petrolEngine")
private Engine engine;
```

---

## Question 26. What is `@Primary`?

### Definition

`@Primary` marks one Bean as the default choice when multiple Beans of the same type exist.

### Example

```java
@Primary
@Component
class PetrolEngine {

}
```

---

## Question 27. Difference between `@Qualifier` and `@Primary`

| `@Qualifier` | `@Primary` |
|--------------|------------|
| Selects a specific Bean | Declares the default Bean |
| Used at the injection point | Used on the Bean definition |
| Higher priority | Used when no qualifier is specified |

---

## Question 28. What is `@Inject`?

### Definition

`@Inject` is the standard dependency injection annotation provided by Jakarta Dependency Injection.

Spring supports it similarly to `@Autowired`.

---

## Question 29. Difference between `@Autowired` and `@Inject`

| `@Autowired` | `@Inject` |
|--------------|-----------|
| Spring-specific | Jakarta Standard |
| Supports `required` attribute | No `required` attribute |
| Most common in Spring | Useful for framework portability |

---

## Question 30. What is `@Resource`?

### Definition

`@Resource` is a Jakarta annotation that injects a Bean, typically resolving **by name first**, then by type if necessary.

### Example

```java
@Resource
private StudentService service;
```

---

## Question 31. Difference between `@Autowired` and `@Resource`

| `@Autowired` | `@Resource` |
|--------------|-------------|
| Primarily resolves by type | Primarily resolves by name |
| Spring Annotation | Jakarta Annotation |
| Often combined with `@Qualifier` | Bean name is commonly used |

---

# 💼 Real-Time Interview Questions

## Why is Constructor Injection recommended?

### Expected Answer

Because it:

- Makes dependencies mandatory.
- Improves unit testing.
- Supports immutable objects.
- Clearly declares class dependencies.

---

## Why use `@Qualifier`?

When multiple Beans of the same type exist, Spring needs to know exactly which Bean should be injected.

---

## Why use `@Bean` instead of `@Component`?

Use `@Bean` when creating Beans for third-party classes that you cannot modify.

---

# 🧠 Scenario-Based Questions

## Scenario 1

### Two `Engine` Beans exist. What happens?

**Answer**

Spring throws a `NoUniqueBeanDefinitionException` unless the ambiguity is resolved using `@Qualifier`, `@Primary`, or another suitable approach.

---

## Scenario 2

### No matching Bean exists. What happens?

**Answer**

Spring throws a `NoSuchBeanDefinitionException` (or a related dependency exception during application startup).

---

## Scenario 3

### You forgot to add `@Component`. Will Spring create the Bean?

**Answer**

No.

Unless the Bean is registered another way (such as using an `@Bean` method), Spring will not create it.

---

# 💡 Key Interview Tips

- Prefer **Annotation-Based Configuration** in modern Spring applications.
- Understand when to use `@Component` versus `@Bean`.
- Remember the responsibilities of each stereotype annotation.
- Constructor Injection is the recommended approach for new applications.
- Know the difference between `@Qualifier`, `@Primary`, `@Autowired`, `@Inject`, and `@Resource`.
- Be prepared for scenario-based questions involving multiple Beans.

---

# 📝 Chapter Summary

In this chapter, you learned:

- Bean Configuration
- XML, Annotation, and Java-Based Configuration
- `@Configuration`
- `@Bean`
- Component Scanning
- Stereotype Annotations
- Dependency Injection
- Constructor, Setter, and Field Injection
- `@Autowired`
- `@Qualifier`
- `@Primary`
- `@Inject`
- `@Resource`
- Common Interview Scenarios
- Frequently Asked Differences

These concepts are fundamental to Spring development and are among the most frequently asked topics in Spring and Spring Boot interviews.

---
