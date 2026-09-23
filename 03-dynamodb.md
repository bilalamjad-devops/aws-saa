**Partition key and Cardinality:**


Problem: Database ka Write Capacity Units (WCU) unevenly consume ho raha hai. Iska matlab hai ke data kisi ek jagah bohot ziada ja raha hai (jisey hum AWS mein Hot Partition kehte hain), aur baki partitions khali pade hain.

We should use select those keys as partitioning keys that have high cardinality 


Example:

We have Users Table. The columns are:

- User_ID (e.g., USR-101, USR-102, USR-103...)
- Country (e.g., Pakistan, USA, UK...)
- Status (e.g., Active, Inactive...)

Low-Cardinality (Bad Partition Key): 

We select Country or Status as Partition Keys:

Why: Values will repeat (hazaron users ka country "Pakistan" ya status "Active" hoga).

Result: AWS background mein "Pakistan" waali saari request ek hi server/partition par bhej dega. Woh server over-load ho jayega (Hot Partition).

High-Cardinality (Good Partition Key):

If we select User_ID as Partition Key:

Wajah: Har row/record ke andar jo value hai woh bilkul distinct/unique hai.

Nateeja: AWS har User_ID ke data ko alag-alag physical servers par barabar (spread) kar ke store karega. Dynamic workload perfectly balance ho jayega.


### Exam rule 🧠

> **DynamoDB performance problem + uneven workload / hot partitions → choose a high-cardinality partition key.**

**High cardinality = many unique values → better distribution.**

**Low cardinality = few unique values → risk of hot partitions.**


# 🧠 Exam shortcut

When you see:

**"Key-value store"**

👉 **DynamoDB**

When you see:

**"Document database / document model"**

👉 **DynamoDB**

When you see:

**"Relational / SQL"**

👉 **RDS / Aurora**

When you see:

**"Collaborate/edit/share documents"**

👉 **WorkDocs**

---

### Q15 in one line:

> **The application needs a key-value/document database → DynamoDB.**

Don't overthink the ECS/Fargate part. **The database requirement is the giveaway.**


<img width="658" height="406" alt="2018-10-23_05-24-29-74b3e6dadc8ce683ccd2a5bd00f99889" src="https://github.com/user-attachments/assets/11de6d8a-d642-44b5-a6b0-dca0915fd1e2" />


# 13. The most important concepts from this question

You can put this tiny table in your notes:

| Requirement                                  | Service                       |
| -------------------------------------------- | ----------------------------- |
| Private access to DynamoDB from VPC          | **DynamoDB Gateway Endpoint** |
| Private access to S3 from VPC                | **S3 Gateway Endpoint**       |
| Restore DynamoDB to an earlier point in time | **PITR**                      |
| Cross-account DynamoDB backup                | **AWS Backup**                |
| Time-series data                             | **Amazon Timestream**         |
| Network traffic inspection/firewall          | **AWS Network Firewall**      |

---

<img width="1105" height="804" alt="amazon-dynamodb-gateway-endpoint (1)" src="https://github.com/user-attachments/assets/7c77137e-f155-456e-992a-fd0311b206f8" />

---
---
---

**Amazon DynamoDB** AWS ki sab se popular **fully managed, serverless, key-value aur document NoSQL database service** hai.

AWS SAA-C03 exam mein DynamoDB se related questions aksar scale, performance, global availability, aur cost optimization ke scenarios par poochhe jate hain.

---

## 1. Core Architecture & High Availability

* **Fully Serverless:** Aap ko koi OS, server, ya cluster manage nahi karna padta. Infrastructure, patching, aur auto-scaling AWS khud handle karta hai.
* **Built-in Multi-AZ Replication:** Jab aap DynamoDB table banate hain, toh AWS aap ke data ko ek hi AWS Region ke **3 physical Availability Zones (AZs)** mein automatically replicate karta hai. Is se high availability aur durability natively milti hai.
* **Single-Digit Millisecond Latency:** Scaling chahe 10 requests per second ki ho ya 10 million requests per second ki, DynamoDB consistent performance maintain rakhta hai.

---

## 2. Capacity Modes (Exam Favorite)

DynamoDB mein do capacity modes hote hain jin ka choose karna workload par depend karta hai:

| Feature | **Provisioned Capacity Mode** | **On-Demand Capacity Mode** |
| --- | --- | --- |
| **How It Works** | Aap pehle se define karte hain ke aap ko kitne **RCUs (Read Capacity Units)** aur **WCUs (Write Capacity Units)** chahiye. | AWS scale-up aur scale-down automatically handle karta hai (no RCU/WCU planning needed). |
| **Best For** | Predictable, consistent traffic (jin ka pattern pehle se pata ho). | Unpredictable / sudden traffic spikes (e.g., flash sales, voting apps). |
| **Cost Strategy** | Cheaper for stable workloads. Supports Reserved Capacity for extra discounts. | Pay-per-request model. Higher cost per request, but zero cost when idle. |

---

## 3. Primary Keys & Secondary Indexes

DynamoDB items (rows) ko identify aur fast-query karne ke liye primary keys aur indexes ka role bohot important hai:

1. **Partition Key (PK) / HASH:**
* Single attribute jo data ko internal SSD partitions mein distribute karta hai.


2. **Sort Key (SK) / RANGE:**
* Partition Key ke sath mil kar Composite Primary Key banata hai, jo data ko partition ke andar order mein organize karta hai.



#### **Secondary Indexes (Querying non-primary attributes):**

* **Local Secondary Index (LSI):**
* Same Partition Key, lekin **Different Sort Key**.
* Single partition tak limited hota hai. Must be created **ONLY at table creation time**.


* **Global Secondary Index (GSI):**
* **Different Partition Key AND Different Sort Key**.
* Table banne ke baad kisi bhi waqt create kiya ja sakta hai. Complete table-wide querying ki capability deta hai.



---

## 4. Advanced DynamoDB Features for SAA-C03

Exam ke scenario-based questions mein yeh specific features aksar trigger hote hain:

```
┌─────────────────────────────────────────────────────────────────────────┐
│                      DYNAMODB KEY EXTENSIONS                            │
├──────────────────────────┬──────────────────────┬───────────────────────┤
│ DAX (Accelerator)        │ DynamoDB Streams     │ Global Tables         │
│ In-memory cache for      │ Real-time change data│ Active-Active         │
│ microsecond latency.     │ capture for Lambda/S3│ Multi-Region sync.    │
└──────────────────────────┴──────────────────────┴───────────────────────┘

```

1. **DynamoDB Accelerator (DAX):**
* Fully managed, highly available **in-memory cache** specially built for DynamoDB.
* **Exam Trigger:** *"Reduce read latency from milliseconds to microseconds"* $\rightarrow$ **DAX**.


2. **DynamoDB Streams:**
* Table mein hone wali har create, update, ya delete operation ka **time-ordered event log** capture karta hai.
* **Exam Trigger:** *"Trigger an AWS Lambda function when a database item is added or updated"* $\rightarrow$ **DynamoDB Streams + Lambda**.


3. **Global Tables:**
* Fully managed **Multi-Region, Active-Active** database replication.
* **Exam Trigger:** *"Provide multi-region low-latency access and disaster recovery with active-active setup"* $\rightarrow$ **DynamoDB Global Tables**.


4. **Time To Live (TTL):**
* Automatic deletion mechanism jo expire hone wale items ko zero cost / zero write capacity consumption par remove karta hai.
* **Exam Trigger:** *"Automatically delete session logs / temporary data older than 30 days without consuming write throughput"* $\rightarrow$ **DynamoDB TTL**.



---

## 5. Exam Decision Matrix (DynamoDB Cheat Sheet)

* **NoSQL + High Scale + Key-Value/Document + Millisecond Latency:** $\rightarrow$ **DynamoDB**
* **Microsecond Read Performance:** $\rightarrow$ **DAX (DynamoDB Accelerator)**
* **Real-time Event Processing on DB Changes:** $\rightarrow$ **DynamoDB Streams**
* **Multi-Region Active-Active Replication:** $\rightarrow$ **DynamoDB Global Tables**
* **Auto-expire temporary records:** $\rightarrow$ **TTL (Time to Live)**


---
---
---

<img width="804" height="778" alt="ddb_as_set_read_1" src="https://github.com/user-attachments/assets/d3e1473b-a0ea-4301-9d93-33cf43fcc4c2" />


Aap ka concept **DAX** ke hawale se bilkul clear ho gaya hai! Ab aayein samajhte hain ke **API Gateway Caching** aur **DAX Caching** mein kya farq hai aur dono alag-alag level par kaise kaam karti hain.

---

### Architecture Mein Caching Kahan Hoti Hai?

Sochein aap ki application ek multi-layer architecture hai:

```
[ Mobile Game / User ]
         │
         ▼
 ┌─────────────────┐
 │   API Gateway   │  ◄── 1. API Gateway Cache (Restricts hits to Lambda)
 └────────┬────────┘
          │
          ▼
 ┌─────────────────┐
 │ AWS Lambda      │
 └────────┬────────┘
          │
          ▼
 ┌─────────────────┐
 │  DynamoDB (DAX) │  ◄── 2. DAX Cache (Restricts hits to DynamoDB Disk)
 └─────────────────┘

```

---

### 1. API Gateway Caching (Frontend / API Layer Cache)

**API Gateway Caching** poori **HTTP API response** ko cache karti hai.

* **Kaise kaam karti hai?** Jab mobile game API Gateway ko koi request bhejta hai (e.g., `GET /leaderboard`), toh API Gateway response ko apne paas save kar leta hai.
* **Fayda:** Agli baar jab koi user same request bhejega, toh API Gateway **Lambda function ko execute kiye bina** aur **DynamoDB ko touch kiye bina** direct response return kar dega.
* **Main Benefit:**
* **Cost Reduction:** Lambda function ke run execution charges bach jate hain.
* **Response Speed:** Round-trip time bohot kam ho jata hai.



---

### 2. DynamoDB Accelerator - DAX (Database Layer Cache)

**DAX** sirf aur sirf **DynamoDB database queries/reads** ko cache karta hai.

* **Kaise kaam karti hai?** Jab Lambda function DynamoDB se data mangta hai (e.g., `GetItem` ya `Query`), toh request pehle DAX mein jati hai. Agar data DAX mein hai, toh mil jata hai; agar nahi hai, toh DAX DynamoDB se la kar save karta hai.
* **Fayda:** Lambda function chalega aur code execute hoga, lekin DynamoDB database disk par load nahi padega.
* **Main Benefit:**
* **Microsecond Latency:** Query response time milliseconds se drop ho kar **microseconds** ho jata hai.
* **Database RCU Saving:** DynamoDB ki Read Capacity Units (RCU) consume nahi hoti.



---

### Comparison Table (Quick Summary)

| Feature | **API Gateway Caching** | **DynamoDB Accelerator (DAX)** |
| --- | --- | --- |
| **Kya Cache Hota Hai?** | Poora HTTP API Response. | Specific Database Items / Queries. |
| **Kahan Hota Hai?** | System ke Frontend (API) level par. | System ke Database level par. |
| **Lambda Run Hota Hai?** | ❌ Nahi (Lambda execution bypass ho jata hai). | ✅ Haan (Lambda run hota hai, par DB saved rehta hai). |
| **Main Objective** | Traffic ko Lambda tak pohenchne se rokna. | DB Reads ko **microseconds** speed dena. |

---

### Exam Rule of Thumb:

* Agar question bole: *"Cache API responses to reduce Lambda execution costs"* $\rightarrow$ **API Gateway Caching**
* Agar question bole: *"In-memory cache for DynamoDB to get microsecond read latency"* $\rightarrow$ **DynamoDB Accelerator (DAX)**

---
---
---


Absolutely. For **AWS SAA**, DynamoDB questions usually revolve around these concepts. Since you want short revision, focus on these:

## 🎯 DynamoDB — SAA Must-Know Concepts

### 1. What is DynamoDB?

**Fully managed NoSQL database** designed for very high performance and scalability.

* Key-value + document database
* Serverless
* Millisecond latency
* Automatically scales
* NoSQL → **not SQL**

**Exam clue:**
`NoSQL + massive scale + low latency → DynamoDB`

---

### 2. Primary Key ⭐⭐⭐

Two types:

**Simple primary key**

```text
Partition Key
```

**Composite primary key**

```text
Partition Key + Sort Key
```

Example:

```text
UserID = 123        ← Partition Key
OrderID = 456       ← Sort Key
```

**Shortcut:**
Partition key decides **where data is stored**.
Sort key organizes **related items**.

---

### 3. Query vs Scan ⭐⭐⭐

**Query**

* Searches using a specific partition key
* Efficient
* Preferred

**Scan**

* Examines the entire table
* Expensive/slower
* Avoid when possible

**Shortcut:**
`Known partition key → Query`
`Need entire table → Scan`

---

### 4. Provisioned vs On-Demand Capacity ⭐⭐⭐

**Provisioned**

* You specify RCU/WCU
* Can use **DynamoDB Auto Scaling**
* Good for predictable workloads

**On-Demand**

* Pay per request
* Automatically handles capacity
* Good for unpredictable/spiky workloads

**Shortcut:**
`Provisioned + changing traffic → Auto Scaling`

`Unpredictable traffic → On-Demand`

---

### 5. RCU and WCU ⭐⭐⭐

**WCU = Write Capacity Unit**

**RCU = Read Capacity Unit**

Think:

```text
Write → WCU
Read  → RCU
```

Don't confuse them with storage.

---

### 6. DynamoDB Auto Scaling ⭐⭐⭐

Automatically adjusts **provisioned RCU/WCU** based on demand.

Example:

```text
Normal traffic
     ↓
Low capacity

Traffic spike
     ↓
Auto Scaling
     ↓
More RCU/WCU
```

**Exam clue:**
`Provisioned DynamoDB + throttling during traffic peaks → Auto Scaling`

---

### 7. DynamoDB Accelerator (DAX) ⭐⭐⭐

**DAX = in-memory cache for DynamoDB.**

It reduces read latency from approximately:

```text
milliseconds → microseconds
```

Useful when the application repeatedly reads the same data.

**Shortcut:**
`DynamoDB + extremely low read latency → DAX`

---

### 8. DynamoDB Streams ⭐⭐⭐

Captures changes made to a DynamoDB table.

Example:

```text
DynamoDB
   ↓
DynamoDB Streams
   ↓
Lambda
   ↓
SNS / SQS / other processing
```

Can capture:

* INSERT
* MODIFY
* REMOVE

**Exam clue:**
`When item changes → trigger something → DynamoDB Streams + Lambda`

---

### 9. Global Tables ⭐⭐⭐

For **multi-Region DynamoDB**.

Example:

```text
Region A DynamoDB
       ↕
Global Tables
       ↕
Region B DynamoDB
```

Provides:

* Multi-Region replication
* Low-latency access globally
* Disaster recovery
* Active-active architecture

**Shortcut:**
`DynamoDB + users globally distributed → Global Tables`

---

### 10. Local Secondary Index (LSI)

Alternative sort key while keeping the **same partition key**.

```text
Same Partition Key
Different Sort Key
```

Important:

* Created when the table is created
* Same partition key as base table

**Shortcut:**
`LSI = Same PK, different SK`

---

### 11. Global Secondary Index (GSI) ⭐⭐⭐

Allows querying using a **different partition key**.

```text
Table:
PK = UserID

GSI:
PK = Email
```

Important:

* Different partition key allowed
* Can have different sort key
* Can be created/modified after table creation

**Shortcut:**

```text
LSI → same PK
GSI → different PK
```

This is a **very common SAA question**.

---

### 12. Eventually Consistent vs Strongly Consistent Reads

**Eventually consistent**

* Default
* May briefly return older data
* Lower read capacity cost

**Strongly consistent**

* Returns latest data
* Higher RCU consumption

**Shortcut:**
`Need latest data immediately → Strongly Consistent Read`

---

### 13. DynamoDB Transactions

Provides **ACID transactions** across multiple items/tables.

Useful when several changes must either:

```text
ALL succeed
OR
ALL fail
```

**Exam clue:**
`Multiple DynamoDB operations must be atomic → Transactions`

---

### 14. TTL — Time to Live

Automatically deletes expired items.

Example:

```text
Session expires
     ↓
TTL
     ↓
DynamoDB eventually removes it
```

Useful for:

* Temporary data
* Sessions
* Expiring records
* Old logs

**Shortcut:**
`Automatically remove expired DynamoDB items → TTL`

---

### 15. DynamoDB Backup ⭐⭐

Two important options:

**Point-in-Time Recovery (PITR)**

* Continuous backups
* Restore to a specific point in time

**On-demand backup**

* Manual backup
* Long-term retention

**Shortcut:**
`Restore to any point in time → PITR`

---

### 16. DynamoDB Encryption

DynamoDB encrypts data **at rest** by default.

Can use:

* AWS owned key
* AWS managed KMS key
* Customer managed KMS key

**Exam clue:**
`DynamoDB encryption at rest → KMS`

---

### 17. DynamoDB + Lambda ⭐⭐⭐

Very common architecture:

```text
DynamoDB
   ↓
Streams
   ↓
Lambda
   ↓
Process change
```

Example:

> When a new order is inserted, automatically send notification.

→ **DynamoDB Streams + Lambda**

---

### 18. DynamoDB + API Gateway

Common serverless architecture:

```text
Client
  ↓
API Gateway
  ↓
Lambda
  ↓
DynamoDB
```

No EC2 required.

---

### 19. DynamoDB + AppSync

AWS AppSync is a managed service for building APIs, commonly with **GraphQL**.

Example:

```text
Mobile/Web App
      ↓
   AppSync
      ↓
 DynamoDB
```

**Exam clue:**
`GraphQL + DynamoDB → AppSync`

---

### 20. Hot Partition ⭐⭐

If too many requests go to the same partition key, you can get a **hot partition**.

Bad design:

```text
Partition Key = "USA"
```

Millions of requests all targeting `"USA"`.

Better partition-key design distributes traffic.

**Shortcut:**
`Uneven traffic → hot partition`

---

# 🔥 Highest-Priority DynamoDB Topics

If you're short on time, memorize these **10 first**:

| Concept            | Exam shortcut            |
| ------------------ | ------------------------ |
| Primary Key        | PK + optional SK         |
| Query              | Specific PK              |
| Scan               | Entire table             |
| Auto Scaling       | Provisioned capacity     |
| DAX                | Microsecond cached reads |
| Streams            | Changes → Lambda         |
| Global Tables      | Multi-Region             |
| GSI                | Different PK             |
| LSI                | Same PK                  |
| Strong Consistency | Latest data              |

### 🧠 One-line DynamoDB memory map

**DynamoDB = NoSQL → Query → RCU/WCU → Auto Scaling → DAX → Streams → Global Tables → GSI/LSI → Consistency → TTL/PITR.**

These are the areas I'd expect you to see repeatedly in **SAA practice questions**.

---
---
---

### 5. Cheat Sheet for Database Event Triggers (SAA-C03)

* **Detect new items / updates in DynamoDB & trigger Lambda:** $\rightarrow$ **DynamoDB Streams**
* **Detect S3 object uploads & trigger Lambda:** $\rightarrow$ **S3 Event Notifications**
* **Detect AWS API calls / Resource state changes:** $\rightarrow$ **Amazon EventBridge (CloudWatch Events)**

---
24-August-2026

31-August-2026

1-September-2026

12-September-2026

16-September-2026

18-September-2026

23-September-2026
