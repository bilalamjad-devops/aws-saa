

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

7-September-2026

12-September-2026
