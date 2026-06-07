# 🚀 Vertical Scaling vs Horizontal Scaling (System Design Notes)

---

# 📌 Introduction

System Design-এ **scaling** হলো এমন একটি technique যার মাধ্যমে আমরা system-এর capacity বাড়াই যাতে বেশি traffic handle করা যায়।

Scaling মূলত দুই ধরনের:

- 📈 Vertical Scaling (Scale Up)
- 📊 Horizontal Scaling (Scale Out)

---

# 📌 1. Vertical Scaling (Scale Up)

## 🎯 What is Vertical Scaling?

একটা single server-এর ক্ষমতা (**CPU**, **RAM**, Storage) বাড়ানোকে Vertical Scaling বলে।

👉 সহজভাবে:

একটা server-কে আরও powerful বানানো।

---

## 🧠 Example

Before:

- **CPU**: 2 Core
- **RAM**: 4 GB

After upgrade:

- **CPU**: 16 Core
- **RAM**: 64 GB

---

## 🏗️ Architecture

```text Users → Single Powerful Server 👍 Advantages সহজ architecture Easy to implement No distributed system complexity 👎 Disadvantages Single point of failure Hardware limit আছে Expensive high-end machine 📌 2. Horizontal Scaling (Scale Out) 🎯 What is Horizontal Scaling?

একাধিক server add করে load distribute করাকে Horizontal Scaling বলে।

👉 সহজভাবে:

অনেকগুলো server দিয়ে system scale করা।

🧠 Example

Traffic বাড়লে:

Server 1
Server 2
Server 3
🏗️ Architecture
Users
  ↓
### Load Balancer
  ↓
Server 1 | Server 2 | Server 3
👍 Advantages
Highly scalable
No single point of failure
Fault tolerant
Cloud friendly
👎 Disadvantages
Complex system design
Data consistency issue
Requires load balancer
⚖️ Vertical vs Horizontal Scaling
Feature	Vertical Scaling	Horizontal Scaling
Approach	Scale Up	Scale Out
Servers	1 powerful server	Multiple servers
Complexity	Low	High
Scalability	Limited	Almost unlimited
Failure Risk	High	Low
Cost	High hardware cost	Cost efficient
☁️ Load Balancer Role

Horizontal scaling-এর মূল component হলো Load Balancer।

👉 এটা decide করে কোন request কোন server-এ যাবে।

Example
### User Request
     ↓
### Load Balancer
  ↓    ↓    ↓
 S1   S2   S3
🔥 Common Algorithms Used

Scaling systems-এ load distribution-এর জন্য কিছু algorithm ব্যবহার হয়:

1️⃣ Round Robin

Sequentialভাবে request distribute করে

2️⃣ Weighted Round Robin

Powerful server বেশি request পায়

3️⃣ Least Connections

যে server কম busy, সেখানে request যায়

4️⃣ IP Hashing

Same user always same server পায়

5️⃣ Auto Scaling Algorithm

Cloud system automatically scale করে based on:

**CPU** usage
Traffic load
Memory usage
🌍 Real World Examples
Company	Scaling Type
Netflix	Horizontal Scaling
YouTube	Horizontal Scaling
Amazon	Horizontal Scaling
Small Startup Apps	Vertical Scaling (early stage)
🧠 Final Mental Model
Vertical Scaling = **ONE** **BIG** **MACHINE** 💪
Horizontal Scaling = **MANY** **MACHINES** 🖥️🖥️🖥️
🚀 Final Summary

Modern systems mostly use:

👉 Horizontal Scaling + Load Balancer + Auto Scaling

Because it provides:

High availability Scalability Fault tolerance Performance stability