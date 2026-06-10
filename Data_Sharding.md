# 🧩 Data Sharding - System Design Notes (বাংলা)

## 📌 Data Sharding কী?

**Data Sharding** হলো একটি Database Scaling Technique যেখানে একটি বড় Database কে ছোট ছোট অংশে (**Shards**) ভাগ করে বিভিন্ন Server-এ সংরক্ষণ করা হয়।

এর ফলে:

* 🚀 Performance বৃদ্ধি পায়
* 📈 Scalability বৃদ্ধি পায়
* ⚡ Query দ্রুত হয়
* 🛡️ Fault Isolation পাওয়া যায়

সহজভাবে,

> **একটি বড় Database → একাধিক ছোট Database (Shards) → বিভিন্ন Server-এ Store করা = Data Sharding**

---

# 🏪 Real Life Example

ধরো তোমার একটি E-commerce Application আছে:

* 10 Million Users
* 50 Million Orders

একটি Database আর সব Request Handle করতে পারছে না।

তাই Database কে Shard করা হলো।

```text
Shard 1 → Users A - F
Shard 2 → Users G - M
Shard 3 → Users N - Z
```

এখন:

```text
A - F Users → Shard 1

G - M Users → Shard 2

N - Z Users → Shard 3
```

---

# 🧠 Architecture Diagram

```text
             Application Server
                     |
     ----------------------------------
     |                |               |
     v                v               v

+------------+  +------------+  +------------+
|  Shard 1   |  |  Shard 2   |  |  Shard 3   |
| Users A-F  |  | Users G-M  |  | Users N-Z  |
+------------+  +------------+  +------------+
```

---

# 🔍 Sharding কেন প্রয়োজন?

## ❌ Without Sharding

```text
          Application
                |
                v
       +----------------+
       | Single Database|
       +----------------+
                |
      Too Many Requests
                |
          Slow / Crash
```

### Problems

* High Latency
* CPU Overload
* Memory Pressure
* Disk Bottleneck
* Limited Scaling
* Single Point of Failure

---

## ✅ With Sharding

```text
          Application
                |
      --------------------
      |        |         |
      v        v         v

   Shard1   Shard2   Shard3
```

### Benefits

* Faster Queries
* Better Performance
* Horizontal Scaling
* Reduced Load
* Better Availability
* Fault Isolation

---

# ⚙️ How Sharding Works

## Step 1: Choose a Shard Key

Shard Key হলো এমন একটি Field যার মাধ্যমে Data বিভিন্ন Shard-এ ভাগ করা হবে।

Common Examples:

```text
user_id
email
country
order_id
customer_id
```

---

## Step 2: Apply Sharding Logic

ধরো:

```text
user_id % 3
```

Result:

```text
User 1 → Shard 1

User 2 → Shard 2

User 3 → Shard 3

User 4 → Shard 1

User 5 → Shard 2
```

এভাবে Data Automatically বিভিন্ন Shard-এ ছড়িয়ে যাবে।

---

# 🧮 Types of Sharding

## 1️⃣ Range-Based Sharding

Data Range অনুযায়ী Shard করা হয়।

### Example

```text
User ID 1 - 1000      → Shard 1

User ID 1001 - 2000   → Shard 2

User ID 2001 - 3000   → Shard 3
```

### Advantages

✅ Easy to understand

✅ Easy to implement

### Disadvantages

❌ Hotspot Problem

❌ Uneven Traffic Distribution

---

## 2️⃣ Hash-Based Sharding

Hash Function ব্যবহার করে Shard নির্ধারণ করা হয়।

### Formula

```text
shard = hash(user_id) % total_shards
```

### Example

```text
User 101 → Shard 2

User 102 → Shard 1

User 103 → Shard 3
```

### Advantages

✅ Even Data Distribution

✅ Better Load Balancing

### Disadvantages

❌ Re-sharding Complex

❌ Data Migration Difficult

---

## 3️⃣ Directory-Based Sharding

একটি Lookup Service বা Directory বলে দেয় Data কোন Shard-এ আছে।

### Example

```text
User 123 → Shard 3

User 456 → Shard 1

User 789 → Shard 2
```

### Advantages

✅ Flexible

✅ Easy Migration

### Disadvantages

❌ Directory Failure Risk

❌ Extra Lookup Cost

---

# 🏬 E-Commerce Example

ধরো একটি Global Shopping Platform আছে।

## User Data

```text
Shard 1 → Bangladesh Users

Shard 2 → India Users

Shard 3 → USA Users
```

---

## Order Data

```text
Shard 1 → Low Value Orders

Shard 2 → Medium Value Orders

Shard 3 → High Value Orders
```

---

# ⚡ Sharding vs Partitioning

| Feature       | Sharding           | Partitioning     |
| ------------- | ------------------ | ---------------- |
| Server Count  | Multiple Servers   | Single Server    |
| Scaling Type  | Horizontal Scaling | Vertical Scaling |
| Performance   | High               | Medium           |
| Data Location | Distributed        | Same Machine     |
| Complexity    | Higher             | Lower            |

---

# 🚨 Challenges of Sharding

## 1️⃣ Cross-Shard Joins

```text
User Table → Shard 1

Order Table → Shard 3
```

Join করতে Multiple Server Access করতে হয়।

ফলে Query Slow হতে পারে।

---

## 2️⃣ Re-Sharding

নতুন Shard যোগ করলে Existing Data Redistribute করতে হয়।

```text
Shard 1
Shard 2
Shard 3

↓ Add New Shard

Shard 1
Shard 2
Shard 3
Shard 4
```

এটি Complex এবং Costly।

---

## 3️⃣ Hotspot Problem

খারাপ Shard Key নির্বাচন করলে:

```text
Shard 1 → 80% Traffic

Shard 2 → 10% Traffic

Shard 3 → 10% Traffic
```

একটি Shard Overloaded হয়ে যায়।

---

## 4️⃣ Consistency Issues

Data Multiple Server-এ থাকায়:

* Synchronization
* Transactions
* Consistency

Maintain করা কঠিন হয়ে যায়।

---

# 🏗️ Real World Architecture

```text
                  Users
                     |
                     v
              Load Balancer
                     |
                     v
              Application Layer
                     |
     ----------------------------------
     |                |               |
     v                v               v

+------------+  +------------+  +------------+
|  Shard 1   |  |  Shard 2   |  |  Shard 3   |
+------------+  +------------+  +------------+
```

---

# 🎤 Interview Answer

**Data Sharding হলো একটি Database Scaling Technique যেখানে বড় Database কে ছোট ছোট Shard-এ ভাগ করে বিভিন্ন Server-এ রাখা হয়। এটি Horizontal Scaling, High Performance এবং Better Availability নিশ্চিত করে। Sharding সাধারণত Range-Based, Hash-Based এবং Directory-Based হতে পারে। তবে Cross-Shard Query, Re-Sharding এবং Consistency Challenges মোকাবিলা করতে হয়।**

---

# 🔥 Key Takeaways

✅ Large Database → Multiple Shards

✅ Improves Performance

✅ Supports Horizontal Scaling

✅ Reduces Database Load

✅ Uses Shard Key

✅ Types:

* Range-Based
* Hash-Based
* Directory-Based

✅ Used by Large Scale Systems

* Facebook
* Amazon
* Google
* Uber
* Netflix

---

## 📚 Quick Summary

```text
Large Database
       |
       v
Choose Shard Key
       |
       v
Split Data
       |
       v
Store Across Multiple Servers
       |
       v
Better Performance + Scalability
```
