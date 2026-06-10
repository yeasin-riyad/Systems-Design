# 🌍 CDN (Content Delivery Network) - System Design Notes (বাংলা)

## 📌 CDN কী?

**CDN (Content Delivery Network)** হলো পৃথিবীর বিভিন্ন Location-এ ছড়িয়ে থাকা Server-এর একটি Network, যা User-এর সবচেয়ে কাছের Server থেকে Content Deliver করে।

CDN মূলত Static Content Cache করে রাখে, যেমন:

* Images
* CSS
* JavaScript
* Fonts
* Videos
* PDFs

সহজভাবে,

> **User-এর কাছাকাছি Server থেকে Content Serve করার মাধ্যমে Website Fast করার Technology হলো CDN।**

---

# 🎯 CDN কেন প্রয়োজন?

ধরো তোমার Website-এর Main Server Singapore-এ Host করা আছে।

```text
Origin Server
(Singapore)
```

কিন্তু User আছে:

```text
Bangladesh
India
Germany
USA
Australia
```

যদি সবাই Singapore Server থেকে Data Fetch করে:

```text
User
  |
Internet
  |
Singapore Server
```

তাহলে:

❌ High Latency

❌ Slow Loading

❌ Increased Server Load

❌ Poor User Experience

---

# ✅ CDN Solution

CDN পৃথিবীর বিভিন্ন Location-এ Content-এর Copy Store করে রাখে।

```text
                Origin Server
                  (Singapore)

                       |
    ------------------------------------------
    |                   |                    |
    v                   v                    v

 CDN Node          CDN Node            CDN Node
 (India)           (Germany)           (USA)
```

এখন User সবচেয়ে কাছের CDN Node থেকে Content পাবে।

---

# 🧠 Real Life Example

ধরো Netflix-এর একটি Movie আছে।

### Without CDN

```text
Bangladesh User → USA Server

India User → USA Server

Germany User → USA Server
```

Result:

❌ Buffering

❌ Slow Streaming

---

### With CDN

```text
Bangladesh User → Singapore CDN

India User → Mumbai CDN

Germany User → Frankfurt CDN
```

Result:

✅ Faster Streaming

✅ Better Experience

---

# 🏗️ How CDN Works?

ধরো Website-এ একটি Image আছে:

```text
https://example.com/logo.png
```

---

## First Request (Cache Miss)

```text
User
  |
CDN
  |
Image Not Found ❌
  |
Origin Server
  |
Fetch Image
  |
Store in CDN Cache
  |
Return Response
```

---

## Second Request (Cache Hit)

```text
User
  |
CDN
  |
Image Found ✅
  |
Return Response
```

Origin Server-এ যেতে হবে না।

---

# 📦 Origin Server কী?

Origin Server হলো তোমার Main Server যেখানে Original Content Store করা থাকে।

Examples:

* VPS
* Dedicated Server
* Cloud Server
* Kubernetes Cluster

---

## Architecture

```text
User
  |
CDN
  |
Origin Server
```

---

# 🌎 Global CDN Architecture

```text
                       Users

       ----------------------------------------
       |                 |                    |
       v                 v                    v

 Bangladesh         Germany               USA
    User             User                User

       |                 |                    |

       v                 v                    v

 CDN Node         CDN Node            CDN Node
  (India)         (Germany)           (USA)

        \             |              /
         \            |             /
          \           |            /
           v          v           v

              Origin Server
```

---

# 📁 What CDN Caches?

## Commonly Cached

```text
Images

CSS Files

JavaScript Files

Fonts

Videos

Audio Files

PDF Files
```

---

## Usually Not Cached

```text
User Profile

Shopping Cart

Bank Account

Private Dashboard

Authentication Data
```

কারণ এগুলো Dynamic Content।

---

# 🚀 Benefits of CDN

## 1️⃣ Faster Website Loading

User কাছের Server থেকে Content পায়।

```text
Short Distance
      ↓
Low Latency
      ↓
Fast Website
```

---

## 2️⃣ Reduced Origin Server Load

```text
Users
  |
 CDN
  |
Origin Server
```

সব Request Main Server-এ যায় না।

---

## 3️⃣ Better Scalability

Millions of Users Handle করা সহজ হয়।

---

## 4️⃣ High Availability

একটি CDN Node Down হলেও অন্য Node Serve করতে পারে।

---

## 5️⃣ DDoS Protection

অনেক CDN Provider Built-in Security দেয়।

```text
DDoS Mitigation

Rate Limiting

Web Application Firewall
```

---

# ⚡ Cache Hit vs Cache Miss

## Cache Hit

```text
User
  |
CDN
  |
Data Found ✅
```

Benefits:

✅ Fast Response

✅ No Origin Access

---

## Cache Miss

```text
User
  |
CDN
  |
Data Not Found ❌
  |
Origin Server
```

First Request সাধারণত Cache Miss হয়।

---

# 🏪 E-Commerce Example

ধরো Amazon-এর Product Image:

```text
iphone-16-pro.jpg
```

---

## Without CDN

```text
Bangladesh User
       |
USA Server
```

High Latency

---

## With CDN

```text
Bangladesh User
       |
India CDN Node
```

Low Latency

---

# 🛠 Popular CDN Providers

## Cloudflare

Features:

✅ Global Network

✅ Free Plan

✅ DDoS Protection

---

## Akamai

Features:

✅ Enterprise CDN

✅ Massive Global Coverage

---

## Fastly

Features:

✅ Real-Time Cache Control

✅ High Performance

---

## AWS CloudFront

Features:

✅ AWS Integration

✅ Global Edge Locations

---

## Google Cloud CDN

Features:

✅ Google Network

✅ High-Speed Delivery

---

# 🔄 CDN Request Flow

```text
1. User Requests Image

          |
          v

2. CDN Checks Cache

          |
    ----------------
    |              |
    v              v

Cache Hit      Cache Miss
    |              |
    |              v
    |       Origin Server
    |              |
    |      Store in Cache
    |              |
    ---------------
          |
          v

3. Return Response
```

---

# ⚔️ CDN vs Cache

| Feature  | Cache            | CDN               |
| -------- | ---------------- | ----------------- |
| Scope    | Local            | Global            |
| Purpose  | Faster Access    | Global Delivery   |
| Location | Same Application | Worldwide Network |
| Example  | Redis            | Cloudflare        |

---

# ⚔️ CDN vs Load Balancer

| CDN                 | Load Balancer       |
| ------------------- | ------------------- |
| Delivers Content    | Distributes Traffic |
| Caches Static Files | Routes Requests     |
| Global Edge Servers | Backend Servers     |
| Reduces Latency     | Balances Load       |

---

# 🏗️ Real World Architecture

```text
                    Users
                       |
                       v

                 CDN (Cloudflare)
                       |
                       v

                 Load Balancer
                       |
                       v

               Application Servers
                       |
                       v

                    Database
```

---

# 🎤 Interview Answer

**CDN (Content Delivery Network) হলো পৃথিবীর বিভিন্ন Location-এ থাকা Edge Server-এর Network, যা User-এর কাছাকাছি Server থেকে Static Content Deliver করে। এর ফলে Website Faster হয়, Latency কমে, Origin Server-এর Load কমে এবং High Availability নিশ্চিত হয়। CDN সাধারণত Images, CSS, JavaScript, Videos এবং অন্যান্য Static Assets Cache করে রাখে।**

---

# 🔥 Key Takeaways

✅ CDN = Global Distributed Cache

✅ User-এর কাছের Server ব্যবহার করে

✅ Website Faster করে

✅ Latency কমায়

✅ Origin Server Load কমায়

✅ Supports Millions of Users

✅ DDoS Protection দেয়

---

# 📚 One Line Memory Trick

```text
Cache = Fast Storage

CDN = Global Cache Network
```

---

# 🎯 System Design Interview Shortcut

```text
Caching       = Speed 🚀

CDN           = Global Speed 🌍

Replication   = Availability 🛡️

Sharding      = Scalability 📈

Load Balancer = Traffic Distribution ⚖️
```
