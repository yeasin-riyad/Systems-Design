# 🔐 Authentication (AuthN) & Authorization (AuthZ) Complete Guide


---

# 📚 Table of Contents

* Introduction
* What is Authentication?
* What is Authorization?
* Authentication vs Authorization
* Authentication Methods
* Authorization Models
* JWT & Authentication Flow
* HTTP Status Codes
* Real World Examples
* Express.js Examples
* Interview Questions & Answers
* Final Summary

---

# 🌟 Introduction

Application Security-এর সবচেয়ে গুরুত্বপূর্ণ দুটি Concept হলো:

```text
Authentication (AuthN)
Authorization (AuthZ)
```

প্রায় সব Modern Applications যেমন:

* Google
* Facebook
* Amazon
* Netflix

এই দুইটি Concept ব্যবহার করে User Access Control করে।

---

# 🔐 What is Authentication (AuthN)?

Authentication হলো:

```text
Identity Verification Process
```

অর্থাৎ:

```text
তুমি আসলে কে?
```

সেটা Verify করা।

---

# 🏢 Real Life Example

ধরো তুমি একটি অফিসে প্রবেশ করতে চাও।

Security Guard তোমাকে জিজ্ঞাসা করলো:

```text
আপনি কে?
```

তুমি ID Card দেখালে।

Guard Verify করলো।

```text
Authentication Successful ✅
```

---

# 🎯 Authentication Goal

User-এর Identity Verify করা।

---

# 🌐 Authentication Example

Login Form:

```json
{
  "email": "riyad@gmail.com",
  "password": "123456"
}
```

Server Verify করবে:

* Email Correct?
* Password Correct?

---

# Result

```text
Correct → Authenticated ✅

Incorrect → Authentication Failed ❌
```

---

# 🔑 Authentication Methods

---

## 1. Username & Password

সবচেয়ে Common Method।

Example:

* Facebook Login
* Instagram Login
* LinkedIn Login

---

## 2. OTP Authentication

Example:

```text
SMS OTP
Email OTP
```

---

### Banking Example

```text
Password
+
OTP
```

---

## 3. Biometric Authentication

Example:

* Face ID
* Fingerprint
* Retina Scan

---

## 4. Multi-Factor Authentication (MFA)

একাধিক Authentication Method ব্যবহার করা।

Example:

```text
Password
+
OTP
```

---

# 🏗️ Authentication Flow

```text
User
   ↓
Login Form
   ↓
Server
   ↓
Verify Credentials
   ↓
Authenticated
```

---

# 🔥 After Authentication

Server সাধারণত Return করে:

```text
Session ID
```

অথবা

```text
JWT Token
```

---

# JWT Example

```json
{
  "userId": "123",
  "email": "riyad@gmail.com",
  "role": "admin"
}
```

---

# 🔐 What is Authorization (AuthZ)?

Authorization হলো:

```text
Permission Verification Process
```

অর্থাৎ:

```text
তুমি কী করতে পারবে?
```

সেটা Determine করা।

---

# 🏢 Real Life Example

ধরো তুমি অফিসে প্রবেশ করেছো।

এখন প্রশ্ন:

```text
তুমি কোন কোন Room Access করতে পারবে?
```

* HR Room?
* CEO Room?
* Server Room?

---

এই Permission Checking-ই হলো Authorization।

---

# 🎯 Authorization Goal

Determine:

```text
What Resources Can Be Accessed?
```

---

# Authorization Example

User Logged In।

এখন:

```text
Can View Profile?
```

✅ Yes

---

```text
Can Delete All Users?
```

❌ No

---

# Authorization Flow

```text
User
  ↓
Authenticated
  ↓
Permission Check
  ↓
Access Granted / Denied
```

---

# 🔄 Authentication vs Authorization

| Authentication        | Authorization           |
| --------------------- | ----------------------- |
| Who are you?          | What can you do?        |
| Identity Verification | Permission Verification |
| First Step            | Second Step             |
| Login Required        | Permission Required     |
| AuthN                 | AuthZ                   |

---

# 🏗️ Complete Security Flow

```text
User
   ↓
Login
   ↓
Authentication
   ↓
JWT Token
   ↓
Protected Route
   ↓
Authorization
   ↓
Access Granted
```

---

# 🎭 Role-Based Access Control (RBAC)

সবচেয়ে জনপ্রিয় Authorization Model।

---

## Admin

Permissions:

* Create User
* Delete User
* Manage System
* Manage Roles

---

## Manager

Permissions:

* View Team
* Approve Requests

---

## Employee

Permissions:

* View Own Profile
* Update Own Profile

---

## Guest

Permissions:

* View Public Resources

---

# RBAC Example Table

| Role     | Permission       |
| -------- | ---------------- |
| Admin    | Full Access      |
| Manager  | Team Access      |
| Employee | Own Resources    |
| Guest    | Public Resources |

---

# 🔥 Other Authorization Models

---

# 1. RBAC

Role-Based Access Control

Example:

```text
Admin
Manager
Employee
```

---

# 2. ABAC

Attribute-Based Access Control

Based On:

* Department
* Country
* Age
* Location

---

### Example

```text
HR Department
Can Access HR Documents
```

---

# 3. ACL

Access Control List

Example:

```text
Document A

User A → Read
User B → Write
User C → No Access
```

---

# 🌐 Real World Example

---

# Facebook Example

## Authentication

```text
Email
Password
```

Verify Identity।

---

## Authorization

Can:

* Create Post ✅
* Edit Profile ✅

Cannot:

* Delete Facebook Database ❌

---

# Banking System Example

---

## Authentication

```text
Account Number
Password
OTP
```

---

## Authorization

Can:

```text
View Own Account
```

✅

---

Can:

```text
View Another User Account
```

❌

---

# 🔐 JWT Based Authentication

JWT =

```text
JSON Web Token
```

---

# Login Flow

```text
User Login
     ↓
Server Verify
     ↓
JWT Generated
     ↓
JWT Sent To User
```

---

# API Request

```http
Authorization: Bearer JWT_TOKEN
```

---

# JWT Verification

```text
Token Valid?
```

Yes →

```text
Authenticated
```

---

No →

```text
401 Unauthorized
```

---

# 🚨 Common Status Codes

---

# 401 Unauthorized

Meaning:

```text
Authentication Failed
```

Example:

* JWT Missing
* Invalid Token

---

# Response

```http
401 Unauthorized
```

---

# 403 Forbidden

Meaning:

```text
Authenticated But Permission Denied
```

---

# Example

Normal User Trying Admin Route।

---

# Response

```http
403 Forbidden
```

---

# 💻 Express.js Authentication Middleware

```js
const verifyToken = (req, res, next) => {
  const token = req.headers.authorization;

  if (!token) {
    return res.status(401).json({
      message: "Unauthorized",
    });
  }

  next();
};
```

---

# 💻 Express.js Authorization Middleware

```js
const verifyAdmin = (req, res, next) => {
  if (req.user.role !== "admin") {
    return res.status(403).json({
      message: "Forbidden",
    });
  }

  next();
};
```

---

# 🎯 Authentication Technologies

Modern Systems Use:

* Session Authentication
* JWT Authentication
* OAuth 2.0
* OpenID Connect (OIDC)
* SAML
* Multi-Factor Authentication (MFA)

---

# 🎤 Interview Questions & Answers

---

## Q1: What is Authentication?

### Answer

Authentication হলো User Identity Verification Process।

---

## Q2: What is Authorization?

### Answer

Authorization হলো Permission Verification Process।

---

## Q3: Which Comes First?

### Answer

```text
Authentication First
Authorization Second
```

---

## Q4: What is JWT?

### Answer

JWT হলো Secure Token Format যা User Identity Carry করে।

---

## Q5: What is RBAC?

### Answer

Role-Based Access Control।

Role অনুযায়ী Permission Assign করা হয়।

---

## Q6: Difference Between 401 and 403?

### Answer

| 401               | 403                 |
| ----------------- | ------------------- |
| Not Authenticated | Not Authorized      |
| Login Required    | Permission Required |

---

## Q7: Can Authorization Exist Without Authentication?

### Answer

Generally No.

কারণ User কে চিনতে না পারলে Permission Check করা সম্ভব নয়।

---

## Q8: Why JWT Popular?

### Answer

* Stateless
* Scalable
* Fast
* Easy To Use

---

## Q9: What is MFA?

### Answer

Multiple Authentication Factors ব্যবহার করা।

Example:

```text
Password + OTP
```

---

## Q10: What is the Goal of Authentication?

### Answer

Verify:

```text
Who Are You?
```

---

## Q11: What is the Goal of Authorization?

### Answer

Verify:

```text
What Can You Do?
```

---

# 🧠 Final Mental Model

| Concept        | Think Like            |
| -------------- | --------------------- |
| Authentication | Who Are You?          |
| Authorization  | What Can You Do?      |
| JWT            | Identity Card         |
| RBAC           | Role-Based Permission |
| 401            | Login Required        |
| 403            | Permission Denied     |

---

# 🚀 Final Summary

Authentication (AuthN) এবং Authorization (AuthZ) হলো Modern Security Architecture-এর Foundation।

Authentication:

✅ User Identity Verify করে

Authorization:

✅ User Permission Verify করে

Together They Provide:

* Secure Login
* Secure API Access
* Role Management
* Resource Protection
* Enterprise Security

Modern Systems Follow:

```text
Authentication
        ↓
Authorization
        ↓
Access Control
```

Remember:

```text
AuthN = Who Are You?

AuthZ = What Can You Do?
```

এই একটি লাইন Interview-তে Authentication এবং Authorization-এর পুরো Concept মনে রাখতে সাহায্য করবে।
