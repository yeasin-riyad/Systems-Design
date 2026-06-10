# 🔄 Data Replication - System Design Notes (বাংলা)

## 📌 Data Replication কী?

**Data Replication** হলো এমন একটি Technique যেখানে একই Data-এর একাধিক Copy বিভিন্ন Database Server-এ রাখা হয়।

এর প্রধান উদ্দেশ্য:

* 🚀 High Availability
* ⚡ Better Read Performance
* 🛡️ Fault Tolerance
* 🔥 Disaster Recovery

সহজভাবে,

> **একই Data-এর একাধিক Copy বিভিন্ন Server-এ রাখা = Data Replication**

---

# 🎯 কেন Replication প্রয়োজন?

একটি Database Server-এর উপর পুরো Application নির্ভর করলে Server Crash হওয়ার সাথে সাথে Application Down হয়ে যেতে পারে।

```text
Users
  |
  v
Database Server
```

যদি Database Server Down হয়:

```text
Database ❌
     |
Application ❌
```

এটিকে বলা হয়:

> **Single Point of Failure (SPOF)**

---

# ✅ Replication Solution

```text
                 Primary Database
                         |
            --------------------------
            |                        |
            v                        v

      Replica DB 1            Replica DB 2
```

এখন Primary Database-এর Data Replica Database-গুলোতেও Copy হয়ে থাকবে।

---

# 🧠 How Replication Works

ধরো একজন User Register করলো।

```sql
INSERT INTO users(name)
VALUES('Rahim');
```

### Step 1

Application Write Request পাঠায়।

```text
Application
     |
     v
Primary Database
```

---

### Step 2

Primary Database Data Save করে।

```text
Write Success
```

---

### Step 3

Primary Database Replica Database-এ Data Copy করে।

```text
Primary DB
     |
     +------ Replica 1
     |
     +------ Replica 2
```

---

# 🏗️ Replication Architecture

```text
                    Application
                         |
                         v

                 +---------------+
                 |   Primary DB  |
                 +---------------+
                    /         \
                   /           \
                  v             v

         +---------------+ +---------------+
         |  Replica DB1  | |  Replica DB2  |
         +---------------+ +---------------+
```

---

# ⚡ Benefits of Replication

## 1️⃣ High Availability

Primary Database Down হলে:

```text
Primary DB ❌
```

Replica Database ব্যবহার করা যায়।

```text
Replica DB ✅
```

Application চালু থাকে।

---

## 2️⃣ Read Scalability

ধরো:

```text
10000 Read Requests / Second
```

একটি Database Handle করতে পারছে না।

তখন Read Request Replica-তে পাঠানো হয়।

```text
             Read Requests
                   |
       --------------------------
       |            |           |
       v            v           v

   Replica 1   Replica 2   Replica 3
```

Load ভাগ হয়ে যায়।

---

## 3️⃣ Fault Tolerance

একটি Replica নষ্ট হলে অন্য Replica কাজ করতে পারে।

```text
Replica 1 ❌

Replica 2 ✅

Replica 3 ✅
```

---

## 4️⃣ Disaster Recovery

Primary Server Crash হলেও Replica Database-এ Data থাকে।

ফলে Data Loss-এর ঝুঁকি কমে যায়।

---

# 🧮 Types of Replication

## 1️⃣ Primary-Replica Replication

সব Write Primary Database-এ হবে।

```text
Write
  |
  v
Primary DB
```

সব Read Replica Database থেকে হবে।

```text
Read
  |
  v
Replica DB
```

### Architecture

```text
               Primary
                   |
         -------------------
         |                 |
         v                 v

      Replica 1       Replica 2
```

### Advantages

✅ Easy Setup

✅ Better Read Performance

✅ Widely Used

### Disadvantages

❌ Primary Failure Risk

---

# 2️⃣ Multi-Master Replication

সব Database Read এবং Write Accept করতে পারে।

```text
Database 1  ←→  Database 2
      ↕              ↕
Database 3  ←→  Database 4
```

### Advantages

✅ High Availability

✅ No Single Point of Failure

### Disadvantages

❌ Conflict Resolution Complex

❌ More Difficult to Manage

---

# ⚡ Synchronous Replication

Primary Database Replica-এর Confirmation না পাওয়া পর্যন্ত Commit করবে না।

```text
Write
  |
Primary
  |
Replica ACK
  |
Commit
```

### Advantages

✅ Strong Consistency

### Disadvantages

❌ Higher Latency

❌ Slower Writes

---

# ⚡ Asynchronous Replication

Primary Database আগে Commit করে।

Replica পরে Update হয়।

```text
Write
  |
Primary Commit
  |
Replica Updated Later
```

### Advantages

✅ Faster Writes

✅ Better Performance

### Disadvantages

❌ Replica কিছু সময় পিছিয়ে থাকতে পারে

---

# 🐘 PostgreSQL Replication

PostgreSQL সাধারণত Replication-এর জন্য

**WAL (Write Ahead Log)** ব্যবহার করে।

---

## Write Flow

```text
Application
     |
     v
Primary PostgreSQL
     |
     v
WAL Logs
     |
     v
Replica PostgreSQL
```

---

## Example

Primary Server:

```text
192.168.1.10
```

Replica Server:

```text
192.168.1.20
```

Write Query:

```sql
INSERT INTO users(name)
VALUES('Rahim');
```

প্রথমে Primary Database-এ Save হবে।

তারপর WAL Logs ব্যবহার করে Replica Sync হবে।

---

# 🚨 Challenges of Replication

## 1️⃣ Replication Lag

```text
Primary Updated

Replica Not Updated Yet
```

কিছু সময় Data Mismatch হতে পারে।

---

## 2️⃣ Storage Cost

একই Data একাধিক Server-এ Store করতে হয়।

---

## 3️⃣ Network Dependency

Server-গুলোর মধ্যে Reliable Network প্রয়োজন।

---

## 4️⃣ Failover Complexity

Primary Failure হলে Replica-কে Promote করতে হয়।

---

# ⚔️ Replication vs Sharding

| Feature      | Replication  | Sharding             |
| ------------ | ------------ | -------------------- |
| Goal         | Copy Data    | Split Data           |
| Data         | Same Data    | Different Data       |
| Scaling      | Read Scaling | Read + Write Scaling |
| Availability | High         | Medium               |
| Complexity   | Lower        | Higher               |
| Storage      | More         | Normal               |

---

## Replication

```text
Primary
   |
   +---- Replica 1
   |
   +---- Replica 2
```

সব Database-এ একই Data।

---

## Sharding

```text
Shard 1 → Users 1-1000

Shard 2 → Users 1001-2000

Shard 3 → Users 2001-3000
```

প্রতিটি Database-এ আলাদা Data।

---

# 🏢 Real World Usage

Large Scale Companies:

* Facebook
* Instagram
* Netflix
* Amazon
* YouTube

Replication ব্যবহার করে High Availability এবং Read Scalability নিশ্চিত করে।

---

# 🎤 Interview Answer

**Data Replication হলো এমন একটি Technique যেখানে একই Data-এর একাধিক Copy বিভিন্ন Database Server-এ রাখা হয়। এটি High Availability, Fault Tolerance, Disaster Recovery এবং Read Scalability নিশ্চিত করে। Replication সাধারণত Primary-Replica অথবা Multi-Master Architecture ব্যবহার করে Implement করা হয়। PostgreSQL WAL-based Replication ব্যবহার করে Replica Database Sync রাখে।**

---

# 🔥 Key Takeaways

✅ Same Data Multiple Servers-এ থাকে

✅ Improves Read Performance

✅ Provides High Availability

✅ Supports Disaster Recovery

✅ Reduces Single Point of Failure

✅ PostgreSQL Uses WAL Replication

✅ Common Architectures:

* Primary-Replica
* Multi-Master

---

## 📚 Quick Summary

```text
Write → Primary Database
             |
             v
      Replicate Data
             |
             v
     Multiple Replicas

Result:
✔ High Availability
✔ Better Read Performance
✔ Fault Tolerance
```
