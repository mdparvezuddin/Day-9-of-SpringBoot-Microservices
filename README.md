# Day 09 – JWT Authentication & Authorization using Spring Security

# Project Overview

This mini project demonstrates the implementation of **JWT (JSON Web Token) based Authentication and Authorization** in Spring Boot.

Unlike traditional Session-Based Authentication, JWT provides a **stateless security mechanism** where the server does not store session information.

The client first authenticates using valid credentials through a login API. Upon successful authentication, a JWT token is generated and returned to the client.

For every subsequent request, the client sends the token in the Authorization header, allowing access to secured APIs without maintaining server-side sessions.

---

# Learning Objectives

By completing this project, we learned:

✔ Stateless Authentication

✔ JWT Token Generation

✔ Token Validation

✔ Security Filter Implementation

✔ Authentication using Spring Security Context

✔ Securing REST APIs

✔ Request Interception using Filters

✔ Bearer Token Mechanism

✔ Protected Endpoint Access

---

# Technologies Used

- Java 21
- Spring Boot 4.x
- Spring Security
- JWT (JJWT Library)
- Maven
- REST APIs
- Postman
- Tomcat
- STS / IntelliJ IDEA

---

# Project Architecture

```text
Client
   │
   │ Login Request
   ▼

POST /auth/login

   │
   │ Validate Credentials
   ▼

AuthController

   │
   │ Generate JWT
   ▼

JwtUtil

   │
   │ Return Token
   ▼

JWT Token

══════════════════════════

Client stores Token

Authorization:
Bearer eyJhbGci...

══════════════════════════

GET /api/dashboard

   │

JwtFilter

   │

Validate Token

   │

SecurityContextHolder

   │

DashboardController

   │

Protected Resource

   ▼

Response
```

---

# Project Structure

```text
jwt-demo

src/main/java

└── com.example.demo

    ├── JwtDemoApplication.java

    ├── AppUser.java

    ├── AuthController.java

    ├── DashboardController.java

    ├── JwtFilter.java

    ├── JwtUtil.java

    ├── LoginRequest.java

    ├── LoginResponse.java

    └── SecurityConfig.java
```

---

# Modules Implemented

## 1. AppUser

Stores application credentials.

Current implementation uses static values.

```java
USERNAME = "Parvez"

PASSWORD = "Parvez123"
```

Later this can be migrated to:

- H2 Database
- MySQL
- PostgreSQL

Source: :contentReference[oaicite:0]{index=0}

---

## 2. AuthController

Responsible for authentication.

Exposes:

```text
POST /auth/login
```

Receives:

```json
{
   "username":"Parvez",
   "password":"Parvez123"
}
```

Validates credentials.

Generates JWT.

Returns token.

Source: :contentReference[oaicite:1]{index=1}

---

## 3. JwtUtil

Core JWT utility component.

Responsibilities:

### Generate Token

```java
generateToken()
```

### Extract Username

```java
extractUsername()
```

### Validate Token

```java
isTokenValid()
```

Token Algorithm:

```text
HS256
```

Token Expiry:

```text
1 Hour
```

Source: :contentReference[oaicite:2]{index=2}

---

## 4. JwtFilter

Custom Spring Security Filter.

Extends:

```java
OncePerRequestFilter
```

Responsibilities:

- Reads Authorization Header

- Extracts JWT Token

- Validates Token

- Retrieves Username

- Creates Authentication Object

- Stores Authentication in Security Context

Source: :contentReference[oaicite:3]{index=3}

---

## 5. DashboardController

Protected API endpoint.

Exposes:

```text
GET /api/dashboard
```

Retrieves authenticated user information using:

```java
SecurityContextHolder
```

Returns:

```text
Welcome, Parvez!
This is protected data.
```

Source: :contentReference[oaicite:4]{index=4}

---

## 6. JwtDemoApplication

Entry point of the application.

Bootstraps Spring Boot.

Source: :contentReference[oaicite:5]{index=5}

---

# Authentication Flow

```text
Client

↓

POST /auth/login

↓

Credentials Validation

↓

JWT Generation

↓

Token Returned

↓

Client Stores Token

↓

Authorization Header

↓

Bearer <token>

↓

GET /api/dashboard

↓

JwtFilter

↓

Token Validation

↓

SecurityContextHolder

↓

DashboardController

↓

Protected Response
```

---

# API Endpoints

## Login API

```http
POST /auth/login
```

Request Body

```json
{
   "username":"Parvez",
   "password":"Parvez123"
}
```

Response

```json
{
   "token":"eyJhbGciOiJIUzI1NiJ9..."
}
```

---

## Protected API

```http
GET /api/dashboard
```

Headers

```text
Authorization

Bearer eyJhbGciOiJIUzI1NiJ9...
```

Response

```text
Welcome, Parvez!
This is protected data.
```

---

# Postman Testing

## Step 1

Create Request

```text
POST

http://localhost:8181/auth/login
```

Body

```json
{
   "username":"Parvez",
   "password":"Parvez123"
}
```

Click Send.

Copy JWT Token.

---

## Step 2

Create New Request

```text
GET

http://localhost:8181/api/dashboard
```

Authorization

```text
Bearer Token
```

Paste token.

Click Send.

Expected Response

```text
Welcome, Parvez!
This is protected data.
```

---

# Security Concepts Covered

### Authentication

Verifying user identity.

---

### Authorization

Determining what resources the authenticated user can access.

---

### JWT

Self-contained security token.

Contains:

- Subject

- Issued Time

- Expiry Time

- Signature

---

### Bearer Token

Token sent with every request.

```text
Authorization:

Bearer <JWT_TOKEN>
```

---

### SecurityContextHolder

Stores authenticated user details during request processing.

---

### OncePerRequestFilter

Ensures filter execution only once per request.

---

# Key Takeaways

✔ Stateless Authentication

✔ Secure REST APIs

✔ Custom Security Filter

✔ Token-Based Authentication

✔ Spring Security Integration

✔ JWT Generation and Validation

✔ Request Authorization

✔ Protected Endpoints

✔ Postman Testing

✔ Industry Standard Authentication Mechanism

---

# Future Enhancements

- Database Authentication

- H2 Integration

- MySQL Integration

- BCrypt Password Encryption

- Role Based Authorization

- Refresh Tokens

- Access Token Expiration Handling

- User Registration API

- Custom Exception Handling

- Microservices Security

- API Gateway JWT Validation

---

# Outcome

Successfully implemented a JWT-based Authentication System using Spring Boot and Spring Security, enabling secure access to protected REST APIs through stateless token-based authentication.
