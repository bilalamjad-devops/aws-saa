**RDS Event:** "Something happened to my database service."

```rdsevent
Instance failure
Failover
Backup
Maintenance
Configuration changes
```



**Aurora Lambda integration:** "Something happened to data inside my database."

```auroraLambdaIntegration
INSERT
UPDATE
DELETE
```


**Multi-AZ:** Standby + Synchronous + HA

**Read Replica:** Read scaling + Asynchronous

**RDS Read Replica =** DynamoDB Global Tables


## Exam shortcut 🧠

When you see:

**“frequent schema changes”**

→ **DynamoDB**

When you see:

**“complex relationships / SQL / transactions”**

→ **RDS / Aurora**

When you see:

**“high-performance relational database”**

→ **Aurora**

When you see:

**“data warehouse / OLAP / analytics”**

→ **Redshift**

When you see:

**“massive scale + millisecond/low-latency + NoSQL”**

→ **DynamoDB**

### For Question 52:

**Frequent schema changes** → NoSQL
**High traffic** → DynamoDB
**Low latency** → DynamoDB
**Global scalability** → DynamoDB

✅ **Answer: Amazon DynamoDB**



## 6. Your SAA memory table

| Service/concept           | Think                                   |
| ------------------------- | --------------------------------------- |
| **IAM Role**              | Give AWS permissions to EC2             |
| **STS**                   | Temporary AWS credentials               |
| **IAM DB Authentication** | Temporary authentication token for RDS  |
| **SSL/TLS**               | Encrypt data in transit                 |
| **Secrets Manager**       | Store/rotate database passwords/secrets |
| **RDS Multi-AZ**          | High availability                       |
| **RDS Read Replica**      | Read scaling                            |


### 🎯 Shortcut

| If question says...      | Think...                     |
| ------------------------ | ---------------------------- |
| RDS primary fails        | **Multi-AZ failover**        |
| Standby becomes primary  | **Automatic**                |
| What changes?            | **CNAME/DNS**                |
| New DB created?          | ❌ No, standby already exists |
| IP address switched?     | ❌ No                         |
| Main purpose of Multi-AZ | **High availability**        |

**One-line memory:**

> 🧠 **RDS Multi-AZ failure = Standby promoted + CNAME/DNS points to it.**

<img width="500" height="498" alt="rds_ha_5 (1)" src="https://github.com/user-attachments/assets/28269856-5893-48a5-be42-f6b46ac16e1f" />

---

**RDS Proxy:** manage and scale database connections 

<img width="713" height="481" alt="amazon-rds-proxy" src="https://github.com/user-attachments/assets/fdbbeee7-deca-4402-9273-b6819ea7ae63" />

**Amazon RDS Proxy** ek aisa intermediary (beech ka bridge) hai jo aap ki application aur aap ke RDS database ke darmiyan baithta hai aur **Database Connections ko manage/pool** karta hai.

Simple lafzon mein: Yeh database ke aage khada ek **"Traffic Controller"** ya **"Gatekeeper"** hai.

---

### **1. Real-Life Analogy (Bank Teller Example)**

* **Bina RDS Proxy Ke (Direct Connection):**
Agar 1,000 log ek sath bank mein ghus jayein aur har banda alag teller (cashier) maange, toh teller pareshan ho jayenge aur bank system crash kar jayega.
* **RDS Proxy Ke Sath (Connection Pooling):**
Bank ke bahar ek manager (RDS Proxy) khada hai. Woh 1,000 logon ko line mein khada karta hai aur jaise hi koi 1 teller free hota hai, agli qataar wale ko wahan bhej deta hai. Fast, managed, aur bina crash hue!

---

### **2. RDS Proxy Ki 3 Badi Wajaat (Why Use It?)**

1. **Connection Pooling (Database Crash Hone Se Bachana):**
Serverless functions (jaise **AWS Lambda**) jab bohot zyada scale hoti hain, toh hazaron direct database connections khol deti hain, jis se RDS ki CPU/RAM exhaust ho jati hai. RDS Proxy un hazaron connections ko **reuse** karta hai.
2. **Faster Failover Time (66% Faster):**
Agar Multi-AZ setup mein primary database fail ho jaye, toh RDS Proxy application ko disconnect nahi hone deta balke silently backend par standby DB par shift kar deta hai (Failover time bohot Kam kar deta hai).
3. **Better Security (IAM Integration):**
Aap application ko DB credentials (username/password) dene ke bajaye **AWS IAM Authentication** aur **AWS Secrets Manager** se secure connect karwa sakte hain.

---

### **3. Exam Cheat Sheet (AWS SAA-C03 Shortcuts)**

* **Keywords: "Serverless / Lambda connecting to RDS", "Database Connection Exhaustion", "Connection Pooling":** $\rightarrow$ **Amazon RDS Proxy**
* **Keywords: "Reduce database failover time for applications":** $\rightarrow$ **Amazon RDS Proxy**


### 🎯 What is being tested?

**Read Replica vs Multi-AZ**

### ✅ Correct answers — Select TWO

**1. It elastically scales out beyond the capacity constraints of a single DB instance for read-heavy database workloads.**

**2. Provides asynchronous replication and improves the performance of the primary database by taking read-heavy database workloads from it.**

### 🔑 Key concept

**Read Replica = Read scaling**

Primary DB → **asynchronous replication** → Read Replica(s) → handle read queries

This reduces the read workload on the primary DB and allows **horizontal read scaling**.

### ❌ Key distinction

**Multi-AZ** → **high availability**

* Synchronous replication
* Automatic failover
* Not primarily for read scaling

### 🔥 Exam shortcut

> **Read Replica = scale READS + asynchronous**
> **Multi-AZ = HA/failover + synchronous**


12-September-2026

## 4. Exam Decision Matrix (RDS Read Replica vs Multi-AZ Cheat Sheet)

* **Scale READ queries / reporting workload:** $\rightarrow$ **Read Replicas**
* **Replication Type for Read Replicas:** $\rightarrow$ **Asynchronous**
* **High Availability (HA) & Automatic Failover:** $\rightarrow$ **Multi-AZ**
* **Replication Type for Multi-AZ Standby:** $\rightarrow$ **Synchronous**

---

24-August-2026

27-August-2026

28-August-2026

30-August-2026

5-September-2026

11-September-2026

12-September-2026
