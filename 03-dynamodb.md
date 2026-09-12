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

24-August-2026

31-August-2026

1-September-2026

12-September-2026
