# 🔐 How Applications Manage Permissions


---

# 📚 Table of Contents

* Introduction
* Why Permission Management Matters
* Authentication vs Authorization
* Permission Management Flow
* RBAC (Role-Based Access Control)
* Permission-Based Access Control
* ABAC (Attribute-Based Access Control)
* ACL (Access Control List)
* JWT & Permission Management
* Frontend vs Backend Permission Checks
* Real World Examples
* Interview Questions & Answers
* Final Summary

---

# 🎯 Introduction

প্রতিটি Application-এর একটি গুরুত্বপূর্ণ দায়িত্ব হলো:

```text
Right User
Gets
Right Access
```

এবং

```text
Wrong User
Cannot Access
Protected Resources
```

এই Process-কে বলা হয়:

## Permission Management

অথবা

## Access Control

---

# 🤔 Why Permission Management Matters?

ধরো একটি HR Management System আছে।

---

## Admin Can

* Create Users
* Delete Users
* Manage Payroll
* Change Settings

---

## Manager Can

* Approve Leave
* View Team Reports

---

## Employee Can

* View Own Profile
* Submit Leave Requests

---

এখন যদি Employee Payroll Delete করতে পারে তাহলে?

```text
System Security Broken 😱
```

তাই Permission Management প্রয়োজন।

---

# 🔐 Authentication vs Authorization

অনেক Developer শুরুতে এই দুইটি Concept গুলিয়ে ফেলে।

---

## Authentication (AuthN)

```text
Who Are You?
```

User-এর Identity Verify করা।

---

## Authorization (AuthZ)

```text
What Can You Do?
```

User-এর Permission Verify করা।

---

# Example

```text
Login Success
     ↓
Authentication Complete
     ↓
Permission Check
     ↓
Authorization Complete
```

---

# 🏗️ Permission Management Flow

```text
User Login
     ↓
Authentication
     ↓
Fetch User Role
     ↓
Load Permissions
     ↓
Request Resource
     ↓
Permission Check
     ↓
Access Granted / Denied
```

---

# Step 1: Authentication

User Login করে।

Example:

```json
{
  "email": "riyad@gmail.com",
  "password": "123456"
}
```

---

Server Verify করে:

```text
Email Correct?
Password Correct?
```

---

Result:

```text
Authenticated ✅
```

---

# Step 2: Fetch User Role

Database থেকে Role আনা হয়।

Example:

```json
{
  "id": 1,
  "name": "Riyad",
  "role": "admin"
}
```

---

অথবা

```json
{
  "id": 2,
  "name": "Rahim",
  "role": "employee"
}
```

---

# Step 3: Load Permissions

Role অনুযায়ী Permission Load করা হয়।

---

## Admin

```json
[
  "create_user",
  "delete_user",
  "manage_payroll",
  "manage_roles"
]
```

---

## Employee

```json
[
  "view_profile",
  "apply_leave"
]
```

---

# Step 4: Permission Check

Request:

```http
DELETE /users/123
```

---

Server Check করে:

```text
Has delete_user permission?
```

---

Result:

```text
No ❌
```

---

Response:

```http
403 Forbidden
```

---

# 🏆 RBAC (Role-Based Access Control)

Industry-তে সবচেয়ে বেশি ব্যবহৃত Model।

---

# Core Idea

Permission সরাসরি User-কে দেওয়া হয় না।

---

Instead:

```text
User
 ↓
Role
 ↓
Permissions
```

---

# Example Structure

```text
Admin
 ├── Create User
 ├── Delete User
 ├── Manage Payroll

Manager
 ├── View Team
 ├── Approve Leave

Employee
 ├── View Profile
 ├── Apply Leave
```

---

# Database Design

## Users Table

| ID | Name  | Role     |
| -- | ----- | -------- |
| 1  | Riyad | Admin    |
| 2  | Rahim | Employee |

---

Permission Role থেকে Determine করা হয়।

---

# Advantages

✅ Easy To Implement

✅ Easy To Maintain

✅ Scalable

✅ Industry Standard

---

# Disadvantages

❌ Highly Flexible নয়

❌ Complex Enterprise Rules Handle করা কঠিন

---

# 🔥 Permission-Based Access Control

এখানে User-এর মধ্যে Direct Permission Store করা হয়।

---

Example:

```json
{
  "name": "Riyad",
  "permissions": [
    "create_user",
    "delete_user"
  ]
}
```

---

Check:

```text
delete_user exists?
```

---

Result:

```text
Access Granted ✅
```

---

# Advantages

Very Flexible

---

# Disadvantages

Large System-এ Manage করা কঠিন।

---

# 🚀 ABAC (Attribute-Based Access Control)

Enterprise Security Systems-এ জনপ্রিয়।

---

Decision নেয়:

* Department
* Location
* Age
* Country
* Time

---

# Example

Policy:

```text
Only HR Department
Can Access Payroll
```

---

User:

```json
{
  "department": "HR"
}
```

---

Access:

```text
Allowed ✅
```

---

User:

```json
{
  "department": "Engineering"
}
```

---

Access:

```text
Denied ❌
```

---

# 📄 ACL (Access Control List)

Specific Resource-এর জন্য Permission Store করা হয়।

---

Example

Document:

```text
Salary_Report.pdf
```

---

Permissions:

```text
Riyad → Read + Write

Rahim → Read

Karim → No Access
```

---

# ACL Structure

```text
Resource
    ↓
User Permission Mapping
```

---

# 🔑 JWT & Permission Management

Modern APIs সাধারণত JWT ব্যবহার করে।

---

# Login Success

JWT Generated:

```json
{
  "userId": "123",
  "role": "admin"
}
```

---

# Request

```http
Authorization: Bearer JWT_TOKEN
```

---

# Server Flow

```text
Verify JWT
     ↓
Extract Role
     ↓
Permission Check
```

---

# Example

Role:

```text
Admin
```

---

Route:

```http
DELETE /users/123
```

---

Permission:

```text
Allowed ✅
```

---

# 💻 Express.js Example

## Role Based Middleware

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

# Generic Permission Middleware

```js
const checkPermission = (permission) => {
  return (req, res, next) => {

    if (!req.user.permissions.includes(permission)) {
      return res.status(403).json({
        message: "Permission Denied",
      });
    }

    next();
  };
};
```

---

# Usage

```js
app.delete(
  "/users/:id",
  checkPermission("delete_user")
);
```

---

# 🎨 Frontend Permission Check

Example:

```jsx
{
  user.role === "admin" && (
    <button>Delete User</button>
  );
}
```

---

# ⚠️ Important

Frontend Security নয়।

কারণ:

```text
Frontend Can Be Manipulated
```

---

Real Security:

```text
Backend Authorization
```

---

# 🏢 Enterprise Architecture

```text
User
  ↓
Authentication
  ↓
JWT
  ↓
API Gateway
  ↓
Authorization Layer
  ↓
Microservices
  ↓
Database
```

---

# 🌍 Real World Examples

| System           | Permission Model |
| ---------------- | ---------------- |
| Facebook         | RBAC             |
| GitHub           | RBAC             |
| Google Workspace | RBAC + ACL       |
| AWS IAM          | RBAC + ABAC      |
| Google Drive     | ACL              |
| Enterprise ERP   | RBAC + ABAC      |

---

# 🎤 Interview Questions

---

## Q1: How Does An Application Manage Permissions?

### Answer

Application প্রথমে User Authenticate করে, তারপর User Role অথবা Permissions Load করে এবং Resource Access করার আগে Authorization Check করে।

---

## Q2: What Is RBAC?

### Answer

Role-Based Access Control।

User → Role → Permissions

---

## Q3: Why Is RBAC Popular?

### Answer

* Easy Management
* Scalable
* Industry Standard
* Easy To Understand

---

## Q4: What Is ABAC?

### Answer

Attribute-Based Access Control।

Permission Attributes-এর উপর নির্ভর করে।

---

## Q5: What Is ACL?

### Answer

Access Control List।

Resource অনুযায়ী User Permission Store করা হয়।

---

## Q6: Why Backend Authorization Is Mandatory?

### Answer

কারণ Frontend Manipulate করা যায়।

Security সবসময় Backend-এ Enforce করতে হয়।

---

## Q7: What Status Code Is Used For Permission Denied?

### Answer

```http
403 Forbidden
```

---

## Q8: What Status Code Is Used For Authentication Failure?

### Answer

```http
401 Unauthorized
```

---

# 🧠 Final Mental Model

```text
User Login
     ↓
Authentication
     ↓
Get Role
     ↓
Load Permissions
     ↓
Request Resource
     ↓
Authorization Check
     ↓
Allow / Deny
```

---

# 🚀 Final Summary

Modern Applications Permission Management করার জন্য সাধারণত:

✅ Authentication

✅ Authorization

✅ RBAC

✅ JWT

✅ Permission Middleware

ব্যবহার করে।

Most Common Industry Approach:

```text
User
 ↓
Role
 ↓
Permissions
```

অর্থাৎ:

```text
RBAC (Role-Based Access Control)
```

এটি Simple, Secure, Scalable এবং Maintain করা সহজ।

---

# 🔥 Golden Interview Line

```text
Authentication Identifies The User.

Authorization Determines What The User Can Do.
```

এবং

```text
Permissions Are Enforced By The Authorization Layer.
```
