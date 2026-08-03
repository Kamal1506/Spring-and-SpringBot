# 📘 Spring MVC & ORM Interview Handbook

> **Chapter 5: Spring MVC & ORM**

This chapter covers **Spring MVC**, one of the core modules of the Spring Framework, along with **ORM, JPA, Hibernate, and Spring Data JPA**. These topics are fundamental for building web applications and REST APIs and are among the most frequently asked questions in Spring Boot interviews.

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand the Spring MVC architecture.
- Explain the responsibilities of Model, View, and Controller.
- Understand the role of DispatcherServlet.
- Explain the complete Spring MVC request flow.
- Learn form handling and validation.
- Understand exception handling in Spring MVC.
- Learn ORM concepts.
- Differentiate JPA, Hibernate, and Spring Data JPA.
- Understand Entities, Repositories, and CRUD operations.
- Answer common Spring MVC interview questions confidently.

---

# 📚 Topics Covered

## Spring MVC

- Spring MVC
- MVC Architecture
- Model
- View
- Controller
- DispatcherServlet
- Front Controller Pattern
- Spring MVC Request Flow
- Form Handling
- Validation
- Exception Handling

## ORM & Spring Data JPA

- ORM
- Hibernate
- JPA
- Spring Data JPA
- Entity
- Repository
- Query Methods
- CRUD Operations
- Common Differences
- Scenario-Based Questions

---

# ❓ Interview Questions & Answers

---

# Part 1 – Spring MVC

---

## Question 1. What is Spring MVC?

### ⭐ Interview Definition

Spring MVC is a web framework in the Spring Framework that follows the **Model-View-Controller (MVC)** design pattern to build web applications and REST APIs.

### Simple Answer

Spring MVC separates an application into three layers:

- Model
- View
- Controller

Each layer has a specific responsibility, making applications easier to develop and maintain.

### 💡 Real-World Example

Imagine an online shopping website.

```
Customer clicks "Buy Product"
            │
            ▼
      Controller
            │
            ▼
        Service
            │
            ▼
        Database
            │
            ▼
      Controller
            │
            ▼
      Response to User
```

---

## Question 2. What is MVC?

### Definition

MVC stands for:

- **Model**
- **View**
- **Controller**

It is a design pattern used to separate application logic into different layers.

---

## Question 3. Explain MVC Architecture.

### Architecture Flow

```
Client
   │
   ▼
Controller
   │
   ▼
Service
   │
   ▼
Repository
   │
   ▼
Database
   │
   ▼
Repository
   │
   ▼
Service
   │
   ▼
Controller
   │
   ▼
View / JSON Response
   │
   ▼
Client
```

This layered architecture is used in most Spring Boot applications.

---

## Question 4. What is Model?

### Definition

The **Model** represents the application's data and business information.

### Example

```java
public class Student {

    private int id;
    private String name;

}
```

The Model stores application data.

---

## Question 5. What is View?

### Definition

The **View** is responsible for displaying data to the user.

### Examples

- JSP
- Thymeleaf
- HTML

For REST APIs, the **JSON response** acts as the View.

---

## Question 6. What is Controller?

### Definition

A **Controller** receives HTTP requests, delegates business logic to the service layer, and returns a view or response.

### Example

```java
@RestController
@RequestMapping("/students")
public class StudentController {

}
```

### Responsibilities

- Receive HTTP Requests
- Call Service Layer
- Return Response

---

## Question 7. What is DispatcherServlet?

### ⭐ Very Important Interview Question

### Definition

DispatcherServlet is the **Front Controller** of Spring MVC.

Every incoming HTTP request first reaches the DispatcherServlet.

### Flow

```
Browser
   │
   ▼
DispatcherServlet
   │
   ▼
Controller
   │
   ▼
Service
   │
   ▼
Repository
   │
   ▼
Database
```

### 💡 Easy Way to Remember

Think of DispatcherServlet as a **receptionist**.

Every visitor first meets the receptionist, who directs them to the correct department.

---

## Question 8. Why is DispatcherServlet called the Front Controller?

### Answer

Because it is the **single entry point** for all incoming HTTP requests in a Spring MVC application.

It receives every request and forwards it to the appropriate controller.

---

## Question 9. Explain the Spring MVC Request Flow.

### ⭐ Most Asked Interview Question

```
Client
   │
   ▼
DispatcherServlet
   │
   ▼
Controller
   │
   ▼
Service
   │
   ▼
Repository
   │
   ▼
Database
   │
   ▼
Repository
   │
   ▼
Service
   │
   ▼
Controller
   │
   ▼
DispatcherServlet
   │
   ▼
Client
```

### Interview Answer

> The client sends an HTTP request to the DispatcherServlet. The DispatcherServlet identifies the appropriate controller and forwards the request. The controller delegates business logic to the service layer, which interacts with the repository to access the database. The result flows back through the service and controller, and the DispatcherServlet returns the final response to the client.

---

## Question 10. What is Form Handling?

### Definition

Form Handling is the process of receiving, validating, and processing user input submitted through forms.

### Example

```
Registration Form
      │
      ▼
Controller
      │
      ▼
Database
```

---

## Question 11. What is Validation?

### Definition

Validation ensures that user input satisfies predefined rules before processing.

### Examples

- Email is required
- Password minimum length
- Age must be greater than 18

### Spring Validation

```java
@Valid
```

### Common Validation Annotations

- `@NotNull`
- `@NotBlank`
- `@Size`
- `@Email`
- `@Min`
- `@Max`

---

## Question 12. What is Exception Handling?

### Definition

Exception Handling allows applications to respond gracefully to errors instead of failing unexpectedly.

### Common Annotations

```java
@ControllerAdvice
```

or

```java
@ExceptionHandler
```

### Example

User requests:

```
Student ID = 500
```

No record exists.

Instead of returning an unexpected exception, the application returns:

```
Student Not Found
```

---

# Part 2 – ORM

---

## Question 13. What is ORM?

### ⭐ Interview Definition

ORM (Object Relational Mapping) is a technique that maps Java objects to database tables and database records back to Java objects.

### Simple Answer

ORM allows developers to work with Java objects instead of writing SQL for every database operation.

### Real-Time Example

```
Java Object
(Student)
     │
     ▼
ORM
     │
     ▼
Database Table
(student)
```

---

## Question 14. Why do we use ORM?

### Without ORM

- Create Connection
- Write SQL
- Use PreparedStatement
- Process ResultSet

Lots of manual code.

### With ORM

```java
studentRepository.save(student);
```

Much simpler and more maintainable.

---

## Question 15. What is Hibernate?

### Definition

Hibernate is a popular ORM framework that implements JPA.

### Responsibilities

- Generate SQL
- Map Objects
- Perform CRUD Operations
- Manage Database Interaction

---

## Question 16. What is JPA?

### Definition

JPA (Jakarta Persistence API) is a **specification** that defines how ORM should work in Java.

It is **not an implementation**.

### Easy Way to Remember

```
JPA
  │
Rules / Specification

Hibernate
  │
Implementation
```

---

## Question 17. Difference between JPA and Hibernate

| JPA | Hibernate |
|-----|-----------|
| Specification | Implementation |
| Defines rules | Implements rules |
| Cannot be used directly | Can be used directly |

---

## Question 18. What is Spring Data JPA?

### Definition

Spring Data JPA simplifies database access by providing repository interfaces with built-in CRUD operations.

### Example

```java
public interface StudentRepository
extends JpaRepository<Student, Integer> {

}
```

No implementation code is required.

---

## Question 19. What is an Entity?

### Definition

An Entity is a Java class mapped to a database table.

### Example

```java
@Entity
public class Student {

}
```

### Interview Tip

Every Entity usually represents one database table.

---

## Question 20. What is Repository?

### Definition

Repository is the Data Access Layer responsible for interacting with the database.

### Example

```java
@Repository
public interface StudentRepository
extends JpaRepository<Student, Integer> {

}
```

### Responsibilities

- Save
- Update
- Delete
- Find

---

## Question 21. What are Query Methods?

Spring Data JPA automatically generates SQL queries from repository method names.

### Examples

```java
findByName()

findByEmail()

findByAgeGreaterThan()
```

No SQL needs to be written manually.

---

## Question 22. What is CRUD?

CRUD stands for:

- **Create**
- **Read**
- **Update**
- **Delete**

### Common Methods

```java
save()

findById()

findAll()

delete()
```

---

# 💼 Real-Time Interview Questions

## Explain MVC using your project.

### Sample Answer

> In my Student Management project, the `StudentController` receives HTTP requests from the frontend. It calls the `StudentService`, which contains the business logic. The service interacts with `StudentRepository`, which uses Spring Data JPA and Hibernate to communicate with the MySQL database. Finally, the controller returns JSON responses to the React frontend.

---

## Why use ORM instead of JDBC?

### Expected Answer

Because ORM:

- Reduces boilerplate code.
- Automatically maps objects to database tables.
- Improves developer productivity.
- Is easier to maintain.
- Integrates seamlessly with Spring.

---

## Why use Hibernate?

### Expected Answer

Because Hibernate:

- Implements JPA.
- Automatically generates SQL.
- Simplifies CRUD operations.
- Supports caching and lazy loading.
- Reduces manual database code.

---

# 🧠 Scenario-Based Questions

## Scenario 1

### You need to insert a student.

**Without ORM**

Write SQL manually.

**With ORM**

```java
studentRepository.save(student);
```

---

## Scenario 2

### You want all students.

```java
findAll();
```

No SQL is required.

---

## Scenario 3

### A user submits an invalid email.

What should happen?

**Answer**

Validation should fail, and the application should return an appropriate validation error instead of saving invalid data.

---

# ⚖️ Frequently Asked Differences

## MVC vs ORM

| MVC | ORM |
|------|-----|
| Web architecture | Database mapping technique |
| Handles requests and responses | Maps Java objects to database tables |

---

## JPA vs Hibernate

| JPA | Hibernate |
|-----|-----------|
| Specification | Implementation |

---

## Entity vs Table

| Entity | Table |
|--------|-------|
| Java Class | Database Table |

---

## Controller vs Service

| Controller | Service |
|------------|---------|
| Handles HTTP requests | Contains business logic |

---

## Repository vs Service

| Repository | Service |
|------------|---------|
| Database access | Business logic |

---

# 💡 Key Interview Tips

- Understand the complete Spring MVC request flow.
- Remember that **DispatcherServlet is the Front Controller**.
- Know the responsibilities of **Controller, Service, Repository, and Entity**.
- Be able to clearly differentiate **JPA**, **Hibernate**, and **Spring Data JPA**.
- Use real project examples when explaining MVC architecture.
- Practice common differences such as MVC vs ORM and Controller vs Service.

---

# 📝 Chapter Summary

In this chapter, you learned:

- Spring MVC
- MVC Architecture
- DispatcherServlet
- Request Processing Flow
- Form Handling
- Validation
- Exception Handling
- ORM
- Hibernate
- JPA
- Spring Data JPA
- Entity
- Repository
- Query Methods
- CRUD Operations
- Common Interview Differences
- Scenario-Based Questions

These concepts are essential for developing Spring Boot applications and are among the most frequently asked topics in Java backend interviews.

---

## 🚀 Next Chapter

**Chapter 6 – Spring AOP (Aspect-Oriented Programming)**
