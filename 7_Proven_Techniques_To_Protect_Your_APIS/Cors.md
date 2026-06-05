# 🌐 CORS (Cross-Origin Resource Sharing) - Complete Guide

> A simple, practical and interview-ready Bangla notes on **CORS** for Backend & System Design

---

# 📌 What is CORS?

**CORS** (Cross-Origin Resource Sharing) হলো একটি browser security mechanism যা control করে কোন domain অন্য domain-এর **API** access করতে পারবে।

👉 সহজভাবে বললে:

একটি website অন্য website-এর **API** call করতে পারবে কিনা সেটা **CORS** decide করে।

---

# 🧠 Why CORS Exists?

Browser by default same-origin policy follow করে।

এর মানে:

```text [https://site-a.com](https://site-a.com)  ❌ cannot directly call  [https://site-b.com/api](https://site-b.com/api)

👉 কারণ security risk আছে:

Unauthorized data access **CSRF** attack Data leakage Malicious websites **API** abuse 🚨 Same-Origin Policy (**SOP**)

Browser rule:

👉 Protocol + Domain + Port একই হতে হবে

Example:

[https://example.com](https://example.com) → **SAME** **ORIGIN** [http://example.com](http://example.com) → **DIFFERENT** (protocol change) [https://api.example.com](https://api.example.com) → **DIFFERENT** (subdomain) 🔥 What **CORS** Does?

**CORS** server কে allow করে decide করতে:

Which origins are allowed to access **API**?
🌐 **CORS** Flow (Simple)
Frontend (React App)
        ↓
Browser sends request
        ↓
Backend **API**
        ↓
Server checks Origin
        ↓
Allow / Block response
📦 Example Scenario
Frontend:
[https://frontend.com](https://frontend.com)
Backend:
[https://api.backend.com](https://api.backend.com)

Frontend যদি **API** call করে:

**GET** /users Origin: [https://frontend.com](https://frontend.com) ❌ Without **CORS**

Server response:

Blocked by **CORS** policy 😱

Browser নিজেই request block করে দেয়।

✅ With **CORS** Enabled

Server allows:

Access-Control-Allow-Origin: [https://frontend.com](https://frontend.com)

Then request works ✅

🔐 Important **CORS** Headers ## Access-Control-Allow-Origin

Defines allowed domains:

Access-Control-Allow-Origin: [https://frontend.com](https://frontend.com) ## Access-Control-Allow-Methods

Allowed **HTTP** methods:

**GET**, **POST**, **PUT**, **DELETE** ## Access-Control-Allow-Headers

Allowed custom headers:

Authorization, Content-Type ## Access-Control-Allow-Credentials

Allow cookies / authentication:

true / false 🍪 **CORS** + Cookies Issue

By default cookies cross-origin এ send হয় না।

To enable:

Access-Control-Allow-Credentials: true

Frontend:

fetch(*[https://api.com*,](https://api.com*,) { credentials: *include" }); ⚠️ Common **CORS** Errors ❌ 1. No Access-Control-Allow-Origin Blocked by **CORS** policy ❌ 2. Preflight Failure

**OPTIONS** request fail হলে।

❌ 3. Credentials mismatch

Cookie send হয় না।

🧪 Preflight Request (Very Important)

Browser কিছু request আগে check করে:

👉 **OPTIONS** request

Example:

**OPTIONS** /api/users Why Preflight happens?

When request contains:

Authorization header Non-simple methods (**PUT**, **DELETE**) Custom headers 🏗️ Backend Example (Express.js) import cors from *cors*; import express from *express*;

const app = express();

app.use(cors({
    origin: *[https://frontend.com*,](https://frontend.com*,)
    methods: [*GET*, *POST*, *PUT*, ***DELETE**"],
    credentials: true
}));
🔥 Open **CORS** (**NOT** **SAFE** ❌)
app.use(cors());

👉 This allows **ALL** origins (dangerous in production)

🔐 Secure **CORS** Setup
app.use(cors({
    origin: [*[https://frontend.com*,](https://frontend.com*,) *[https://admin.com*],](https://admin.com*],)
    credentials: true
}));
🌍 Real World Example
App	**CORS** Role
React frontend → Node **API**	Prevent unauthorized **API** access
Banking apps	Block malicious sites
SaaS apps	Secure multi-domain access
🚨 **CORS** vs Security

Important:

👉 **CORS** is **NOT** backend security 👉 It is browser security

⚠️ Attack Misunderstanding

**CORS** does **NOT** stop:

Postman requests Server-to-server calls Curl requests

👉 Only browser blocks cross-origin calls

🧠 Key Mental Model
Concept	Meaning
Origin	Domain + Protocol + Port
**SOP**	Browser restriction rule
**CORS**	Server permission system
Preflight	Browser safety check
🎯 Interview Questions
❓ What is **CORS**?

**CORS** হলো browser security mechanism যা control করে কোন origin **API** access করতে পারবে।

❓ Why do we need **CORS**?

To prevent unauthorized cross-origin access and protect user data.

❓ What is Preflight request?

Browser sent **OPTIONS** request to check permission before actual **API** call.

❓ Is **CORS** a backend security feature?

No. It is a browser-level security mechanism.

❓ Difference between **SOP** and **CORS**?
**SOP**	**CORS**
Browser rule	Server policy
Blocks request	Allows exceptions
🧠 Final Summary

**CORS** হলো একটি browser-based security system যা cross-origin **API** access control করে।

👉 It protects:

User data APIs from unauthorized websites Browser security boundary 🚀 One Line Definition

**CORS** = Browser security mechanism that controls which domains can access your **API**.