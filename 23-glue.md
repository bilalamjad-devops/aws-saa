Yes — this question is actually testing one very specific **AWS Glue feature**.

### 🎯 What is the question saying?

The bank has:

```text
S3
 ↓
XML financial data
```

Every day, **new data is added**.

But their Glue ETL job does this:

```text
Day 1:
100 files → process all 100

Day 2:
20 new files added

Glue processes:
120 files ❌
```

So Glue is **processing old data again and again**.

The bank wants:

```text
Day 1:
100 files → process 100

Day 2:
20 new files → process ONLY 20 ✅

Day 3:
10 new files → process ONLY 10 ✅
```

This saves **processing time and resources**.

---

### ✅ Correct answer: Enable job bookmarks

**AWS Glue Job Bookmarks** allow Glue to **remember what data it has already processed**.

Think of a bookmark like a **bookmark in a book** 📖.

If you read pages 1–100 today, you put a bookmark at page 100.

Tomorrow:

> "Continue from where I stopped."

Similarly:

```text
First run:
S3 files 1–100
       ↓
Glue processes them
       ↓
Bookmark remembers them

Next run:
S3 files 1–100 + 101–120
                  ↑
          Process only new data
```

So:

> **Job Bookmark = remembers previously processed data and helps process only new/changed data.**

---

### ❌ Why the other answers?

**Glue Data Quality**

Used to check whether data is **valid/accurate/complete**.

Example:

> Is `customer_id` present?  
> Is age within an expected range?

It doesn't solve repeated processing.

---

**FindMatches ML Transform**

Used to find **matching/duplicate records**.

Example:

```text
John Smith, 123 Main St
John Smith, 123 Main Street
```

It can identify that they may represent the same person.

Not for tracking previously processed files.

---

**NumberOfWorkers = 3**

Only changes the **amount of compute capacity**.

It doesn't tell Glue:

> "Don't process the old files."

---

### 🔥 SAA shortcut

When you see:

> **Glue keeps processing the same old data + want only new/changed data**

Immediately think:

**👉 Glue Job Bookmarks** ✅

### 🧠 One-line memory

**Job Bookmark = "Glue, remember what you already processed."**

---
---
---

* **Crawler:** Scans S3/DB to find schemas.
* **Data Catalog:** Stores the schemas as tables.
* **Glue Job:** Executes the Python/Spark code to **Extract, Transform, and Load** the actual data.

---

# 📊 Final Revision Table

| Requirement / Keyword              | Think of              |
| ---------------------------------- | --------------------- |
| Managed ETL                        | ⭐ AWS Glue            |
| Discover schema in S3              | Glue Crawler          |
| Store metadata/schema              | Glue Data Catalog     |
| CSV → Parquet                      | ⭐ Glue ETL            |
| Columnar analytics format          | Apache Parquet        |
| General batch computing            | AWS Batch             |
| Serverless code                    | Lambda                |
| Big-data Hadoop/Spark platform     | EMR                   |
| Serverless Spark/Hive              | EMR Serverless        |
| EMR access to S3                   | EMRFS                 |
| Detect new S3 object               | S3 Event Notification |
| Least operational overhead for ETL | ⭐ Glue                |


---

### **Exam Cheat Sheet (AWS SAA-C03 Shortcuts)**

| Use Case | AWS Glue Feature |
| --- | --- |
| **Discover schema & create tables** | **Glue Crawler** |
| **Central Metadata Store for Athena / EMR** | **Glue Data Catalog** |
| **Transform CSV to Parquet / Data Cleaning** | **Glue ETL Job** |
| **No-code visual ETL pipeline builder** | **Glue Studio** |
| **Visual data cleaning for analysts** | **Glue DataBrew** |



AWS Glue ke paas **Serverless Data Integration** aur **Data Lake Management** ke liye ek poora suite (features ka set) hai.

Exam aur practical DevOps/Data Engineering ke context mein AWS Glue ke main components yeh hain:

---

### **1. Core AWS Glue Components (The Essentials)**

* **Glue Crawlers:**
* S3, RDS, DynamoDB, ya Redshift jaise data stores ko scan karke automaticamente **schema, data formats, aur partitions** discover karte hain.


* **Glue Data Catalog:**
* Apni saari datasets ki metadata (tables, schemas, partitions) ka ek **centralized repository** (index) hai. Amazon Athena, EMR, aur Redshift Spectrum seedha is Data Catalog ko query karne ke liye use karte hain.


* **Glue ETL Jobs:**
* Python/PySpark scripts run karne ke liye serverless execution engine. Is ke 3 types hote hain:
* **Spark Jobs:** Heavy distributed big data processing ke liye.
* **Python Shell Jobs:** Lightweight Python scripts (boto3, pandas) run karne ke liye.
* **Ray Jobs:** Machine Learning aur Python workloads ko scale karne ke liye.





---

### **2. Visual & Workflow Features**

* **Glue Studio:**
* Aisa **drag-and-drop visual interface** jahan aap bina code likhe ETL pipelines (nodes, joins, transformations) design kar sakte hain.


* **Glue Workflows & Triggers:**
* Multiple Crawlers aur ETL Jobs ko aapas mein chain/orchestrate karne ke liye (e.g., *Crawler Finish $\rightarrow$ Trigger ETL Job $\rightarrow$ Send Notification*).


* **Glue DataBrew:**
* Aisa visual data preparation tool jo non-programmers/analysts ko **clean and normalize data** karne ki ijaazat deta hai without writing code (250+ pre-built transformations).



---

### **3. Data Quality & Streaming Features**

* **Glue Data Quality:**
* Automatic data validation rules define karne ke liye (e.g., *Check if 'Email' column is not null* ya *Check if 'Age' > 0*).


* **Glue Streaming ETL:**
* Real-time streaming data (Kinesis Data Streams ya Apache Kafka se) ko micro-batches mein process karke S3/Data Lake mein load karne ke liye.


* **Glue Schema Registry:**
* Streaming data ke schemas ko control aur manage karne ke liye (Event-driven architectures ke liye).

---
---
---

Aaiye, in dono concepts ko bilkul aasan alfaz mein samajhte hain! Pehle Glue Crawler ko dekhte hain, aur phir QuickSight aur OpenSearch Dashboards ka farq samajte hain.

---

### 1. AWS Glue Crawler & Glue Data Catalog Kya Hai? 📂

Imagine karein ke aap ke paas Amazon S3 mein hazaron CSV files pari hain jin mein sales ka data hai.

* Computer ko raw S3 files dekh kar yeh samajh nahi aati ke konsa column "Name" ka hai aur konsa "Price" ka hai. Use pehle se ek **Table** ki shakal (Schema) chahiye hoti hai jismein rows aur columns define hon.

Yahan aata hai **AWS Glue Crawler**:

1. **Glue Crawler (The Smart Clerk):** Yeh ek automated worker hai jo aap ke S3 bucket ke andar jata hai, files ko khol kar parhta hai, aur khud-ba-khud pata laga leta hai ke columns ke naam kya hain aur data kis type ka hai (jaise text, number, date).
2. **Glue Data Catalog (The Filing Cabinet):** Jab Crawler saari information nikal leta hai, toh woh use ek organized **Data Catalog (Database/Tables)** mein save kar deta hai.

**Faida:** Ab Amazon Athena ya koi bhi query tool direct S3 ki raw files par nahi balkay is Glue Data Catalog ki table par SQL query chala sakta hai — bilkul waise jaise aap kisi SQL database ko query karte hain!

---

### 2. Amazon QuickSight vs. OpenSearch Dashboards (Kibana) 📊

Yeh dono data ko visualize (charts aur graphs ki shakal mein) karne ke tools hain, lekin inka istemal bilkul mukhtalif jagahon par hota hai:

| Feature | Amazon QuickSight | OpenSearch Dashboards (Kibana) |
| --- | --- | --- |
| **Main Purpose** | **Business Intelligence (BI) & Reports** (Jaise sales charts, revenue graphs, executive dashboards). | **Log Analysis & Real-time Monitoring** (Jaise server logs, error tracking, security alerts). |
| **Kiske sath chalta hai?** | Yeh **Amazon Athena**, RDS, aur Redshift ke sath deeply integrated hota hai. | Yeh sirf **Amazon OpenSearch (Elasticsearch)** ke sath chalta hai. |
| **Pricing Model** | Serverless, **Pay-per-session** (jab user dekhta hai tab paise lagte hain). | Dedicated cluster chalana parta hai (24/7 hourly charges). |

**Is sawal mein QuickSight kyun sahi tha?**
Kyunki sales team ko weekly revenue reports aur business analytics chahiye thin jo S3/Athena par bani tables se aani thin, na ke servers ke logs ya search data!

---

7-September-2026

12-September-2026
