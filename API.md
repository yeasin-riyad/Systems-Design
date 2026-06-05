# 🚀 API (Application Programming Interface)

> Complete Beginner to Interview Level Notes on APIs & Their Role in System Architecture

---

# 📌 What is an API?

API stands for:

```text
Application Programming Interface
```

An API is a **communication bridge** between two software systems.

It allows:

- Frontend ↔ Backend
- Mobile App ↔ Server
- Microservice ↔ Microservice
- Website ↔ Third-party Service

to communicate with each other.

---

# 🍔 Real Life Analogy

Imagine a restaurant:

| Real World | Software World |
|---|---|
| Customer | Client |
| Kitchen | Server |
| Waiter | API |

You don't go directly into the kitchen.

You tell the waiter what you want.

The waiter:
- takes your request
- sends it to kitchen
- brings the response back

👉 The waiter is the API.

---

# 🏗️ API in System Architecture

```text
Frontend (React)
       |
       | HTTP Request
       v
REST API (Node.js/Express)
       |
       v
Database (MongoDB/PostgreSQL)
```

---

# 🔄 API Request-Response Lifecycle

## Step 1: Client Sends Request

```http
GET /products
```

---

## Step 2: Server Receives Request

```js
app.get("/products", (req, res) => {
   res.send(products);
});
```

---

## Step 3: Business Logic Executes

- Validation
- Authentication
- Database Query
- Authorization

---

## Step 4: Response Returned

```json
[
  {
    "name": "Laptop",
    "price": 50000
  }
]
```

---

# 🎯 Why APIs are Important?

Without APIs:

❌ Frontend would access database directly  
❌ Security would be destroyed  
❌ Business logic could not be controlled  
❌ Scalability would become difficult  

APIs solve these problems.

---

# 🔥 Roles of APIs in System Architecture

---

# 1. Communication Layer

APIs enable communication between systems.

```text
Frontend → API → Backend
```

---

# 2. Data Exchange

APIs transfer data between systems.

## Example

```json
{
  "email": "user@gmail.com",
  "password": "1234"
}
```

---

# 3. Security Layer

API handles:

- Authentication
- Authorization
- Validation
- Rate Limiting

---

# 4. Business Logic Layer

All business rules stay inside APIs.

## Example

E-commerce API checks:

- Product stock
- Payment status
- Coupon validity
- User permissions

---

# 5. Scalability

One API can serve multiple clients.

```text
Web App
Mobile App
Admin Panel

     ↓

 Same Backend API
```

---

# 6. Service Integration

APIs connect external services.

Examples:

- Payment Gateway
- SMS Service
- Email Service
- Google Login

---

# 🧠 Key Characteristics of APIs

---

# 1. Abstraction

API hides internal complexity.

```http
POST /pay
```

You don't see:
- banking logic
- fraud detection
- encryption

---

# 2. Statelessness

REST APIs are stateless.

Each request is independent.

```http
Authorization: Bearer token
```

Every request must contain required information.

---

# 3. Standard Communication

Most APIs use:

- HTTP
- HTTPS

---

# 4. Structured Data Exchange

Most APIs use:

- JSON
- XML

## JSON Example

```json
{
  "name": "Riyad",
  "age": 24
}
```

---

# 5. Platform Independent

Same API can be used by:

- Web App
- Android App
- iOS App
- Desktop App

---

# 6. Reusability

One API can serve many applications.

---

# 7. Security

API security includes:

- JWT
- OAuth
- Validation
- Encryption

---

# 8. Loose Coupling

Frontend and backend remain independent.

Backend can change internally without affecting frontend.

---

# 9. Versioning

```text
/api/v1/users
/api/v2/users
```

Helps avoid breaking old applications.

---

# 10. Scalability

APIs support distributed systems.

```text
Clients
   ↓
Load Balancer
   ↓
Multiple API Servers
```

---

# 🌐 Types of APIs

---

# 1. REST API

Most popular API architecture.

Uses:
- HTTP Methods
- JSON

## Example

```http
GET /users
POST /users
PUT /users/1
DELETE /users/1
```

---

# 2. GraphQL API

Client requests exactly what it needs.

## Example

```graphql
{
  user {
    name
    email
  }
}
```

---

# 3. SOAP API

- XML based
- Enterprise systems
- Highly strict

---

# 4. gRPC

High-performance communication protocol.

Used heavily in:
- microservices
- distributed systems

---

# 📬 HTTP Methods

| Method | Purpose |
|---|---|
| GET | Retrieve data |
| POST | Create data |
| PUT | Full update |
| PATCH | Partial update |
| DELETE | Remove data |

---

# 🔐 API Authentication Example

## Login Request

```http
POST /login
```

---

## Server Response

```json
{
  "token": "jwt-token"
}
```

---

## Protected Request

```http
Authorization: Bearer jwt-token
```

---

# 🏢 API Gateway

In large systems, a central API entry point exists.

This is called:

```text
API Gateway
```

Responsibilities:

- Authentication
- Rate Limiting
- Routing
- Logging
- Load Balancing

---

# ⚡ APIs in Microservice Architecture

```text
Order Service ---> Payment Service
```

Example:

```http
POST /process-payment
```

Microservices communicate through APIs.

---

# 🛒 Real World E-commerce Architecture

```text
                ┌─────────────┐
                │ React Front │
                └──────┬──────┘
                       |
                       | HTTPS API
                       v
             ┌───────────────────┐
             │ API Gateway       │
             └────────┬──────────┘
                      |
      ┌───────────────┼────────────────┐
      v               v                v

┌──────────┐   ┌──────────┐    ┌──────────┐
│Auth API  │   │Order API │    │Product API│
└────┬─────┘   └────┬─────┘    └────┬─────┘
     |               |               |
     v               v               v

 Databases      Databases      Databases
```

---

# 🧩 Internal API vs Public API

| Type | Description |
|---|---|
| Internal API | Used inside company |
| Public API | Used by external developers |

---

# 🌍 Famous Public APIs

- Google Maps API
- Stripe Payment API
- OpenAI API
- Facebook Graph API

---

# 🧠 Simple Mental Model

```text
Frontend = Face
Backend = Brain
Database = Memory
API = Nervous System
```

---

# 📋 API Best Practices

- Use HTTPS
- Validate inputs
- Use JWT authentication
- Apply rate limiting
- Use proper status codes
- Version your APIs
- Write documentation
- Keep APIs stateless

---

# 📚 Common HTTP Status Codes

| Code | Meaning |
|---|---|
| 200 | Success |
| 201 | Created |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 500 | Internal Server Error |

---

# 🛠️ Popular API Tools

| Tool | Purpose |
|---|---|
| Postman | API Testing |
| Swagger | API Documentation |
| Insomnia | API Testing |
| Thunder Client | VS Code API Testing |

---

# 🎤 Interview Questions on APIs

---

## Q1: What is an API?

API is a communication interface between software systems.

---

## Q2: Why are APIs important?

They enable:
- communication
- scalability
- security
- modularity

---

## Q3: What is REST API?

REST API is an architectural style using:
- HTTP
- Stateless communication
- JSON data format

---

## Q4: What is Stateless API?

Server does not remember previous requests.

Each request is independent.

---

## Q5: Difference Between REST and GraphQL?

| REST | GraphQL |
|---|---|
| Multiple endpoints | Single endpoint |
| Fixed response | Flexible response |
| Overfetching possible | Exact data fetching |

---

# 🚀 Final Summary

API is the backbone of modern software systems.

It provides:

✅ Communication  
✅ Security  
✅ Scalability  
✅ Reusability  
✅ Integration  
✅ Business Logic Handling  

Without APIs:

- frontend/backend separation
- mobile applications
- cloud systems
- microservices

would not function efficiently.

---

# ❤️ End Note

If you deeply understand APIs, you automatically understand a huge part of:

- Backend Development
- System Design
- Microservices
- Cloud Architecture
- Full Stack Development

Mastering APIs is one of the most important skills in modern software engineering.

---