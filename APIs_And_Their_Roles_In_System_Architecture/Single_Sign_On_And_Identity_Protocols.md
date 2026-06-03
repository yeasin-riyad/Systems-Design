# 🔐 SSO (Single Sign-On) & Identity Protocols Complete Guide

> Beginner to Advanced Notes for System Design & Backend Interviews
> Written in Bangla 🇧🇩

---

# 📚 Table of Contents

* What is SSO?
* Why SSO Needed?
* SSO Architecture
* Identity Provider (IdP)
* Service Provider (SP)
* OAuth 2.0
* OpenID Connect (OIDC)
* SAML
* OAuth vs OIDC vs SAML
* Real World Examples
* Interview Questions & Answers
* Final Summary

---

# 🌟 What is SSO (Single Sign-On)?

SSO এর পূর্ণরূপ:

```text
Single Sign-On
```

SSO এমন একটি authentication mechanism যেখানে:

```text
একবার Login করে
একাধিক Application ব্যবহার করা যায়
```

---

# 🌍 Real Life Example

ধরো তুমি Google Account দিয়ে Login করলে।

এরপর তুমি access করতে পারো:

* Gmail
* YouTube
* Google Drive
* Google Docs
* Google Photos

পুনরায় Login করতে হয় না।

কারণ:

```text
One Login → Multiple Applications
```

এটাই SSO।

---

# ❌ Without SSO

```text
Login Gmail
Login YouTube
Login Drive
Login Docs
```

প্রতিটি Application-এর জন্য আলাদা Login প্রয়োজন।

---

# ✅ With SSO

```text
Login Once
     ↓
Access Everything
```

---

# 🎯 Why SSO Needed?

Modern organizations এ শত শত applications থাকে।

Example:

* HR System
* Payroll System
* CRM
* Email
* Internal Dashboard

প্রতিটি system-এ আলাদা Login করা User Experience খারাপ করে।

SSO এই সমস্যা সমাধান করে।

---

# 🚀 Benefits of SSO

## Better User Experience

একবার Login।

---

## Less Password Fatigue

অনেক Password মনে রাখতে হয় না।

---

## Better Security

Centralized Authentication।

---

## Easy User Management

এক জায়গা থেকে User Access Control করা যায়।

---

## Faster Onboarding

নতুন Employee-এর Access সহজে Configure করা যায়।

---

# 🏗️ SSO Architecture

```text
             User
               |
               v
      Identity Provider
            (IdP)
               |
      ------------------
      |       |        |
      v       v        v
    Gmail   Drive    Docs
```

---

# Important Components

## User

যে Login করছে।

---

## Identity Provider (IdP)

Authentication Verify করে।

Examples:

* Google Identity
* Microsoft Entra ID
* Okta
* Auth0

---

## Service Provider (SP)

যে Application Identity Provider কে Trust করে।

Examples:

* Gmail
* Slack
* Salesforce
* Notion

---

# 🔄 SSO Login Flow

## Step 1

User visits:

```text
myapp.com
```

---

## Step 2

Click:

```text
Continue with Google
```

---

## Step 3

Redirect:

```text
accounts.google.com
```

---

## Step 4

Google verifies credentials।

---

## Step 5

Google issues token।

---

## Step 6

User Logged In ✅

---

# 🔐 Identity Protocols

SSO Implement করার জন্য কিছু Standard Protocol ব্যবহার করা হয়।

Most Popular:

1. OAuth 2.0
2. OpenID Connect (OIDC)
3. SAML

---

# 1️⃣ OAuth 2.0

## What is OAuth?

OAuth হলো:

```text
Authorization Protocol
```

---

# Problem OAuth Solves

ধরো Canva তোমার Google Drive Access করতে চায়।

Password Share করা Dangerous।

OAuth বলে:

```text
Password না দিয়ে
Permission দাও
```

---

# OAuth Example

```text
Login with Google
Connect Google Drive
Connect GitHub
```

---

# OAuth Roles

## Resource Owner

User

---

## Client

Application

Example:

```text
Canva
```

---

## Authorization Server

Google

---

## Resource Server

Google APIs

---

# OAuth Flow

```text
User
  ↓
Client App
  ↓
Authorization Server
  ↓
Access Token
  ↓
Protected API
```

---

# OAuth Provides

```text
Access Token
```

Password দেয় না।

---

# ⚠️ Important

OAuth Authentication Protocol না।

OAuth হলো:

```text
Authorization Protocol
```

---

# 2️⃣ OpenID Connect (OIDC)

## What is OIDC?

OIDC হলো:

```text
OAuth 2.0 + Authentication Layer
```

---

# Why OIDC Needed?

OAuth বলে:

```text
What user can access
```

OIDC বলে:

```text
Who the user is
```

---

# Example

User clicks:

```text
Login With Google
```

Application জানতে চায়:

* Name
* Email
* Profile Picture

OIDC এই Identity Information দেয়।

---

# OIDC Tokens

## Access Token

API Access-এর জন্য।

---

## ID Token

User Identity-এর জন্য।

---

# Example ID Token

```json
{
  "name": "Riyad",
  "email": "riyad@gmail.com"
}
```

---

# OIDC Flow

```text
User
   ↓
Google Login
   ↓
ID Token
   ↓
Application
```

---

# Modern Authentication

আজকের প্রায় সব SaaS Application ব্যবহার করে:

```text
OAuth 2.0 + OIDC
```

---

# 3️⃣ SAML

## Full Form

```text
Security Assertion Markup Language
```

---

# What is SAML?

Enterprise Authentication Protocol।

---

# Data Format

```text
XML
```

ব্যবহার করে।

---

# Common Use Cases

* Enterprise SSO
* Government Systems
* Banking Systems
* Large Organizations

---

# Example

একটি Company Employee Login করে Access পায়:

* HR Portal
* Payroll System
* Email
* Internal Dashboard

সবকিছু এক Login দিয়ে।

---

# SAML Architecture

```text
User
   ↓
Identity Provider
   ↓
SAML Assertion
   ↓
Service Provider
```

---

# SAML Assertion

Identity Proof।

Example:

```xml
<User>
   <Name>Riyad</Name>
</User>
```

---

# OAuth vs OIDC vs SAML

| Feature            | OAuth 2.0 | OIDC     | SAML    |
| ------------------ | --------- | -------- | ------- |
| Authentication     | ❌         | ✅        | ✅       |
| Authorization      | ✅         | ✅        | Limited |
| Format             | JSON      | JWT/JSON | XML     |
| Mobile Friendly    | ✅         | ✅        | ❌       |
| Modern Apps        | ✅         | ✅        | Less    |
| Enterprise Systems | Medium    | Medium   | High    |

---

# 🎯 When Should You Use What?

## OAuth

When:

```text
Need API Access Permission
```

---

## OIDC

When:

```text
Need User Login
```

---

## SAML

When:

```text
Enterprise SSO Required
```

---

# 🌍 Real World Examples

| System                     | Protocol     |
| -------------------------- | ------------ |
| Login with Google          | OAuth + OIDC |
| Login with Facebook        | OAuth + OIDC |
| Login with GitHub          | OAuth + OIDC |
| Microsoft Enterprise Login | SAML / OIDC  |
| Enterprise HR Systems      | SAML         |
| Modern SaaS Platforms      | OIDC         |

---

# 🏢 Enterprise Example

```text
Employee
    ↓
Microsoft Entra ID
    ↓
SSO Token
    ↓
CRM System

    ↓

HR System

    ↓

Payroll System

    ↓

Email System
```

একবার Login।

সব Application Accessible।

---

# 🎤 Interview Questions & Answers

---

## Q1: What is SSO?

### Answer

Single Sign-On হলো এমন একটি Authentication System যেখানে একবার Login করে Multiple Applications Access করা যায়।

---

## Q2: What are the Benefits of SSO?

### Answer

* Better User Experience
* Less Passwords
* Centralized Authentication
* Easy User Management

---

## Q3: What is OAuth?

### Answer

OAuth হলো Authorization Protocol যা Password Share না করে Application-কে Permission দেয়।

---

## Q4: What is OIDC?

### Answer

OIDC হলো OAuth 2.0-এর উপর Build করা Authentication Layer।

---

## Q5: Difference Between OAuth and OIDC?

| OAuth         | OIDC                           |
| ------------- | ------------------------------ |
| Authorization | Authentication + Authorization |
| Access Token  | Access Token + ID Token        |
| API Access    | User Login                     |

---

## Q6: What is SAML?

### Answer

SAML হলো Enterprise-Level XML-Based Authentication Protocol।

---

## Q7: Which Protocol is Used in Login with Google?

### Answer

```text
OAuth 2.0 + OpenID Connect (OIDC)
```

---

## Q8: What is an Identity Provider (IdP)?

### Answer

যে System User Authentication Manage করে।

Example:

* Google
* Microsoft Entra ID
* Okta

---

## Q9: What is a Service Provider (SP)?

### Answer

যে Application Identity Provider-এর Authentication Trust করে।

---

## Q10: Which Protocol is Most Common in Modern SaaS Applications?

### Answer

```text
OpenID Connect (OIDC)
```

---

# 🧠 Final Mental Model

| Concept | Think Like                    |
| ------- | ----------------------------- |
| SSO     | Login Once, Access Everywhere |
| OAuth   | Permission Delegation         |
| OIDC    | User Identity Verification    |
| SAML    | Enterprise Authentication     |
| IdP     | Authentication Authority      |
| SP      | Trusted Application           |

---

# 🚀 Final Summary

Modern Authentication Systems-এর Foundation হলো:

✅ SSO

✅ OAuth 2.0

✅ OpenID Connect (OIDC)

✅ SAML

Together they provide:

* Secure Login
* Centralized Authentication
* Enterprise Identity Management
* Better User Experience
* Scalable Access Control

Every Modern Enterprise System relies on these technologies for Authentication and Authorization.
