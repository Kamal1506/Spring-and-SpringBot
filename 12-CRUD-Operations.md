# RESTful CRUD Operations Interview Handbook

**Interview Importance:** Critical

---

# CRUD Basics

## Q1. What is CRUD?

**Interview Importance:** Critical

### Interview Answer

CRUD stands for:

- **C** – Create
- **R** – Read
- **U** – Update
- **D** – Delete

These are the four basic operations performed on resources in a REST API.

---

## Q2. Which HTTP methods are used for CRUD?

**Interview Importance:** Critical

| CRUD Operation | HTTP Method |
|---------------|-------------|
| Create | POST |
| Read | GET |
| Update | PUT / PATCH |
| Delete | DELETE |

---

## Q3. Explain CRUD operations with an Employee API.

**Interview Importance:** Critical

| Operation | Endpoint | HTTP Method |
|------------|----------|-------------|
| Create Employee | `POST /employees` | POST |
| Get All Employees | `GET /employees` | GET |
| Get Employee by ID | `GET /employees/{id}` | GET |
| Update Employee | `PUT /employees/{id}` | PUT |
| Delete Employee | `DELETE /employees/{id}` | DELETE |

---

# Create (POST)

## Q4. Why is POST used for Create?

**Interview Importance:** Critical

### Interview Answer

POST is used to create a new resource because the server accepts the new resource and typically generates its unique identifier (URI).

**Example**

```http
POST /employees
```

**Request Body**

```json
{
  "name": "Kamal",
  "salary": 50000
}
```

**Response**

```http
201 Created
```

---

## Q5. What status code should POST return?

**Interview Answer**

```
201 Created
```

---

# Read (GET)

## Q6. Why is GET considered a Safe HTTP Method?

**Interview Importance:** Critical

### Interview Answer

GET is considered **safe** because it only retrieves data and does not modify the server state.

Calling it multiple times should never change the resource.

---

## Q7. Why is GET idempotent?

Because multiple GET requests always produce the same effect on the server—they only fetch data and do not modify it.

---

# Update (PUT & PATCH)

## Q8. What is PUT?

**Interview Importance:** Critical

### Interview Answer

PUT updates or completely replaces an existing resource.

The client usually sends the entire updated object.

**Example**

```http
PUT /employees/10
```

---

## Q9. What is PATCH?

**Interview Importance:** Critical

### Interview Answer

PATCH updates only selected fields of an existing resource.

**Current Employee**

```json
{
  "name": "Kamal",
  "salary": 50000
}
```

**PATCH Request**

```json
{
  "salary": 60000
}
```

Only the salary field is updated.

---

## Q10. Difference between PUT and PATCH

| PUT | PATCH |
|------|--------|
| Updates the entire resource | Updates selected fields |
| Sends complete object | Sends only modified fields |
| Idempotent | Usually idempotent (depends on implementation) |

---

# Delete

## Q11. What is DELETE?

**Interview Importance:** Critical

### Interview Answer

DELETE removes an existing resource from the server.

**Example**

```http
DELETE /employees/5
```

---

## Q12. Which status code should DELETE return?

**Recommended**

```
204 No Content
```

If the API returns a response body, it may return:

```
200 OK
```

---

# Idempotency

> This is one of the most frequently asked interview topics.

## Q13. What is Idempotency?

**Interview Importance:** Critical

### Interview Answer

An HTTP method is **idempotent** if performing the same request multiple times has the same effect as performing it once.

---

## Q14. Which HTTP methods are idempotent?

| HTTP Method | Idempotent |
|-------------|------------|
| GET | ✅ |
| PUT | ✅ |
| DELETE | ✅ |
| POST | ❌ |
| PATCH | Usually (depends on implementation) |

---

## Q15. Why is POST not idempotent?

**Example**

```http
POST /employees
```

Called three times

↓

Three employee records are created.

The server state changes after every request.

---

## Q16. Why is DELETE idempotent?

**Example**

```
DELETE /employees/5
```

**First Request**

↓

Employee is deleted.

**Second Request**

↓

Employee already does not exist.

The final server state remains unchanged—Employee 5 is absent.

---

# Validation

> Very frequently asked in Spring Boot interviews.

## Q17. Why do we validate input?

**Interview Importance:** Critical

### Interview Answer

Validation ensures that incoming data is correct before processing.

### Benefits

- Prevents invalid data
- Improves security
- Maintains data integrity
- Reduces application errors

---

## Q18. What is `@Valid`?

**Interview Importance:** Critical

### Interview Answer

`@Valid` triggers Bean Validation before the controller method executes.

```java
@PostMapping
public Employee create(
        @Valid
        @RequestBody EmployeeDTO dto) {
}
```

---

## Q19. Common Validation Annotations

| Annotation | Purpose |
|------------|----------|
| `@NotNull` | Value cannot be null |
| `@NotBlank` | String cannot be null, empty or whitespace |
| `@NotEmpty` | Collection/String cannot be empty |
| `@Size` | Minimum or maximum length |
| `@Email` | Valid email format |
| `@Pattern` | Regular expression validation |
| `@Min` | Minimum numeric value |
| `@Max` | Maximum numeric value |
| `@Positive` | Value must be greater than zero |

---

## Q20. Difference between `@NotNull`, `@NotEmpty`, and `@NotBlank`

| Annotation | Allows Empty String? | Allows Only Spaces? |
|------------|----------------------|---------------------|
| `@NotNull` | ✅ Yes | ✅ Yes |
| `@NotEmpty` | ❌ No | ✅ Yes |
| `@NotBlank` | ❌ No | ❌ No |

### Example

#### `@NotNull`

```java
String name;
```

Allowed

```text
""
```

because it is not null.

---

#### `@NotEmpty`

```java
String name;
```

Not Allowed

```text
""
```

Allowed

```text
"   "
```

---

#### `@NotBlank`

Rejects

```text
""
```

and

```text
"   "
```

---

## Q21. What happens if validation fails?

Spring throws a validation exception (commonly `MethodArgumentNotValidException` for `@RequestBody` validation).

The API should return:

```http
400 Bad Request
```

with meaningful validation error details.

---

# Optimistic Locking

> Advanced interview topic.

## Q22. What is Optimistic Locking?

**Interview Importance:** High

### Interview Answer

Optimistic Locking prevents lost updates when multiple users modify the same record simultaneously.

It assumes conflicts are rare and detects them before saving.

---

## Q23. Which annotation enables Optimistic Locking?

```java
@Version
```

Example

```java
@Entity
public class Employee {

    @Version
    private Integer version;

}
```

---

## Q24. How does Optimistic Locking work?

Suppose:

```
Employee Version = 5
```

Two users load the same record.

```
User A → Version 5

User B → Version 5
```

User A updates first.

```
Version becomes 6
```

User B now tries to save Version 5.

Hibernate detects the version mismatch.

↓

Throws an Optimistic Locking exception instead of overwriting User A's changes.

---

## Q25. Why use Optimistic Locking?

It prevents concurrent users from accidentally overwriting each other's updates and protects data consistency.

---

# Internal Working

## Q26. Explain the POST request flow.

```text
Client
   ↓
POST /employees
   ↓
@RequestBody
   ↓
DTO
   ↓
Validation
   ↓
Service
   ↓
Repository
   ↓
Database
   ↓
Entity
   ↓
DTO
   ↓
JSON
   ↓
Client
```

---

# Scenario Questions

## Q27. User submits an empty email.

What happens?

Validation fails.

The API returns:

```http
400 Bad Request
```

---

## Q28. Two users update the same record simultaneously.

How do you prevent data loss?

Use **Optimistic Locking** with the `@Version` annotation.

---

## Q29. Which validation annotation checks email format?

```java
@Email
```

---

## Q30. Employee name cannot contain only spaces.

Which annotation?

```java
@NotBlank
```

---

## Q31. Password must contain at least eight characters.

Which annotation?

```java
@Size(min = 8)
```

---

# HR Follow-Up Questions

## Q32. Why validate on the server if the frontend already validates?

Frontend validation improves user experience.

However, it can be bypassed.

Server-side validation is essential to protect data integrity and application security.

---

## Q33. Why should clients not decide resource IDs?

A common REST design is for the server to generate IDs to ensure uniqueness and maintain control over resource creation.

---

## Q34. Why should PUT replace the entire object?

PUT represents a complete replacement of a resource.

If only a few fields need to change, PATCH is generally the better choice.

---

# Tricky Questions

## Q35. Can POST update data?

Yes.

Technically POST can update data, but according to REST conventions it is primarily intended for creating resources or performing non-idempotent operations.

PUT or PATCH should generally be used for updates.

---

## Q36. Can DELETE return `200 OK` instead of `204 No Content`?

Yes.

- **200 OK** → When the API returns a response body.
- **204 No Content** → When no response body is returned.

Both are valid depending on the API design.

---

## Q37. Which HTTP method is most dangerous?

No HTTP method is inherently "dangerous."

However, methods like **DELETE**, **PUT**, and **PATCH** modify data and therefore require proper authentication, authorization, and validation.

---
```
