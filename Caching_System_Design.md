# 🚀 Caching - System Design Notes (বাংলা)

## 📌 Caching কী?

**Caching** হলো এমন একটি Performance Optimization Technique যেখানে Frequently Accessed Data-কে Fast Storage (Cache)-এ Temporary Store করা হয়, যাতে পরবর্তীতে একই Data খুব দ্রুত পাওয়া যায়।

সহজভাবে,

> **বারবার প্রয়োজন হয় এমন Data-কে RAM বা Fast Storage-এ রেখে দ্রুত Serve করাই হলো Caching।**

---

# 🎯 কেন Caching দরকার?

ধরো তোমার Application-এ:

* 1 Million Users
* 100,000 Requests প্রতি মিনিটে

যদি প্রতিটি Request Database-এ যায়:

```text
User
  |
  v
Database
  |
Response
```

তাহলে:

❌ Database Overload হবে

❌ Response Slow হবে

❌ Application Scalability কমে যাবে

---

## ✅ With Cache

```text
User
  |
Cache
  |
Response
```

Database-এর উপর Load অনেক কমে যায়।

---

# 🧠 Real Life Example

ধরো তুমি প্রতিদিন একই বই পড়ো।

### Without Cache

```text
Bookshelf
   |
Find Book
   |
Read
```

প্রতিবার বই খুঁজতে সময় লাগবে।

---

### With Cache

```text
Table
  |
Read Directly
```

অনেক দ্রুত বই পাবে।

---

### Analogy

```text
Bookshelf = Database

Table = Cache
```

---

# 🏗️ Basic Caching Architecture

```text
                User
                  |
                  v

            Application
                  |
          ----------------
          |              |
          v              v

        Cache       Database
```

---

# ⚙️ How Caching Works?

## First Request (Cache Miss)

ধরো User Product List Request করলো।

```text
User
  |
Application
  |
Cache
  |
Data Not Found ❌
  |
Database
  |
Data Found ✅
  |
Store in Cache
  |
Return Response
```

---

## Second Request (Cache Hit)

```text
User
  |
Application
  |
Cache
  |
Data Found ✅
  |
Return Response
```

Database Access করার প্রয়োজন নেই।

---

# 🎯 Cache Hit vs Cache Miss

## Cache Hit

```text
Data Found in Cache
```

Benefits:

✅ Faster Response

✅ No Database Query

✅ Low Latency

---

## Cache Miss

```text
Data Not Found in Cache
```

Result:

❌ Database Query Needed

❌ Higher Latency

---

# 📊 Performance Example

Database Query:

```text
500 ms
```

Cache Query:

```text
5 ms
```

Result:

```text
100x Faster
```

---

# 🔥 Types of Caching

## 1️⃣ Client-Side Cache

Browser Data Store করে।

```text
Browser Cache
```

Examples:

* Images
* CSS
* JavaScript Files
* Fonts

---

## 2️⃣ CDN Cache

Static Content User-এর কাছাকাছি Server-এ Store হয়।

```text
User
  |
CDN
  |
Origin Server
```

Examples:

* Images
* Videos
* Static Files

---

## 3️⃣ Application Cache

Application Layer-এ Cache রাখা হয়।

```text
Application
     |
   Redis
```

সবচেয়ে জনপ্রিয় Approach।

---

## 4️⃣ Database Cache

Database Query Result Cache করা হয়।

```text
Query Result
     |
   Cache
```

---

# 🛠 Popular Caching Technologies

## Redis

Redis

Features:

✅ In-Memory

✅ Extremely Fast

✅ Supports Expiration

✅ Distributed

---

## Memcached

Memcached

Features:

✅ Lightweight

✅ High Performance

✅ Easy Setup

---

# 🏪 E-Commerce Example

ধরো:

```http
GET /products
```

---

## First Request

```text
Cache Miss
     |
Database Query
     |
Store in Cache
     |
Return Response
```

---

## Next Requests

```text
Cache Hit
     |
Return Directly
```

Database Access প্রয়োজন হবে না।

---

# ⚡ Cache Eviction Policies

Cache Memory Full হয়ে গেলে কোন Data Remove করা হবে?

---

## 1️⃣ LRU (Least Recently Used)

সবচেয়ে বেশি সময় ব্যবহার হয়নি এমন Data Remove করা হয়।

```text
Oldest Used Data
       |
     Remove
```

সবচেয়ে জনপ্রিয় Policy।

---

## 2️⃣ LFU (Least Frequently Used)

যে Data সবচেয়ে কমবার Access হয়েছে।

```text
Least Accessed
      |
    Remove
```

---

## 3️⃣ FIFO (First In First Out)

যে Data প্রথমে এসেছে সেটি আগে Remove হবে।

```text
First Added
     |
Remove First
```

---

# 🧮 Caching Strategies

## 1️⃣ Cache Aside (Lazy Loading)

সবচেয়ে জনপ্রিয় Strategy।

```text
Check Cache
     |
Not Found
     |
Database
     |
Save to Cache
```

### Advantages

✅ Easy Implementation

✅ Efficient

---

## 2️⃣ Write Through

```text
Write
  |
Cache
  |
Database
```

Cache এবং Database একসাথে Update হয়।

### Advantages

✅ Strong Consistency

### Disadvantages

❌ Slower Writes

---

## 3️⃣ Write Back

```text
Write
  |
Cache
  |
Later Database
```

### Advantages

✅ Fast Writes

### Disadvantages

❌ Risk of Data Loss

---

# 🚨 Caching Challenges

## 1️⃣ Cache Invalidation

ধরো Database Update হলো:

```sql
UPDATE products
SET price = 1500;
```

কিন্তু Cache-এ এখনও:

```text
1200
```

তাহলে Wrong Data Return হবে।

---

## 2️⃣ Cache Consistency

Database এবং Cache Sync রাখা কঠিন।

---

## 3️⃣ Memory Cost

Cache সাধারণত RAM ব্যবহার করে।

RAM Storage Expensive।

---

## 4️⃣ Cache Stampede

একই সময়ে অনেক Request Cache Miss করলে:

```text
Thousands of Requests
         |
      Database
```

Database Overload হতে পারে।

---

# 🏗️ Real World Architecture

```text
                    Users
                       |
                       v

                Load Balancer
                       |
                       v

                Application
                       |
             ------------------
             |                |
             v                v

           Redis        PostgreSQL
           Cache        Database
```

---

# ⚔️ Caching vs Replication vs Sharding

| Feature    | Caching        | Replication        | Sharding             |
| ---------- | -------------- | ------------------ | -------------------- |
| Goal       | Speed          | Availability       | Scalability          |
| Stores     | Temporary Data | Same Data Copies   | Split Data           |
| Improves   | Response Time  | High Availability  | Read & Write Scaling |
| Storage    | RAM            | Multiple Databases | Multiple Databases   |
| Complexity | Medium         | Medium             | High                 |

---

# 🏢 Real World Usage

Popular Companies Using Caching:

* Facebook
* Instagram
* Netflix
* Amazon
* YouTube
* Spotify

---

# 🎤 Interview Answer

**Caching হলো একটি Performance Optimization Technique যেখানে Frequently Accessed Data-কে Fast Storage (Cache)-এ Temporary Store করা হয়। এর ফলে Database Load কমে যায় এবং Response Time অনেক দ্রুত হয়। Cache Hit হলে Data Cache থেকে পাওয়া যায় এবং Cache Miss হলে Database থেকে Data এনে Cache-এ Store করা হয়। Redis এবং Memcached সবচেয়ে জনপ্রিয় Caching Solutions।**

---

# 🔥 Key Takeaways

✅ Frequently Used Data Cache-এ রাখা হয়

✅ Database Load কমে যায়

✅ Response Time Improve হয়

✅ User Experience Better হয়

✅ Popular Tools:

* Redis
* Memcached

✅ Popular Strategies:

* Cache Aside
* Write Through
* Write Back

✅ Popular Policies:

* LRU
* LFU
* FIFO

---

## 📚 One Line Memory Trick

```text
Database = Source of Truth

Cache = Fast Temporary Copy
```

---

## 🎯 System Design Interview Shortcut

```text
Caching     = Speed 🚀

Replication = Availability 🛡️

Sharding    = Scalability 📈
```
