# 🚦 Rate Limiting (API Security - Complete Bangla Guide)

Rate Limiting হলো একটি backend security technique যেখানে নির্দিষ্ট সময়ের মধ্যে একজন user, IP বা system কতগুলো request API-তে পাঠাতে পারবে সেটা সীমাবদ্ধ করা হয়।

👉 সহজভাবে বললে:  
একজন user যেন unlimited request পাঠিয়ে server overload বা attack করতে না পারে—সেটাই Rate Limiting।

---

# 🎯 কেন Rate Limiting দরকার?

Rate Limiting API কে বিভিন্ন ধরনের সমস্যা থেকে রক্ষা করে:

- 🚨 DDoS Attack (Server flood)
- 🔐 Brute force login attempt
- 🤖 Bot / scraper abuse
- 📉 Server overload ও crash
- ⚖️ Fair usage নিশ্চিত করা (সব user সমানভাবে resource পায়)

---

# 🧠 Rate Limiting কিভাবে কাজ করে?

Server প্রতিটি request track করে:

- কে request করছে (IP / userId)
- কতবার করছে
- কত সময়ের মধ্যে করছে

তারপর check করে limit cross হয়েছে কিনা।

### 👉 Decision:

- Limit এর মধ্যে → Allow ✅  
- Limit ছাড়িয়ে গেলে → Block ❌  

---

# 🚨 HTTP Status Code

Rate limit exceed হলে সাধারণত response আসে:

```http
HTTP 429 - Too Many Requests

🌐 1. Per Endpoint Rate Limiting

👉 প্রতিটি API route আলাদা আলাদা limit করা হয়।

📌 উদাহরণ:
/login → 5 request / 15 minute
/search → 100 request / minute
/profile → 200 request / minute
🎯 ব্যবহার:
Sensitive API protect করা
Brute force attack prevent করা
👤 2. Per User / IP Rate Limiting

👉 প্রতিটি user বা IP আলাদা track করা হয়।

📌 উদাহরণ:
1 IP → 100 request / minute
1 User → 500 request / minute
🎯 ব্যবহার:
Bot attack prevent করা
Single user abuse stop করা
🌍 3. Global Rate Limiting

👉 পুরো system-এর total request limit করা হয়।

📌 উদাহরণ:
Server capacity: 10,000 req/sec
Global limit: 8,000 req/sec
🎯 ব্যবহার:
Server overload prevent করা
DDoS attack control করা
🛡️ DDoS Mitigation (Layered Security)

Rate limiting সাধারণত ৩ লেয়ারে কাজ করে:

1️⃣ Global Level

👉 পুরো system traffic control করে

2️⃣ Per IP/User Level

👉 attacker identify করে block করে

3️⃣ Endpoint Level

👉 sensitive API protect করে

🧪 Attack Example

ধরো attacker পাঠাচ্ছে:

50,000 requests / second 😱
System Response:
Global limit → extra traffic drop ❌
Per IP limit → attacker block ❌
Login endpoint limit → brute force stop ❌

👉 Result: System safe থাকে ✅

⚙️ Node.js Example (Express)
📦 Install
npm install express-rate-limit
🔧 Basic Setup
import rateLimit from "express-rate-limit";

const limiter = rateLimit({
  windowMs: 1 * 60 * 1000, // 1 minute
  max: 100, // limit each IP to 100 requests
  message: "Too many requests, try again later",
});

app.use(limiter);
🔐 Login Route Specific Limit
const loginLimiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 5, // only 5 attempts
  message: "Too many login attempts, try again later",
});

app.use("/login", loginLimiter);
🧠 Rate Limiting Algorithms

Common algorithms used:

🪣 Token Bucket
⏳ Leaky Bucket
📊 Fixed Window Counter
🔄 Sliding Window Log
🏗️ Production Level Setup

Real-world systems use:

🧠 Redis (distributed tracking)
🚪 API Gateway (Kong / AWS API Gateway)
🌐 Nginx / Load Balancer
☁️ Cloudflare (DDoS protection)
⚠️ Common Mistakes

❌ সব API-তে same limit দেওয়া
❌ শুধু IP-based limiting ব্যবহার করা
❌ Global limit না রাখা
❌ Production-এ unlimited requests রাখা

🎯 Summary

Rate Limiting হলো একটি security mechanism যা API কে abuse, overload এবং DDoS attack থেকে রক্ষা করে।

👉 এটি ৩ লেভেলে কাজ করে:

Endpoint level
User/IP level
Global system level
🚀 One Line Definition

Rate Limiting = API-তে কতবার request করা যাবে সেটা control করে system কে secure ও stable রাখা।