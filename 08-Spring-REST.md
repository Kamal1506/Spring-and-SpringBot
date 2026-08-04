# 📘 Spring REST using Spring Boot 3 Interview Handbook

> **Chapter 8: Spring REST using Spring Boot 3**

**Interview Importance:** ⭐⭐⭐⭐⭐ (Extremely High)

REST APIs are the foundation of modern backend development. Almost every Spring Boot application exposes RESTful web services, making this one of the most frequently asked topics in Java backend interviews.

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand REST and REST APIs.
- Explain the principles of REST.
- Understand why REST is stateless.
- Differentiate REST and SOAP.
- Explain why JSON is preferred over XML.
- Build REST APIs using Spring Boot.
- Understand the role of `spring-boot-starter-web`.
- Explain the responsibilities of `DispatcherServlet`.
- Describe the complete request lifecycle of a REST API.
- Answer real-world Spring REST interview questions confidently.

---

# 📚 Topics Covered

- REST
- REST API
- REST Principles
- Stateless Communication
- REST vs SOAP
- JSON vs XML
- Spring REST
- Spring Boot
- Auto Configuration
- Embedded Tomcat
- `spring-boot-starter-web`
- DispatcherServlet
- REST Request Flow
- Real-Time Interview Questions

---

# ❓ Interview Questions & Answers

---

# Part 1 – Introduction to Spring REST & Spring Boot 3

---

## Question 1. What is REST?

### ⭐⭐⭐⭐⭐ Interview Definition

REST (Representational State Transfer) is an architectural style used to build web services that communicate over HTTP. It treats everything as a resource, identified by a URI, and uses standard HTTP methods such as **GET**, **POST**, **PUT**, and **DELETE** to perform operations.

### Example

```http
GET /employees/1
```

Retrieves employee details.

### 💡 Real-World Examples

**Amazon**

```http
GET /products
```

Fetch all products.

**Flipkart**

```http
POST /orders
```

Create a new order.

---

## Question 2. What is a REST API?

### ⭐⭐⭐⭐⭐ Interview Definition

A REST API is a web service that follows REST principles and allows clients and servers to exchange data, typically in **JSON** format, over HTTP.

### Architecture

```
React Application
        │
        ▼
    REST API
        │
        ▼
   Spring Boot
        │
        ▼
    Database
```

---

## Question 3. What are the principles of REST?

### ⭐⭐⭐⭐⭐ Interview Answer

REST follows six architectural constraints:

- Client-Server Architecture
- Stateless Communication
- Cacheable Responses
- Uniform Interface
- Layered System
- HATEOAS *(optional in many real-world APIs but part of REST constraints)*

---

## Question 4. Why is REST Stateless?

### ⭐⭐⭐⭐⭐ Interview Answer

REST is stateless because the server does not store client session information.

Every request must contain all the required information, such as authentication credentials or a JWT token.

### Advantages

- Better scalability
- Better performance
- Easier load balancing
- Simpler server design

---

## Question 5. Difference between REST and SOAP

| REST | SOAP |
|------|------|
| Architectural style | Protocol |
| Lightweight | Heavyweight |
| Mostly JSON | XML only |
| Faster | Slower |
| Easier to develop | More complex |

---

## Question 6. Why is JSON preferred over XML?

### Interview Answer

JSON is preferred because it offers:

- Smaller payload
- Faster parsing
- Human-readable format
- Better JavaScript support
- Lower bandwidth usage

---

## Question 7. What is Spring REST?

### Interview Definition

Spring REST is Spring's support for building RESTful web services using annotations such as:

- `@RestController`
- `@GetMapping`
- `@PostMapping`
- `@PutMapping`
- `@DeleteMapping`

Spring automatically converts Java objects into JSON using **Jackson**.

---

## Question 8. What is Spring Boot?

### Interview Definition

Spring Boot is an extension of the Spring Framework that simplifies application development by providing:

- Auto Configuration
- Embedded Servers
- Starter Dependencies
- Production-ready Features

---

## Question 9. Why do we use Spring Boot for REST APIs?

### Interview Answer

Spring Boot is preferred because it provides:

- Embedded Tomcat
- Auto Configuration
- Starter Dependencies
- Faster Development
- Minimal Configuration
- Production-ready features such as Actuator

---

## Question 10. What is Auto Configuration?

### Interview Definition

Auto Configuration automatically configures Spring Beans based on the dependencies available in the project.

### Example

Adding:

```xml
spring-boot-starter-web
```

Automatically configures:

- Embedded Tomcat
- DispatcherServlet
- Jackson
- Spring MVC

without manual setup.

---

## Question 11. What is Embedded Tomcat?

### Interview Answer

Spring Boot packages Tomcat inside the application, eliminating the need to install or configure an external web server.

### Startup Flow

```
main()
    │
    ▼
SpringApplication.run()
    │
    ▼
Embedded Tomcat Starts
    │
    ▼
Application Ready
```

---

## Question 12. Why is Spring Boot faster than traditional Spring?

### Interview Answer

Because it provides:

- Auto Configuration
- Starter Dependencies
- Embedded Server
- No XML Configuration
- Convention over Configuration

These features significantly reduce development time.

---

## Question 13. What is `spring-boot-starter-web`?

### Interview Definition

`spring-boot-starter-web` is a starter dependency that contains everything required to build RESTful web applications.

### It includes

- Spring MVC
- Embedded Tomcat
- Jackson
- Validation Support
- REST Support

---

## Question 14. What is DispatcherServlet?

### ⭐⭐⭐⭐⭐ Interview Definition

DispatcherServlet is the **Front Controller** of Spring MVC.

Every HTTP request first reaches DispatcherServlet, which forwards it to the appropriate controller.

### Request Flow

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
```

### Easy Way to Remember

Think of DispatcherServlet as the **receptionist** of a company.

Every visitor first meets the receptionist, who directs them to the correct department.

---

## Question 15. What happens internally when a REST request is received?

### ⭐⭐⭐⭐⭐ Interview Answer

```
Client
   │
   ▼
DispatcherServlet
   │
   ▼
Handler Mapping
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

### Explanation

1. The client sends an HTTP request.
2. DispatcherServlet receives the request.
3. Handler Mapping identifies the correct controller.
4. The controller delegates business logic to the service layer.
5. The service communicates with the repository.
6. The repository interacts with the database.
7. The response travels back through the repository, service, and controller.
8. DispatcherServlet returns the final JSON response to the client.

---

# 💼 Real-Time Interview Questions

## Why did you choose Spring Boot instead of plain Spring?

### Sample Answer

> I chose Spring Boot because it reduces boilerplate configuration through Auto Configuration, Starter Dependencies, and an Embedded Server. It allowed me to develop REST APIs much faster while still using all the features of the Spring Framework.

---

## Why do modern applications prefer REST APIs?

### Expected Answer

REST APIs are preferred because they:

- Are lightweight
- Use standard HTTP methods
- Commonly exchange JSON data
- Are easy to integrate with frontend and mobile applications
- Are scalable and stateless

---

## Why is JSON used in REST APIs?

### Expected Answer

Because JSON:

- Is lightweight
- Is easy to read and write
- Is parsed efficiently
- Integrates naturally with JavaScript
- Consumes less bandwidth than XML

---

# 🧠 Scenario-Based Questions

---

## Scenario 1

### A React frontend needs employee data.

Which HTTP method should you use?

**Answer**

```http
GET /employees
```

Because **GET** is used to retrieve data.

---

## Scenario 2

### A user submits a registration form.

Which HTTP method should you use?

**Answer**

```http
POST /users
```

Because **POST** is used to create new resources.

---

## Scenario 3

### You need to update an employee's salary.

Which HTTP method should you use?

**Answer**

```http
PUT /employees/{id}
```

(or **PATCH** if performing a partial update)

---

## Scenario 4

### You need to remove a product.

Which HTTP method should you use?

**Answer**

```http
DELETE /products/{id}
```

Because **DELETE** is used to remove resources.

---

# ⚖️ Frequently Asked Differences

## REST vs SOAP

| REST | SOAP |
|------|------|
| Architectural style | Protocol |
| Lightweight | Heavyweight |
| Usually JSON | XML only |
| Faster | Slower |
| Easier to develop | More complex |

---

## JSON vs XML

| JSON | XML |
|------|-----|
| Lightweight | More verbose |
| Faster parsing | Slower parsing |
| Easy to read | More complex structure |
| Native JavaScript support | Less convenient for JavaScript |

---

## Spring Framework vs Spring Boot

| Spring Framework | Spring Boot |
|------------------|-------------|
| Requires more configuration | Auto Configuration |
| External server | Embedded Server |
| More setup | Faster development |

---

## Spring MVC vs Spring REST

| Spring MVC | Spring REST |
|------------|-------------|
| Returns Views (JSP/Thymeleaf) | Returns JSON/XML |
| Used for web applications | Used for REST APIs |
| Often uses `@Controller` | Uses `@RestController` |

---

# 💡 Key Interview Tips

- Remember that **REST is an architectural style, not a protocol**.
- Know all common HTTP methods: **GET, POST, PUT, PATCH, DELETE**.
- Understand why REST is **stateless**.
- Be able to explain the complete request flow from **Client → DispatcherServlet → Controller → Service → Repository → Database**.
- Understand the role of **Jackson** in converting Java objects to JSON.
- Use examples from your own Spring Boot projects when explaining REST APIs.

---

# 📝 Chapter Summary

In this chapter, you learned:

- REST
- REST API
- REST Principles
- Stateless Communication
- REST vs SOAP
- JSON vs XML
- Spring REST
- Spring Boot
- Auto Configuration
- Embedded Tomcat
- `spring-boot-starter-web`
- DispatcherServlet
- REST Request Flow
- Real-world Interview Questions
- Scenario-Based Questions
- Frequently Asked Differences

These concepts form the foundation of modern backend API development and are among the most frequently asked topics in Spring Boot interviews.

---

## 🚀 Next Chapter

**Chapter 9 – REST Controllers, HTTP Methods & Request Mapping**
