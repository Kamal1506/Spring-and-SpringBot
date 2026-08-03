# 📘 Spring Boot Interview Handbook

> **Chapter 6: Spring Boot Fundamentals**

**Interview Importance:** ⭐⭐⭐⭐⭐ (Extremely High)

Spring Boot is one of the most important topics in Java backend interviews. Most modern enterprise applications are built using Spring Boot, making it a must-know technology for every Java developer.

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand what Spring Boot is.
- Explain why Spring Boot was introduced.
- Describe the core features of Spring Boot.
- Understand Auto Configuration and Starter Dependencies.
- Explain Embedded Servers.
- Understand Convention over Configuration.
- Learn the Spring Boot project structure.
- Explain the internal startup process.
- Differentiate Spring Framework, Spring MVC, and Spring Boot.
- Answer real-world Spring Boot interview questions confidently.

---

# 📚 Topics Covered

- Spring Boot
- Why Spring Boot?
- Features of Spring Boot
- Auto Configuration
- Convention over Configuration
- Starter Dependencies
- Embedded Server
- `@SpringBootApplication`
- `@EnableAutoConfiguration`
- `@ComponentScan`
- Spring Initializr
- Spring Boot Project Structure
- Spring Boot Startup Process
- `application.properties`
- Spring vs Spring Boot
- Spring Boot vs Spring MVC
- Scenario-Based Questions
- Frequently Asked Differences

---

# ❓ Interview Questions & Answers

---

## Question 1. What is Spring Boot?

### ⭐ Interview Definition

Spring Boot is an extension of the Spring Framework that simplifies application development by providing **Auto Configuration**, **Starter Dependencies**, **Embedded Servers**, and **Convention over Configuration**.

### Simple Answer

Spring Boot helps developers build Spring applications quickly with minimal configuration.

Instead of manually configuring everything, Spring Boot performs most of the setup automatically.

### 💡 Real-World Example

### Without Spring Boot

To build a web application, you typically configure:

- DispatcherServlet
- Tomcat
- Component Scanning
- View Resolver
- Dependencies
- Database
- Properties

A lot of manual work is required.

### With Spring Boot

```
Create Project
      │
      ▼
Add Dependency
      │
      ▼
Write Controller
      │
      ▼
Run Application
```

Done.

---

## Question 2. Why was Spring Boot introduced?

### Expected Answer

Spring Boot was introduced to reduce the complexity of configuring Spring applications.

It provides:

- Auto Configuration
- Embedded Servers
- Starter Dependencies
- Production-ready Features
- Faster Development

---

## Question 3. Why do we use Spring Boot?

### Answer

Spring Boot is used because it:

- Reduces configuration
- Speeds up development
- Provides embedded servers
- Simplifies dependency management
- Makes deployment easier
- Supports microservices

---

## Question 4. What are the features of Spring Boot?

### Important Features

- Auto Configuration
- Starter Dependencies
- Embedded Tomcat
- Convention over Configuration
- Spring Boot Actuator
- Externalized Configuration
- Easy Deployment

---

## Question 5. What is Auto Configuration?

### ⭐ Most Asked Spring Boot Question

### Definition

Auto Configuration automatically configures Spring Beans based on the dependencies available in the project.

### Example

Suppose you add:

```xml
spring-boot-starter-web
```

Spring Boot automatically configures:

- DispatcherServlet
- Embedded Tomcat
- Jackson
- Spring MVC Configuration

No manual configuration is required.

### Without Auto Configuration

You configure everything manually.

### With Auto Configuration

Spring Boot detects what your application needs and configures it automatically.

---

## Question 6. What is Convention over Configuration?

### Definition

Convention over Configuration means Spring Boot follows sensible defaults so developers don't have to configure common settings manually.

### Example

Create:

```
application.properties
```

Spring Boot automatically loads it during startup.

No extra configuration is required.

---

## Question 7. What are Starter Dependencies?

### Definition

Starter Dependencies are pre-packaged collections of dependencies that provide everything required for a specific feature.

### Example

```
spring-boot-starter-web
```

Includes:

- Spring MVC
- Embedded Tomcat
- Jackson
- Validation
- Logging

You don't need to add each dependency individually.

### Popular Starters

- `spring-boot-starter-web`
- `spring-boot-starter-data-jpa`
- `spring-boot-starter-security`
- `spring-boot-starter-test`

---

## Question 8. What is an Embedded Server?

### Definition

An Embedded Server is a web server packaged inside your Spring Boot application.

### Supported Servers

- Tomcat (Default)
- Jetty
- Undertow

### Without Spring Boot

```
Install Tomcat

↓

Deploy WAR
```

### With Spring Boot

```
Run Application

↓

Embedded Tomcat Starts Automatically
```

---

## Question 9. What is `@SpringBootApplication`?

### ⭐ Very Important

### Definition

`@SpringBootApplication` is the main annotation that enables a Spring Boot application.

It combines three annotations:

- `@SpringBootConfiguration`
- `@EnableAutoConfiguration`
- `@ComponentScan`

### Interview Follow-up

**What does `@SpringBootApplication` contain?**

- `@SpringBootConfiguration`
- `@EnableAutoConfiguration`
- `@ComponentScan`

---

## Question 10. What is `@EnableAutoConfiguration`?

### Definition

It tells Spring Boot to automatically configure Beans based on the dependencies and configuration available in the application.

---

## Question 11. What is `@ComponentScan`?

### Definition

`@ComponentScan` searches the package of the main application class and its sub-packages for Spring components.

### Example

If your main class is located in:

```
com.demo
```

Spring scans:

```
com.demo.*
```

---

## Question 12. What is Spring Initializr?

### Definition

Spring Initializr is a tool that generates a ready-to-use Spring Boot project with selected dependencies.

### Interview Tip

When asked:

**How do you create a Spring Boot project?**

Mention:

- Spring Initializr
- IntelliJ IDEA
- Eclipse (STS)
- VS Code Extensions
- Maven Command Line

---

## Question 13. Explain the Spring Boot Project Structure.

```
src
├── main
│   ├── java
│   │   ├── controller
│   │   ├── service
│   │   ├── repository
│   │   ├── entity
│   │   └── Application.java
│   │
│   └── resources
│       ├── application.properties
│       └── static
```

---

## Question 14. How does Spring Boot start?

### ⭐ Very Important

```
main()
     │
     ▼
SpringApplication.run()
     │
     ▼
Create ApplicationContext
     │
     ▼
Component Scan
     │
     ▼
Auto Configuration
     │
     ▼
Create Beans
     │
     ▼
Start Embedded Server
     │
     ▼
Application Ready
```

---

## Question 15. Difference between Spring Framework and Spring Boot

| Spring Framework | Spring Boot |
|------------------|-------------|
| Requires more manual configuration | Auto Configuration |
| External server usually required | Embedded Server |
| More setup | Faster development |
| No starter dependencies | Starter dependencies available |
| Flexible but verbose | Convention over Configuration |

---

## Question 16. Difference between Spring Boot and Spring MVC

| Spring Boot | Spring MVC |
|--------------|------------|
| Framework extension | Web framework |
| Simplifies application setup | Handles web requests using MVC |
| Builds REST APIs, web apps, and microservices | Focuses on the MVC architecture |

---

## Question 17. What is `application.properties`?

### Definition

`application.properties` stores application configuration.

### Example

```properties
server.port=8081

spring.datasource.url=jdbc:mysql://localhost:3306/studentdb
```

---

## Question 18. Why is Spring Boot popular?

### Expected Answer

Because it:

- Reduces boilerplate code
- Speeds up development
- Simplifies deployment
- Provides production-ready features
- Supports microservices

---

# 💼 Real-Time Interview Questions

## Why did you use Spring Boot in your project?

### Sample Answer

> I used Spring Boot because it reduced configuration, provided starter dependencies, included an embedded Tomcat server, and made it easy to build REST APIs. It also integrated seamlessly with Spring Data JPA, making database operations and deployment much simpler.

---

## Why not use Spring Framework directly?

### Expected Answer

Spring Boot speeds up development by providing Auto Configuration, Starter Dependencies, and sensible defaults while still being built on top of the Spring Framework.

---

## Why is Embedded Tomcat useful?

### Expected Answer

Because there is no need to install or configure a separate web server.

The application can be started simply by running:

```bash
mvn spring-boot:run
```

or

executing the packaged JAR file.

---

# 🧠 Scenario-Based Questions

## Scenario 1

### You added:

```
spring-boot-starter-data-jpa
```

What happens?

**Answer**

Spring Boot automatically configures JPA components if the required dependencies and configuration are available.

---

## Scenario 2

### You changed:

```properties
server.port=9090
```

What happens?

**Answer**

The embedded server starts on **port 9090** instead of the default **8080**.

---

## Scenario 3

### You removed `@SpringBootApplication`.

What happens?

**Answer**

The application is no longer configured as a Spring Boot application.

Features such as:

- Auto Configuration
- Component Scanning
- Spring Boot startup behavior

will not work unless they are configured manually.

---

# ⚖️ Frequently Asked Differences

## Spring Framework vs Spring Boot

| Spring Framework | Spring Boot |
|------------------|-------------|
| More configuration | Minimal configuration |
| External server | Embedded server |

---

## Starter vs Dependency

| Starter | Dependency |
|----------|------------|
| Collection of related dependencies | Single library |

---

## Tomcat vs Embedded Tomcat

| Tomcat | Embedded Tomcat |
|---------|-----------------|
| Installed separately | Packaged inside the application |

---

## Spring MVC vs Spring Boot

| Spring MVC | Spring Boot |
|------------|-------------|
| Web framework | Framework extension |
| Focuses on MVC architecture | Simplifies overall Spring development |

---

# 💡 Key Interview Tips

- Understand **Auto Configuration** thoroughly—it is one of the most frequently asked Spring Boot topics.
- Remember the three annotations inside `@SpringBootApplication`.
- Learn the Spring Boot startup flow from `main()` to **Application Ready**.
- Be able to explain the advantages of Embedded Tomcat and Starter Dependencies.
- Know the difference between **Spring Framework**, **Spring MVC**, and **Spring Boot**.
- Use examples from your own projects when explaining why you chose Spring Boot.

---

# 📝 Chapter Summary

In this chapter, you learned:

- Spring Boot Fundamentals
- Auto Configuration
- Starter Dependencies
- Embedded Server
- Convention over Configuration
- `@SpringBootApplication`
- `@EnableAutoConfiguration`
- `@ComponentScan`
- Spring Initializr
- Project Structure
- Startup Process
- `application.properties`
- Spring Framework vs Spring Boot
- Spring Boot vs Spring MVC
- Real-world Scenarios
- Frequently Asked Interview Differences

These concepts form the foundation of modern Spring Boot development and are among the most frequently asked topics in Java backend interviews.

---

## 🚀 Next Chapter

**Chapter 7 – Spring REST API & RESTful Web Services**
