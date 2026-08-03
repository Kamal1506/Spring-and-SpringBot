# 📘 Spring Core & Maven Interview Handbook

> **Chapter 1: Spring Framework Fundamentals**

Welcome to the first chapter of the **Spring Core & Maven Interview Handbook**. This chapter covers the fundamental concepts of the Spring Framework that are frequently asked in technical interviews. Mastering these topics will help you confidently answer most basic Spring interview questions.

---

## 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand what the Spring Framework is.
- Explain why Spring was introduced.
- Describe the advantages of using Spring.
- Understand the IoC Container and Dependency Injection.
- Differentiate between IoC and DI.
- Explain Beans and Bean Management.
- Compare BeanFactory and ApplicationContext.
- Understand POJO, Loose Coupling, and Tight Coupling.
- Differentiate Spring Framework and Spring Boot.
- Answer common Spring interview questions with confidence.

---

# 📚 Topics Covered

- What is Spring Framework?
- Why was Spring introduced?
- Why do we use Spring?
- Advantages of Spring
- Spring Modules
- Inversion of Control (IoC)
- Dependency Injection (DI)
- IoC vs Dependency Injection
- Spring Bean
- BeanFactory
- ApplicationContext
- POJO
- Loose Coupling
- Tight Coupling
- Advantages of Dependency Injection
- Objects Created Using `new`
- Spring Framework vs Spring Boot
- Core of Spring Framework

---

# ❓ Interview Questions & Answers

---

## Question 1. What is Spring Framework?

### Interview Definition

Spring Framework is an open-source Java framework that simplifies enterprise application development by providing features like:

- IoC (Inversion of Control)
- Dependency Injection
- AOP
- Transaction Management
- Spring MVC
- Easy integration with databases and other technologies

### Simple Answer

Spring is a Java framework that helps developers build applications faster with less boilerplate code by managing objects, dependencies, and application configuration.

### 💡 Real-World Example

Suppose you're building an **E-Commerce Website**.

**Without Spring**

- Create every object manually
- Connect objects manually
- Manage object lifecycle manually

**With Spring**

- Spring creates objects
- Injects dependencies automatically
- Manages the object lifecycle

### 🎯 Follow-up Questions

**Who developed Spring?**

Rod Johnson

**Is Spring open source?**

Yes.

**Which language is Spring written in?**

Java

**Is Spring only for web applications?**

No.

Spring can also be used for:

- Web Applications
- REST APIs
- Desktop Applications
- Batch Processing
- Microservices
- Cloud Applications

---

## Question 2. Why was Spring introduced?

### Answer

Before Spring, Java EE development mainly relied on **Enterprise JavaBeans (EJB)**, which made applications:

- Complex
- Tightly Coupled
- Difficult to Test
- Hard to Maintain

Spring was introduced to solve these problems by making enterprise development simpler and more flexible.

### Spring solved:

- Tight Coupling
- Complex XML Configuration
- Difficult Testing
- Boilerplate Code
- Complex Enterprise Development

---

## Question 3. Why do we use Spring?

### Answer

Spring provides several powerful features that simplify application development.

- Dependency Injection
- IoC Container
- Aspect-Oriented Programming (AOP)
- Transaction Management
- Spring MVC
- Easy Database Integration
- Modular Architecture
- Better Maintainability

---

## Question 4. What are the advantages of Spring?

### Expected Answer

- Lightweight
- Open Source
- Loose Coupling
- Easy Testing
- Modular Architecture
- Reusable Components
- Easy Integration
- Excellent Documentation
- Supports AOP
- Supports Transactions

---

## Question 5. What are Spring Modules?

### Answer

Spring is divided into multiple modules, each responsible for a specific functionality.

### Common Spring Modules

- Spring Core
- Spring Beans
- Spring Context
- Spring AOP
- Spring JDBC
- Spring ORM
- Spring MVC
- Spring Security
- Spring Test

### Interview Follow-up

**Which Spring modules have you used?**

> I have mainly worked with Spring Core, Spring Context, Spring MVC, Spring Data JPA, and Spring Boot while building my projects.

---

## Question 6. What is IoC (Inversion of Control)?

### Interview Answer

Inversion of Control (IoC) is a principle in which the responsibility of creating and managing objects is transferred from the application to the Spring IoC Container.

### Simple Answer

Normally, developers create objects.

With Spring, Spring creates and manages the objects.

### Example

**Without Spring**

```java
Student student = new Student();
```

**With Spring**

```java
@Autowired
private Student student;
```

Spring automatically provides the object.

### Interview Follow-up

**Who manages objects?**

Spring IoC Container.

**What is an IoC Container?**

The IoC Container creates, configures, manages, and destroys Spring Beans.

---

## Question 7. What is Dependency Injection?

### Interview Answer

Dependency Injection (DI) is a design pattern where the Spring Container provides the required dependencies to a class instead of the class creating them manually.

### Real-World Example

A **Car** depends on an **Engine**.

Instead of:

```java
Engine engine = new Engine();
```

Spring automatically injects the Engine object into the Car.

---

## Question 8. Difference between IoC and Dependency Injection

| IoC | Dependency Injection |
|------|----------------------|
| Principle | Technique used to implement IoC |
| Spring controls object creation | Spring injects dependencies |
| Bigger concept | Part of IoC |
| Focuses on control | Focuses on dependencies |

### Easy Way to Remember

**IoC asks:**

> Who creates the object?

**Answer:** Spring

**DI asks:**

> Who provides the dependency?

**Answer:** Spring

---

## Question 9. What is a Bean?

### Interview Answer

A Bean is an object that is created, configured, and managed by the Spring IoC Container.

### Interview Follow-up

**Is every Java object a Bean?**

No.

Only objects managed by the Spring Container are considered Spring Beans.

---

## Question 10. What is BeanFactory?

### Answer

BeanFactory is the basic IoC Container responsible for creating and managing Spring Beans.

### Features

- Lazy Initialization
- Lightweight
- Basic Container

---

## Question 11. What is ApplicationContext?

### Answer

ApplicationContext is an advanced IoC Container that extends BeanFactory and provides additional features such as:

- Event Handling
- Internationalization (i18n)
- Annotation Support
- Eager Initialization of Singleton Beans

---

## Question 12. Difference between BeanFactory and ApplicationContext

| BeanFactory | ApplicationContext |
|-------------|--------------------|
| Basic Container | Advanced Container |
| Lazy Initialization | Eager Initialization (Singleton Beans by default) |
| Limited Features | Rich Features |
| Rarely Used | Most Commonly Used |

---

## Question 13. What is a POJO?

### Answer

POJO stands for **Plain Old Java Object**.

It is a simple Java class that is **not dependent on any specific framework**.

### Difference between POJO and Bean

| POJO | Spring Bean |
|------|-------------|
| Simple Java Class | Spring-managed Object |
| Independent of Spring | Managed by IoC Container |
| Exists independently | Exists inside Spring Container |

---

## Question 14. What is Loose Coupling?

### Answer

Loose Coupling means classes depend on abstractions rather than concrete implementations, making applications easier to maintain, test, and modify.

### Example

**Bad Practice**

```java
Car car = new Car(new PetrolEngine());
```

**Better Practice**

```java
@Autowired
private Engine engine;
```

Spring decides which implementation to inject.

---

## Question 15. What is Tight Coupling?

### Answer

Tight Coupling occurs when one class directly depends on another concrete class, making the application difficult to maintain and modify.

---

## Question 16. What is the main advantage of Dependency Injection?

### Expected Answer

- Loose Coupling
- Easy Testing
- Better Maintainability
- Reusability

---

## Question 17. Can Spring manage objects created using `new`?

### Answer

No.

Objects created using the `new` keyword are **not managed by the Spring IoC Container**.

As a result:

- Dependency Injection will not work.
- Bean Lifecycle methods will not execute.
- Spring cannot manage the object.

---

## Question 18. Is Spring Framework and Spring Boot the same?

### Answer

No.

| Spring Framework | Spring Boot |
|------------------|-------------|
| Core Framework | Built on top of Spring Framework |
| Manual Configuration | Auto Configuration |
| Requires more setup | Minimal Configuration |
| No Embedded Server | Embedded Tomcat/Jetty |
| Flexible | Faster Development |

---

## Question 19. What is the core of the Spring Framework?

### Answer

The **IoC (Inversion of Control) Container** is the core of the Spring Framework.

It is responsible for:

- Creating Beans
- Configuring Beans
- Injecting Dependencies
- Managing the Bean Lifecycle

---

# 💡 Key Interview Tips

- Understand the concepts instead of memorizing definitions.
- Be able to explain each topic using a real-world example.
- Learn common comparisons such as IoC vs DI and BeanFactory vs ApplicationContext.
- Expect follow-up questions during technical interviews.
- Practice explaining concepts in simple language.

---

# 📝 Chapter Summary

In this chapter, you learned the core concepts of the Spring Framework, including:

- Spring Fundamentals
- Why Spring was introduced
- IoC and Dependency Injection
- Spring Beans
- BeanFactory and ApplicationContext
- POJO
- Loose Coupling
- Tight Coupling
- Spring Framework vs Spring Boot

These concepts form the foundation of Spring development and are among the most frequently asked topics in Java backend interviews.

---
