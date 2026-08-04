# 📘 Request & Response Handling Interview Handbook

> **Chapter 10: Request & Response Handling**

**Interview Importance:** High

Request and response handling is one of the most commonly tested topics in Spring Boot interviews. Interviewers expect candidates to understand how data is received from clients, processed by the application, and returned with appropriate HTTP responses and status codes.

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand the purpose of `@PathVariable` and `@RequestParam`.
- Differentiate path variables and query parameters.
- Bind JSON request bodies using `@RequestBody`.
- Understand how Spring converts JSON into Java objects.
- Return custom HTTP responses using `ResponseEntity`.
- Work with HTTP status codes and response headers.
- Handle exceptions using `@ExceptionHandler` and `@ControllerAdvice`.
- Explain the complete request and response lifecycle.

---

# 📚 Topics Covered

- Path Variables
- Query Parameters
- `@PathVariable`
- `@RequestParam`
- `@RequestBody`
- Request Processing
- Form Data vs JSON
- `ResponseEntity`
- HTTP Status Codes
- HTTP Headers
- Exception Handling
- `@ExceptionHandler`
- `@ControllerAdvice`
- Global Exception Handling
- Request Lifecycle
- Scenario-Based Questions

---

# ❓ Interview Questions & Answers

---

# Part 1 – Path Variables & Query Parameters

---

## Question 1. What is `@PathVariable`?

**Interview Importance:** High

### Interview Answer

`@PathVariable` is used to extract values from the URI path.

### Example

```java
@GetMapping("/employees/{id}")
public Employee getEmployee(@PathVariable Long id) {
    return service.getEmployee(id);
}
```

### Request

```http
GET /employees/10
```

Here,

```
id = 10
```

---

## Question 2. What is `@RequestParam`?

**Interview Importance:** High

### Interview Answer

`@RequestParam` is used to retrieve query parameters from the URL.

### Example

```java
@GetMapping("/employees")
public List<Employee> getEmployees(
        @RequestParam String department) {
}
```

### Request

```http
GET /employees?department=IT
```

```
department = IT
```

---

## Question 3. Difference between `@PathVariable` and `@RequestParam`

**Interview Importance:** High

| `@PathVariable` | `@RequestParam` |
|-----------------|-----------------|
| URI path | Query string |
| Used to identify a specific resource | Used for filtering, searching, sorting, or pagination |
| `/employees/10` | `/employees?id=10` |

### Real-Time Example

Retrieve a specific product:

```http
GET /products/25
```

Filter products:

```http
GET /products?category=Mobile
```

---

## Question 4. When do you use `@PathVariable`?

### Interview Answer

Use `@PathVariable` when identifying a specific resource.

### Example

```http
GET /employees/100
```

---

## Question 5. When do you use `@RequestParam`?

### Interview Answer

Use `@RequestParam` for:

- Filtering
- Searching
- Sorting
- Pagination

### Example

```http
GET /employees?page=2&size=10
```

---

# Part 2 – Request Body

---

## Question 6. What is `@RequestBody`?

**Interview Importance:** High

### Interview Answer

`@RequestBody` binds the JSON request body to a Java object.

### Example

```java
@PostMapping
public Employee save(@RequestBody Employee employee) {
}
```

### JSON Request

```json
{
  "name": "Kamal",
  "salary": 50000
}
```

### Conversion

```
JSON
   │
   ▼
Java Object
```

---

## Question 7. What happens internally when `@RequestBody` is used?

### Interview Answer

```
JSON
   │
   ▼
HttpMessageConverter
   │
   ▼
Jackson
   │
   ▼
Java Object
   │
   ▼
Controller
```

---

## Question 8. Difference between JSON Request Body and Form Data

| JSON Request Body | Form Data |
|-------------------|-----------|
| Used in REST APIs | Used in HTML forms |
| `@RequestBody` | `@RequestParam` |
| `application/json` | `application/x-www-form-urlencoded` |

---

# Part 3 – Response Handling

---

## Question 9. What is `ResponseEntity`?

**Interview Importance:** High

### Interview Answer

`ResponseEntity` represents the complete HTTP response, including:

- Status Code
- Headers
- Response Body

### Example

```java
return ResponseEntity.ok(employee);
```

---

## Question 10. Why use `ResponseEntity` instead of returning an object directly?

### Interview Answer

`ResponseEntity` provides full control over:

- HTTP status codes
- Response headers
- Response body

---

## Question 11. How do you return **201 Created**?

### Example

```java
return ResponseEntity
        .status(HttpStatus.CREATED)
        .body(employee);
```

---

## Question 12. How do you return **404 Not Found**?

### Example

```java
return ResponseEntity
        .notFound()
        .build();
```

---

## Question 13. Common HTTP Status Codes

**Interview Importance:** High

| Status Code | Meaning |
|-------------|---------|
| 200 | OK |
| 201 | Created |
| 204 | No Content |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 405 | Method Not Allowed |
| 409 | Conflict |
| 500 | Internal Server Error |

---

# Part 4 – Response Headers

---

## Question 14. What are HTTP Headers?

### Interview Answer

HTTP headers contain additional information about a request or response.

### Common Examples

- `Content-Type`
- `Authorization`
- `Accept`
- `Cache-Control`

---

## Question 15. How do you add custom headers?

### Example

```java
return ResponseEntity.ok()
        .header("Company", "ABC")
        .body(employee);
```

---

# Part 5 – Exception Handling

---

## Question 16. Why is Exception Handling important?

**Interview Importance:** High

### Interview Answer

Without proper exception handling:

```
Database Error
      │
      ▼
500 Internal Server Error
      │
      ▼
Poor User Experience
```

Proper exception handling provides meaningful error responses and improves application reliability.

---

## Question 17. What is `@ExceptionHandler`?

### Interview Answer

`@ExceptionHandler` handles exceptions thrown by controller methods.

### Example

```java
@ExceptionHandler(EmployeeNotFoundException.class)
```

---

## Question 18. What is `@ControllerAdvice`?

**Interview Importance:** High

### Interview Answer

`@ControllerAdvice` provides centralized exception handling across all controllers.

Instead of writing exception handling logic in every controller, one global class handles exceptions for the entire application.

---

## Question 19. Difference between `@ExceptionHandler` and `@ControllerAdvice`

| `@ExceptionHandler` | `@ControllerAdvice` |
|---------------------|---------------------|
| Handles specific exceptions | Provides centralized exception handling |
| Controller-specific | Application-wide |

---

## Question 20. What is a Global Exception Handler?

### Interview Answer

A global exception handler catches exceptions from all controllers and returns consistent, standardized error responses throughout the application.

---

# Part 6 – Common HTTP Error Responses

---

## Question 21. What response should be returned if a resource is not found?

### Answer

```http
404 Not Found
```

---

## Question 22. What response should be returned for an invalid request body?

### Answer

```http
400 Bad Request
```

---

## Question 23. What response should be returned for an unauthorized user?

### Answer

```http
401 Unauthorized
```

---

## Question 24. What response should be returned when the user is authenticated but lacks permission?

### Answer

```http
403 Forbidden
```

---

## Question 25. What response should be returned for an internal server failure?

### Answer

```http
500 Internal Server Error
```

---

# Part 7 – Internal Request Processing

---

## Question 26. Explain request processing in Spring Boot.

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
Controller
   │
   ▼
@RequestBody
   │
   ▼
Jackson
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

### Explanation

1. The client sends an HTTP request.
2. `DispatcherServlet` receives the request.
3. Handler Mapping identifies the correct controller.
4. Spring converts the JSON request into a Java object using Jackson.
5. The controller delegates processing to the service layer.
6. The service communicates with the repository.
7. The repository interacts with the database.
8. The response object is converted into JSON.
9. The client receives the final HTTP response.

---

# Part 8 – Scenario-Based Questions

---

## Question 27

A client sends:

```http
GET /employees/15
```

Which annotation should you use?

### Answer

`@PathVariable`

---

## Question 28

A client sends:

```http
GET /employees?page=2
```

Which annotation should you use?

### Answer

`@RequestParam`

---

## Question 29

A client sends a JSON request body.

Which annotation should you use?

### Answer

`@RequestBody`

---

## Question 30

Why should you use `ResponseEntity`?

### Answer

Because it allows you to customize:

- HTTP status code
- Response headers
- Response body

---

## Question 31

A database exception occurs.

Where should you handle it?

### Answer

Using a global exception handler with `@ControllerAdvice` and `@ExceptionHandler`.

---

# Part 9 – Real-Time Interview Questions

---

## Question 32

Why shouldn't we return raw exceptions to clients?

### Interview Answer

Raw exceptions may expose internal implementation details such as class names, SQL queries, or stack traces. This creates security risks and makes APIs harder for clients to consume.

Instead, applications should return meaningful, standardized error responses.

---

## Question 33

Why use global exception handling?

### Interview Answer

Global exception handling:

- Eliminates duplicate code
- Ensures consistent error responses
- Improves maintainability
- Simplifies application-wide error management

---

# 💡 Key Interview Tips

- Use `@PathVariable` to identify a specific resource.
- Use `@RequestParam` for filtering, searching, sorting, and pagination.
- Use `@RequestBody` to receive JSON data.
- Prefer `ResponseEntity` when you need control over status codes and headers.
- Memorize the most common HTTP status codes.
- Use `@ControllerAdvice` for centralized exception handling.
- Be able to explain the complete request lifecycle from the client to the database and back.

---

# 📝 Chapter Summary

In this chapter, you learned:

- Path Variables
- Query Parameters
- `@PathVariable`
- `@RequestParam`
- `@RequestBody`
- Request Processing
- Form Data vs JSON
- `ResponseEntity`
- HTTP Status Codes
- HTTP Headers
- `@ExceptionHandler`
- `@ControllerAdvice`
- Global Exception Handling
- Request Lifecycle
- Scenario-Based Questions
- Real-Time Interview Questions

Mastering these concepts will help you confidently answer Spring Boot interview questions related to request processing, API design, response handling, and exception management.

---
