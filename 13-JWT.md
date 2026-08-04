# JWT (JSON Web Token) Interview Handbook

**Interview Importance:** Critical

---

# JWT Basics

## Q1. What is JWT?

**Interview Importance:** Critical

### Interview Answer

JWT (**JSON Web Token**) is a compact, secure, and self-contained token used to authenticate and authorize users in stateless applications.

Instead of storing user sessions on the server, the server sends a signed token to the client after successful login. The client includes this token with every subsequent request.

### Real-Time Example

```text
Login
   ↓
Username & Password
   ↓
Server verifies credentials
   ↓
Server generates JWT
   ↓
Client stores JWT
   ↓
Client sends JWT with every API request
```

---

## Q2. Why do we use JWT?

**Interview Importance:** Critical

### Interview Answer

JWT is used because it enables **stateless authentication**.

### Benefits

- No server-side session storage
- Better scalability
- Suitable for REST APIs
- Works well with microservices
- Easy to use with web and mobile applications

---

## Q3. What does Stateless mean?

**Interview Importance:** Critical

### Interview Answer

Stateless means the server does **not** store client session information.

Each request contains all the information required for authentication, usually in the JWT.

### Stateful vs Stateless

| Stateful | Stateless |
|-----------|------------|
| Server stores session | Server stores no session |
| Uses Session ID | Uses JWT Token |
| More memory usage | Better scalability |
| Common in traditional web apps | Common in REST APIs |

---

# JWT Structure

## Q4. What is inside a JWT?

**Interview Importance:** Critical

A JWT consists of three parts:

- Header
- Payload
- Signature

Represented as:

```text
xxxxx.yyyyy.zzzzz
```

---

## Q5. Explain the JWT Header.

### Interview Answer

The **Header** contains metadata about the token, such as:

- Token type (`JWT`)
- Signing algorithm (e.g., `HS256`)

Example:

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

---

## Q6. Explain the JWT Payload.

**Interview Importance:** Critical

### Interview Answer

The **Payload** contains claims (information) about the user.

Example:

```json
{
  "username": "kamal",
  "role": "USER"
}
```

### Common Claims

- Subject (`sub`)
- Issued At (`iat`)
- Expiration (`exp`)
- Username
- Roles

---

## Q7. Explain the JWT Signature.

**Interview Importance:** Critical

### Interview Answer

The **Signature** verifies that the token has not been modified.

It is generated using:

- Header
- Payload
- Secret key (or private key for asymmetric algorithms)

If the payload changes, the signature becomes invalid.

---

## Q8. Can anyone read a JWT?

**Interview Importance:** Critical

### Interview Answer

Yes.

The Header and Payload are **Base64URL encoded**, not encrypted.

Anyone with the token can decode and read them.

**Never store sensitive information inside the payload.**

---

## Q9. Can anyone modify a JWT?

### Interview Answer

A user can modify the decoded payload, but they **cannot generate a valid signature** without the server's secret key.

If the payload changes, signature validation fails and the server rejects the token.

---

# JWT in HTTP Requests

## Q10. Where is JWT sent in an HTTP request?

**Interview Importance:** Critical

### Interview Answer

JWT is usually sent in the **Authorization** header.

Example:

```http
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...
```

---

## Q11. Why do we use the Bearer prefix?

### Interview Answer

`Bearer` indicates that the client is presenting a bearer token for authentication.

It is the standard authentication scheme used with the `Authorization` header.

---

# Authentication Flow

## Q12. What happens after login?

**Interview Importance:** Critical

### Interview Answer

1. User submits username and password.
2. Spring Security authenticates the credentials.
3. The server generates a JWT.
4. The JWT is returned to the client.
5. The client stores the JWT.
6. The client includes the JWT in future requests.

---

## Q13. Explain the JWT Authentication Flow.

**Interview Importance:** Critical

```text
Client
   ↓
Login
   ↓
Spring Security
   ↓
Database
   ↓
Credentials Verified
   ↓
JWT Generated
   ↓
Client Stores JWT
   ↓
Future Request
   ↓
Authorization: Bearer Token
   ↓
JWT Validated
   ↓
Controller
```

---

# Token Storage

## Q14. Where should JWT be stored?

### Interview Answer

Common options include:

- Memory (most secure for SPAs while the page is active)
- HttpOnly Secure Cookies (helps reduce XSS risks when configured correctly)
- Browser Storage (`localStorage` or `sessionStorage`) — common but more vulnerable to XSS attacks

The best option depends on the application's architecture and security requirements.

---

## Q15. What happens if JWT expires?

### Interview Answer

The server rejects the request.

The user must authenticate again or obtain a new access token using a refresh token (if supported).

---

# Access Token & Refresh Token

## Q16. What is an Access Token?

**Interview Importance:** Critical

### Interview Answer

An Access Token is a short-lived JWT used to access protected resources.

Example:

```
Expires in 15 minutes
```

---

## Q17. What is a Refresh Token?

**Interview Importance:** Critical

### Interview Answer

A Refresh Token is a long-lived credential used to obtain a new Access Token without requiring the user to log in again.

---

## Q18. Access Token vs Refresh Token

**Interview Importance:** Critical

| Access Token | Refresh Token |
|---------------|---------------|
| Short-lived | Long-lived |
| Accesses APIs | Requests new Access Tokens |
| Sent frequently | Used only when renewing tokens |

---

## Q19. Why use short-lived Access Tokens?

### Interview Answer

If an Access Token is stolen, it can only be used until it expires.

Short expiration times reduce the impact of token theft.

---

## Q20. What happens if a JWT is stolen?

### Interview Answer

An attacker can use the token until it expires.

To reduce the risk:

- Use HTTPS
- Keep Access Tokens short-lived
- Store tokens securely
- Use Refresh Token rotation or token revocation when appropriate

---

# JWT vs Session

## Q21. Why is JWT preferred over Sessions?

**Interview Importance:** Critical

| Sessions | JWT |
|-----------|-----|
| Server stores session | Client stores token |
| Requires session storage | Stateless |
| Harder to scale | Easier to scale |
| Best for traditional web apps | Ideal for REST APIs |

---

# JWT Validation

## Q22. Explain JWT Validation Flow.

**Interview Importance:** Critical

```text
Client
   ↓
Bearer Token
   ↓
JWT Filter
   ↓
Extract Token
   ↓
Validate Signature
   ↓
Check Expiration
   ↓
Authentication Success
   ↓
Controller
```

---

## Q23. What happens if the signature is invalid?

### Interview Answer

The server rejects the token because it may have been tampered with or signed using an invalid key.

The request is not authenticated.

---

## Q24. What happens if the Authorization header is missing?

### Interview Answer

Spring Security treats the request as unauthenticated.

If the endpoint requires authentication, access is denied.

Typical response:

```http
401 Unauthorized
```

---

## Q25. Why shouldn't passwords be stored in JWT?

### Interview Answer

JWT payloads are encoded—not encrypted.

Anyone possessing the token can decode the payload.

Only non-sensitive claims should be stored in the token.

---

# Scenario Questions

## Q26. User logs in once but accesses APIs for the next 15 minutes without logging in again. Why?

### Answer

Because the client includes the valid JWT in every request.

---

## Q27. User changes one character in the JWT.

What happens?

### Answer

Signature validation fails.

The server rejects the token.

---

## Q28. A frontend developer forgets to send the Bearer token.

What happens?

### Answer

Authentication fails.

Protected endpoints return:

```http
401 Unauthorized
```

---

## Q29. Why is JWT ideal for Microservices?

### Interview Answer

Each microservice can validate the JWT independently without sharing session state.

This improves scalability and keeps services loosely coupled.

---

# Project Questions

## Q30. How did you use JWT in your project?

**Interview Importance:** Critical

### Model Answer

I implemented JWT-based authentication using Spring Security.

During login, the backend verified the user's credentials and generated a JWT containing the username and role.

The frontend stored the token and included it in the `Authorization: Bearer <token>` header for protected API requests.

A JWT filter validated the token before allowing access to secured endpoints.

---

## Q31. Which endpoints should be public?

Typical examples:

- `/login`
- `/register`
- Swagger/OpenAPI documentation (optional)
- Health endpoint (depending on requirements)

---

## Q32. Which endpoints should be protected?

Typical examples:

- Create Employee
- Update Employee
- Delete Employee
- User Profile
- Admin APIs

---

# Internal Working

## Q33. Walk me through what happens from clicking the Login button until accessing a protected API.

**Interview Importance:** Critical

### Model Answer

Model Answer

When the user clicks Login, the frontend sends the username and password to the backend. 

Spring Security authenticates the credentials by loading the user details and comparing the submitted password with the stored BCrypt hash. 

If authentication succeeds, the server generates a signed JWT and returns it to the client. 

The client stores the token and includes it in the Authorization: Bearer header for future requests. 

For every protected request, the Security Filter Chain extracts the JWT, validates its signature and expiration, creates an authenticated security context, and then allows the request to reach the controller. 

If the token is invalid or expired, the request is rejected.

---
