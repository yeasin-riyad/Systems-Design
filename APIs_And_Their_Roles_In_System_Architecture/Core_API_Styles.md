# 🚀 Core API Styles Complete Guide

> Beginner to Advanced Interview Preparation Notes  

---

# 📚 Table of Contents

1. What is API Style?
2. REST API
3. GraphQL API
4. SOAP API
5. gRPC
6. WebSocket API
7. Comparison Between API Styles
8. Real World Usage
9. Interview Questions & Answers
10. Final Summary

---

# 🌐 What is API Style?

API Style বলতে বোঝায়:

```text
কিভাবে client এবং server communicate করবে
```

Different API styles different communication rules follow করে।

---

# 🔥 Core API Styles

| API Style | Main Purpose |
|---|---|
| REST | Standard Web APIs |
| GraphQL | Flexible Data Fetching |
| SOAP | Enterprise Communication |
| gRPC | High Performance Service Communication |
| WebSocket | Real-time Communication |

---

# 1️⃣ REST API

# 📌 What is REST?

REST এর পূর্ণরূপ:

```text
Representational State Transfer
```

এটি সবচেয়ে popular API architecture style।

---

# 🏗️ REST Architecture

```text
Client
   |
HTTP Request
   |
   v
REST API Server
   |
   v
Database
```

---

# 🎯 REST Core Idea

সবকিছুকে Resource হিসেবে treat করা হয়।

Example:

```text
/users
/products
/orders
```

---

# 📬 REST HTTP Methods

| Method | কাজ |
|---|---|
| GET | Data Fetch |
| POST | Create Data |
| PUT | Full Update |
| PATCH | Partial Update |
| DELETE | Remove Data |

---

# ✅ REST Example

## Get Users

```http
GET /users
```

Response:

```json
[
  {
    "id": 1,
    "name": "Riyad"
  }
]
```

---

# Create User

```http
POST /users
```

Request Body:

```json
{
  "name": "Riyad"
}
```

---

# ⚡ REST Characteristics

- Stateless
- JSON Based
- Resource Oriented
- Uses HTTP
- Scalable

---

# ✅ REST Advantages

- Easy to learn
- Huge ecosystem
- Browser friendly
- Fast development
- Cache support

---

# ❌ REST Disadvantages

- Over-fetching
- Under-fetching
- Multiple requests needed

---

# 🔥 REST Over-fetching Example

Client শুধু `name` চায়।

কিন্তু server পুরো object পাঠায়:

```json
{
  "name": "Riyad",
  "email": "abc@gmail.com",
  "address": "Dhaka",
  "phone": "12345"
}
```

এটাকে বলে:

```text
Over-fetching
```

---

# ✅ REST Best For

- CRUD Applications
- Web Apps
- Public APIs
- Standard Backend Systems

---

---

# 2️⃣ GraphQL API

# 📌 What is GraphQL?

GraphQL Facebook তৈরি করেছে।

এটি flexible data fetching system।

---

# 🎯 Core Idea

Client exactly যা দরকার শুধু সেটা request করবে।

---

# 🏗️ GraphQL Architecture

```text
Client
   |
Single Endpoint
   |
   v
GraphQL Server
```

---

# REST vs GraphQL

## REST

```text
/users
/products
/orders
```

Multiple endpoints।

---

## GraphQL

```text
/graphql
```

Single endpoint।

---

# ✅ GraphQL Query Example

```graphql
{
  user {
    name
    email
  }
}
```

---

# Response

```json
{
  "data": {
    "user": {
      "name": "Riyad",
      "email": "abc@gmail.com"
    }
  }
}
```

---

# 🔥 Nested Query Example

```graphql
{
  user {
    name
    posts {
      title
    }
  }
}
```

এক request এ nested data পাওয়া যায়।

---

# ✅ GraphQL Advantages

- No over-fetching
- Flexible queries
- Single endpoint
- Better frontend experience

---

# ❌ GraphQL Disadvantages

- Complex backend
- Difficult caching
- Security complexity

---

# ✅ GraphQL Best For

- Social Media Apps
- Mobile Apps
- Data-heavy Applications

---

---

# 3️⃣ SOAP API

# 📌 What is SOAP?

SOAP এর পূর্ণরূপ:

```text
Simple Object Access Protocol
```

পুরানো enterprise systems এ খুব জনপ্রিয়।

---

# 🎯 SOAP Uses XML

Example:

```xml
<user>
   <name>Riyad</name>
</user>
```

---

# 🏗️ SOAP Architecture

```text
Client
   |
SOAP XML Request
   |
   v
SOAP Server
```

---

# ✅ SOAP Request Example

```xml
<Envelope>
  <Body>
    <GetUser>
      <Id>1</Id>
    </GetUser>
  </Body>
</Envelope>
```

---

# ✅ SOAP Advantages

- Enterprise-level security
- Strong contract
- Reliable communication
- Built-in standards

---

# ❌ SOAP Disadvantages

- Heavy XML
- Slow
- Complex
- Hard to maintain

---

# ✅ SOAP Best For

- Banking Systems
- Government Systems
- Enterprise Software

---

---

# 4️⃣ gRPC

# 📌 What is gRPC?

Google তৈরি করেছে।

High-performance API communication protocol।

---

# 🎯 Core Idea

Uses:

```text
Protocol Buffers + HTTP/2
```

instead of JSON/XML।

---

# 🏗️ gRPC Architecture

```text
Service A
    |
 Binary Communication
    |
    v
Service B
```

---

# ✅ gRPC Example

```proto
service UserService {
  rpc GetUser(UserRequest) returns (UserResponse);
}
```

---

# 🚀 Why gRPC Fast?

কারণ:

- Binary data format
- Small payload
- HTTP/2
- Streaming support

---

# ✅ gRPC Advantages

- Extremely fast
- Lightweight
- Strong typing
- Real-time streaming

---

# ❌ gRPC Disadvantages

- Hard debugging
- Weak browser support
- Complex setup

---

# ✅ gRPC Best For

- Microservices
- Distributed Systems
- High-performance Systems

---

---

# 5️⃣ WebSocket API

# 📌 What is WebSocket?

Real-time bidirectional communication protocol।

---

# ❌ HTTP Problem

HTTP works like:

```text
Client → Request
Server → Response
```

Server নিজে থেকে data push করতে পারে না।

---

# ✅ WebSocket Solution

```text
Client ↔ Server
```

Both can send messages anytime।

---

# 🏗️ WebSocket Architecture

```text
Client
   ⇅
WebSocket Server
```

---

# 💬 Chat Application Example

```text
User A → Server → User B
```

Instant message delivery।

---

# ✅ WebSocket Advantages

- Real-time communication
- Low latency
- Persistent connection

---

# ❌ WebSocket Disadvantages

- Hard scaling
- Stateful connection management
- Complex infrastructure

---

# ✅ WebSocket Best For

- Chat Apps
- Multiplayer Games
- Live Notifications
- Stock Market Apps

---

# 📊 API Styles Comparison Table

| Feature | REST | GraphQL | SOAP | gRPC | WebSocket |
|---|---|---|---|---|---|
| Data Format | JSON | JSON | XML | Binary | Custom |
| Speed | Medium | Medium | Slow | Very Fast | Real-time |
| Complexity | Low | Medium | High | High | Medium |
| Best For | CRUD Apps | Flexible UI | Enterprise | Microservices | Real-time Apps |
| Human Readable | Yes | Yes | Yes | No | Sometimes |

---

# 🌍 Real World Usage

| Company/System | API Style |
|---|---|
| Most Websites | REST |
| Facebook | GraphQL |
| Banking Systems | SOAP |
| Google Internal Systems | gRPC |
| WhatsApp | WebSocket |

---

# 🎤 Interview Questions & Answers

---

# ❓ Q1: What is REST API?

## ✅ Answer

REST API হলো HTTP based stateless architecture style যেখানে resources URL দিয়ে represent করা হয়।

Example:

```http
GET /users
```

---

# ❓ Q2: What is Stateless API?

## ✅ Answer

Stateless API previous request remember করে না।

প্রতি request independent হয়।

Example:

```http
Authorization: Bearer token
```

প্রতি request এ token পাঠাতে হয়।

---

# ❓ Q3: Difference Between REST and GraphQL?

| REST | GraphQL |
|---|---|
| Multiple endpoints | Single endpoint |
| Fixed response | Flexible response |
| Over-fetching possible | Exact data fetching |

---

# ❓ Q4: Why GraphQL Better for Mobile Apps?

## ✅ Answer

কারণ mobile network limited হতে পারে।

GraphQL only required data পাঠায়।

তাই bandwidth save হয়।

---

# ❓ Q5: Why SOAP Used in Banking Systems?

## ✅ Answer

কারণ SOAP provides:

- strong security
- reliability
- strict contracts
- transaction support

---

# ❓ Q6: Why gRPC Fast?

## ✅ Answer

কারণ gRPC uses:

- Binary protocol
- HTTP/2
- Small payload
- Streaming

instead of large JSON/XML।

---

# ❓ Q7: Difference Between HTTP and WebSocket?

| HTTP | WebSocket |
|---|---|
| Request-Response | Full Duplex |
| Stateless | Persistent Connection |
| Slower for realtime | Real-time optimized |

---

# ❓ Q8: When Should You Use WebSocket?

## ✅ Answer

When real-time communication is needed.

Examples:

- Chat apps
- Live games
- Live dashboards
- Notifications

---

# ❓ Q9: What is Over-fetching?

## ✅ Answer

যখন client প্রয়োজনের চেয়ে বেশি data পায়।

Example:

Need:

```json
{
  "name": "Riyad"
}
```

Received:

```json
{
  "name": "Riyad",
  "email": "abc@gmail.com",
  "address": "Dhaka"
}
```

---

# ❓ Q10: Which API Style Should Beginners Learn First?

## ✅ Answer

REST API first।

কারণ:
- industry standard
- easiest
- widely used

তারপর:
- GraphQL
- WebSocket
- gRPC concepts

---

# 🚀 Final Mental Model

| API Style | Think Like |
|---|---|
| REST | Standard Web API |
| GraphQL | Smart Flexible API |
| SOAP | Enterprise Secure API |
| gRPC | Ultra Fast Internal API |
| WebSocket | Live Real-time Connection |

---

# 🧠 Final Summary

Modern system architecture এ different API styles different problems solve করে।

| API Style | Purpose |
|---|---|
| REST | Standard communication |
| GraphQL | Flexible querying |
| SOAP | Enterprise reliability |
| gRPC | High-speed internal communication |
| WebSocket | Real-time communication |

---

# ❤️ Final Advice

For interviews:

## Must Master

✅ REST API  
✅ HTTP Methods  
✅ Stateless Architecture  
✅ Authentication  
✅ GraphQL Basics  
✅ WebSocket Concepts  

---

# 🎯 Recommended Learning Order

```text
REST
   ↓
JWT Authentication
   ↓
GraphQL
   ↓
WebSocket
   ↓
gRPC Concepts
   ↓
Advanced System Design
```

---

# 🚀 Happy Learning

Mastering APIs means mastering modern backend architecture.

Keep building projects.  
That is the fastest way to truly understand APIs.

---