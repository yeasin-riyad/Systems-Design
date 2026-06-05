# 🌐 CORS (Cross-Origin Resource Sharing) - Complete Guide

> A simple, practical and interview-ready Bangla notes on CORS for Backend & System Design

---

# 📌 What is CORS?

CORS (Cross-Origin Resource Sharing) হলো একটি browser security mechanism যা control করে কোন domain অন্য domain-এর API access করতে পারবে।

👉 সহজভাবে বললে:

একটি website অন্য website-এর API call করতে পারবে কিনা সেটা CORS decide করে।

---

# 🧠 Why CORS Exists?

Browser by default same-origin policy follow করে।

এর মানে:

```text
https://site-a.com  ❌ cannot directly call  https://site-b.com/api

# কারণ security risk আছে:

- Unauthorized data access
- CSRF attack
- Data leakage
- Malicious websites API abuse

## 🚨 Same-Origin Policy (SOP)

### Browser rule:

👉 Protocol + Domain + Port একই হতে হবে

### Example:

- `https://example.com` → **SAME ORIGIN**
- `http://example.com` → **DIFFERENT** (protocol change)
- `https://api.example.com` → **DIFFERENT** (subdomain)

## 🔥 What CORS Does?

CORS server কে allow করে decide করতে:
- Which origins are allowed to access API?

## 🌐 CORS Flow (Simple)

```plaintext
Frontend (React App)
        ↓
Browser sends request
        ↓
Backend API
        ↓
Server checks Origin
        ↓
Allow / Block response
```

## 📦 Example Scenario
Frontend: `https://frontend.com`
Backend: `https://api.backend.com`

Frontend যদি API call করে:
```http request
get /users 
Origin: https://frontend.com 
```
❌ Without CORS:
> Server response: Blocked by CORS policy 😱
> Browser নিজেই request block করে দেয়।
✅ With CORS Enabled:
> Server allows: Access-Control-Allow-Origin: https://frontend.com 
and then request works ✅

## 🔐 Important CORS Headers
1. **Access-Control-Allow-Origin**
   - Defines allowed domains:
   - `Access-Control-Allow-Origin: https://frontend.com`
2. **Access-Control-Allow-Methods**
   - Allowed HTTP methods:
   - GET, POST, PUT, DELETE
3. **Access-Control-Allow-Headers**
   - Allowed custom headers:
   - Authorization, Content-Type
4. **Access-Control-Allow-Credentials**
   - Allow cookies / authentication:
   - true / false  							 	 	 	 	 	  
take care of cross-origin cookies.
default cookies cross-origin এ send হয় না। To enable:`