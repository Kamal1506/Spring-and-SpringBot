# 📘 REST Controllers & HTTP Methods Interview Handbook

**Interview Importance:** High

REST Controllers and HTTP methods are among the most frequently discussed topics in Spring Boot interviews. Interviewers expect candidates to understand how REST APIs are created, how HTTP methods work, and how Spring Boot processes requests and responses.

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand the purpose of a REST Controller.
- Differentiate `@Controller` and `@RestController`.
- Explain the purpose of `@ResponseBody`.
- Use `@RequestMapping` and specialized mapping annotations.
- Understand all common HTTP methods.
- Choose the correct HTTP method for CRUD operations.
- Explain serialization and deserialization.
- Understand how Spring Boot converts Java objects into JSON.
- Answer scenario-based REST API interview questions.

---

# 📚 Topics Covered

- REST Controller
- `@Controller` vs `@RestController`
- `@ResponseBody`
- `@RequestMapping`
- HTTP Methods
- GET
- POST
- PUT
- PATCH
- DELETE
- CRUD Mapping
- JSON
- Serialization
- Deserialization
- `@RequestBody`
- HTTP Status Codes
- Internal Request Flow
- Scenario-Based Questions

---

# ❓ Interview Questions & Answers

---

# Part 1 – REST Controllers

---

## Question 1. What is a REST Controller?

**Interview Importance:** High

### Interview Answer

A REST Controller is a Spring component used to create RESTful web services. It handles HTTP requests and returns data directly as **JSON** or **XML** instead of rendering a view.

It is created using the `@RestController` annotation.

### Example

```java
@RestController
@RequestMapping("/employees")
public class EmployeeController {

    @GetMapping
    public List<Employee> getEmployees() {
        return employeeService.getAllEmployees();
    }
}
```

### Internal Working

```
Client
   │
   ▼
DispatcherServlet
   │
   ▼
@RestController
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
JSON Response
```

### Real-Time Example

```http
GET /employees
```

Response

```json
[
  {
    "id": 1,
    "name": "Kamal"
  }
]
```

---

## Question 2. Difference between `@Controller` and `@RestController`

**Interview Importance:** High

| `@Controller` | `@RestController` |
|---------------|-------------------|
| Returns View (JSP/HTML/Thymeleaf) | Returns JSON/XML |
| Used for MVC applications | Used for REST APIs |
| Needs `@ResponseBody` to return JSON | Automatically applies `@ResponseBody` |
| Mainly frontend rendering | Mainly backend APIs |

### Interview Answer

`@RestController` is a combination of `@Controller` and `@ResponseBody`. It is specifically designed for REST APIs because it automatically serializes Java objects into JSON or XML.

---

## Question 3. What is `@ResponseBody`?

**Interview Importance:** Medium

### Interview Answer

`@ResponseBody` tells Spring to write the method's return value directly into the HTTP response body instead of resolving it as a view.

`@RestController` already includes this behavior automatically.

---

## Question 4. What is `@RequestMapping`?

**Interview Importance:** High

### Interview Answer

`@RequestMapping` maps HTTP requests to a controller or a specific handler method.

It can be used at:

- Class level
- Method level

### Example

```java
@RequestMapping("/employees")
```

---

## Question 5. Difference between `@RequestMapping` and `@GetMapping`

**Interview Importance:** Medium

| `@RequestMapping` | `@GetMapping` |
|-------------------|---------------|
| Generic mapping | GET only |
| Supports all HTTP methods | Supports only GET |
| More configuration | Cleaner and shorter |

### Interview Answer

`@RequestMapping` is a generic annotation used for mapping requests, whereas `@GetMapping` is a specialized shortcut designed specifically for GET requests.

---

# Part 2 – HTTP Methods

---

## Question 6. What are HTTP methods?

**Interview Importance:** High

### Interview Answer

HTTP methods define the type of operation a client wants to perform on a resource.

Common methods are:

- GET
- POST
- PUT
- PATCH
- DELETE

---

## Question 7. Explain the GET method.

**Interview Importance:** High

### Interview Answer

GET retrieves data from the server.

### Characteristics

- Read-only
- Safe
- Idempotent
- Typically has no request body

### Example

```http
GET /employees/1
```

### Real-Time Example

```http
GET /products
```

Retrieves all products from an e-commerce application.

---

## Question 8. Explain the POST method.

**Interview Importance:** High

### Interview Answer

POST creates a new resource.

### Example

```http
POST /employees
```

Request Body

```json
{
  "name": "Kamal"
}
```

Recommended Response

```http
201 Created
```

---

## Question 9. Explain the PUT method.

**Interview Importance:** High

### Interview Answer

PUT replaces the entire existing resource.

### Example

```http
PUT /employees/1
```

The complete employee object is replaced with the new data.

---

## Question 10. Explain PATCH.

**Interview Importance:** Medium

### Interview Answer

PATCH updates only selected fields of a resource.

### Example

Current Employee

```json
{
  "name": "Kamal",
  "salary": 50000
}
```

PATCH Request

```json
{
  "salary": 60000
}
```

Only the salary is updated.

---

## Question 11. Difference between PUT and PATCH

**Interview Importance:** High

| PUT | PATCH |
|------|--------|
| Replaces entire resource | Updates selected fields |
| Sends full object | Sends only modified fields |
| Idempotent | Usually idempotent, depending on implementation |

### Interview Answer

PUT replaces the complete resource, whereas PATCH updates only the specified fields.

---

## Question 12. Explain DELETE.

**Interview Importance:** High

### Interview Answer

DELETE removes a resource from the server.

### Example

```http
DELETE /employees/5
```

Recommended Response

```http
204 No Content
```

---

# Part 3 – REST API Design

---

## Question 13. Why should URLs use nouns instead of verbs?

**Interview Importance:** Medium

### Interview Answer

REST resources represent objects rather than actions.

Correct

```http
GET /employees
```

Incorrect

```http
GET /getEmployees
```

The HTTP method already represents the action.

---

## Question 14. Which HTTP method should be used for CRUD?

**Interview Importance:** High

| CRUD Operation | HTTP Method |
|---------------|-------------|
| Create | POST |
| Read | GET |
| Update | PUT / PATCH |
| Delete | DELETE |

---

## Question 15. Why shouldn't GET modify data?

**Interview Importance:** Medium

### Interview Answer

GET is intended only for retrieving data.

Modifying data through GET violates REST principles and may lead to unexpected behavior because browsers, caches, and proxies can automatically repeat or cache GET requests.

---

# Part 4 – JSON & Request/Response Handling

---

## Question 16. What is JSON?

**Interview Importance:** Medium

### Interview Answer

JSON (JavaScript Object Notation) is a lightweight, text-based format used for exchanging data between client and server.

### Example

```json
{
  "id": 1,
  "name": "Kamal"
}
```

---

## Question 17. How does Spring convert Java objects into JSON?

**Interview Importance:** High

### Interview Answer

Spring Boot uses the **Jackson** library through **HttpMessageConverter** to automatically serialize Java objects into JSON.

### Flow

```
Java Object
      │
      ▼
Jackson
      │
      ▼
JSON
      │
      ▼
Client
```

---

## Question 18. What is Serialization?

**Interview Importance:** Medium

### Interview Answer

Serialization is the process of converting a Java object into JSON or XML before sending it to the client.

---

## Question 19. What is Deserialization?

**Interview Importance:** Medium

### Interview Answer

Deserialization is the process of converting JSON or XML received from the client into a Java object.

---

## Question 20. What is `@RequestBody`?

**Interview Importance:** High

### Interview Answer

`@RequestBody` binds the JSON request body to a Java object.

### Example

```java
@PostMapping
public Employee create(@RequestBody Employee employee) {
    return employeeService.save(employee);
}
```

---

## Question 21. What is `@ResponseBody` used for?

### Interview Answer

It tells Spring to write the method's return value directly into the HTTP response body instead of rendering a view.

---

## Question 22. Which status code should be returned after creating a resource?

### Interview Answer

```http
201 Created
```

---

## Question 23. Which status code is recommended after a successful DELETE?

### Interview Answer

```http
204 No Content
```

---

## Question 24. What happens internally when `GET /employees` is called?

**Interview Importance:** High

### Interview Answer

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
EmployeeController
   │
   ▼
EmployeeService
   │
   ▼
EmployeeRepository
   │
   ▼
Database
   │
   ▼
Employee Objects
   │
   ▼
Jackson Serialization
   │
   ▼
JSON Response
   │
   ▼
Client
```

---

# Part 5 – Scenario-Based Questions

---

## Question 25

A client wants to update only an employee's salary.

Which HTTP method would you choose?

### Answer

**PATCH**, because only a specific field needs to be updated.

---

## Question 26

Why is `@RestController` preferred over `@Controller` for REST APIs?

### Answer

Because `@RestController` automatically returns data as JSON or XML and removes the need to annotate every method with `@ResponseBody`.

---

## Question 27

Your API returns HTML instead of JSON.

What could be the reason?

### Answer

Possible reasons include:

- Using `@Controller` instead of `@RestController`
- Missing `@ResponseBody`
- Incorrect content negotiation or request mapping configuration

---

# Part 6 – Real-Time Interview Questions

---

## Question 28

Why do companies prefer REST APIs?

### Interview Answer

REST APIs are preferred because they are:

- Lightweight
- Stateless
- Scalable
- Easy to integrate
- Platform independent
- Suitable for web, mobile, and third-party applications

---

## Question 29

Why does Spring Boot automatically return JSON?

### Interview Answer

Because `spring-boot-starter-web` includes the Jackson library, and Spring Boot automatically configures an **HttpMessageConverter** that serializes Java objects into JSON.

---

# 💡 Key Interview Tips

- Remember that `@RestController` = `@Controller` + `@ResponseBody`.
- Know when to use **GET**, **POST**, **PUT**, **PATCH**, and **DELETE**.
- Understand which HTTP status codes should be returned for common operations.
- Be able to explain serialization and deserialization.
- Understand how Jackson converts Java objects into JSON.
- Practice explaining the complete request flow from **Client → DispatcherServlet → Controller → Service → Repository → Database → JSON Response**.

---

# 📝 Chapter Summary

In this chapter, you learned:

- REST Controllers
- `@Controller` vs `@RestController`
- `@ResponseBody`
- `@RequestMapping`
- HTTP Methods
- GET
- POST
- PUT
- PATCH
- DELETE
- CRUD Mapping
- JSON
- Serialization
- Deserialization
- `@RequestBody`
- HTTP Status Codes
- Internal Request Flow
- Scenario-Based Questions
- Real-Time Interview Questions

These concepts are essential for building RESTful APIs with Spring Boot and are among the most commonly assessed topics in Java backend interviews.

---

## 🚀 Next Chapter

**Chapter 10 – Request Mapping, Path Variables & Request Parameters**
