# DTOs & JSON Serialization Interview Handbook

**Interview Importance:** Critical

## DTO (Data Transfer Object)

### Q1. What is a DTO?

**Interview Importance:** Critical

**Interview Answer**

A **DTO (Data Transfer Object)** is a simple Java class used to transfer
data between different layers of an application or between the server
and the client.

It contains only the required data and does not contain business logic.

``` java
public class EmployeeDTO {
    private Long id;
    private String name;
}
```

### Q2. Why do we need DTOs?

**Interview Importance:** Critical

-   Hide sensitive data
-   Reduce unnecessary data transfer
-   Improve security
-   Improve performance
-   Decouple API models from database entities

**Real-Time Example**

Entity fields:

-   id
-   name
-   salary
-   password
-   bankAccount
-   createdDate
-   updatedDate

Client only needs:

-   id
-   name

DTO transfers only the required fields.

### Q3. Why shouldn't we expose Entity classes directly?

**Interview Importance:** Critical

Returning entities directly can:

-   Expose sensitive fields
-   Create security issues
-   Tighten API coupling with the database model
-   Return unnecessary data
-   Cause serialization problems with bidirectional relationships

DTOs solve these problems.

### Q4. Difference between Entity and DTO

  Entity                             DTO
  ---------------------------------- ----------------------------
  Represents database table          Represents API data
  Contains persistence annotations   No persistence annotations
  Stored in database                 Used for data transfer
  Managed by JPA                     Not managed by JPA

## Entity Mapping

### Q5. What is Entity Mapping?

Entity Mapping is the process of converting:

-   Entity → DTO
-   DTO → Entity

### Q6. How do you map Entity to DTO?

**Manual Mapping**

``` java
EmployeeDTO dto = new EmployeeDTO();
dto.setId(employee.getId());
dto.setName(employee.getName());
```

**ModelMapper**

``` java
EmployeeDTO dto = modelMapper.map(employee, EmployeeDTO.class);
```

**MapStruct**

``` java
EmployeeDTO dto = mapper.toDTO(employee);
```

MapStruct generates mapping code at compile time and is generally faster
than reflection-based mappers.

### Q7. Manual Mapping vs ModelMapper vs MapStruct

  Manual         ModelMapper        MapStruct
  -------------- ------------------ -------------------------
  Fast           Easy               Fastest
  More code      Less code          Compile-time generation
  Full control   Reflection-based   High performance

## Serialization

### Q8. What is Serialization?

**Interview Importance:** Critical

Converts a Java object into JSON or XML.

    Java Object
       ↓
    Jackson
       ↓
    JSON

### Q9. What is Deserialization?

**Interview Importance:** Critical

Converts JSON into a Java object.

    JSON
     ↓
    Jackson
     ↓
    Java Object

### Q10. Which library performs serialization?

Spring Boot uses **Jackson** by default.

## Jackson Annotations

### Q11. What is @JsonIgnore?

Excludes a field from JSON serialization/deserialization.

``` java
@JsonIgnore
private String password;
```

### Q12. Why use @JsonIgnore?

Hide sensitive information such as passwords, OTPs and secret keys.

### Q13. What is @JsonProperty?

Changes the JSON property name.

``` java
@JsonProperty("employee_name")
private String name;
```

### Q14. What is @JsonFormat?

Formats date/time values during serialization.

``` java
@JsonFormat(pattern = "dd-MM-yyyy")
private LocalDate dob;
```

## API Versioning

### Q15. What is API Versioning?

Allows multiple API versions to coexist.

Example:

-   `/api/v1/employees`
-   `/api/v2/employees`

### Q16. Why is API Versioning needed?

It prevents breaking existing clients when the API evolves.

### Q17. API Versioning Strategies

  Strategy          Example
  ----------------- -------------------------------------------
  URI               `/v1/employees`
  Query Parameter   `?version=1`
  Header            `X-API-Version: 1`
  Accept Header     `Accept: application/vnd.company.v1+json`

### Q18. Most common strategy

**URI Versioning** because it is simple and readable.

## Internal Working

### Q19. DTO Flow

    Database
       ↓
    Entity
       ↓
    DTO
       ↓
    Jackson
       ↓
    JSON
       ↓
    Client

    Client
       ↓
    JSON
       ↓
    DTO
       ↓
    Entity
       ↓
    Database

## Scenario Questions

### Q20. Why use DTO if Entity already has the same fields?

DTOs keep the API independent from the database model.

### Q21. Client should not see salary.

Create a DTO without the salary field.

### Q22. Password should never be returned.

Use `@JsonIgnore`.

### Q23. Which is better?

Return `EmployeeDTO` instead of `Employee`.

### Q24. How do DTOs improve performance?

They reduce response size, bandwidth usage and serialization overhead.

## HR Follow-Up Questions

### Q25. Can DTO contain business logic?

No. Business logic belongs in the Service layer.

### Q26. Where should DTO mapping happen?

Usually in the Service layer or dedicated mapper classes.

### Q27. What happens if Entity changes?

DTOs keep the API contract stable.

### Q28. Why is Jackson used?

It converts Java objects to JSON and JSON back to Java objects.

## Tricky Questions

### Q29. Is DTO mandatory?

No. It is recommended for production applications.

### Q30. Can one Entity have multiple DTOs?

Yes.

Examples:

-   EmployeeSummaryDTO
-   EmployeeDetailDTO
-   EmployeeSalaryDTO
-   EmployeeLoginDTO

### Q31. Can one DTO map to multiple Entities?

Yes. Example: `OrderResponseDTO` combining Order, Customer and Product
data.
