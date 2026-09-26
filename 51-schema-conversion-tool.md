Aap ne bilkul sahi pakda! AWS SAA-C03 exam mein jab bhi **Heterogeneous Database Migration** (yani alag-alag database engines: e.g., Oracle to PostgreSQL ya SQL Server to MySQL) ka zikr aaye, toh dimag mein fauran **2 tools** aane chahiye:

1. **AWS Schema Conversion Tool (AWS SCT):** Source schema, views, stored procedures, aur code ko target database format mein convert karne ke liye.
2. **AWS Database Migration Service (AWS DMS):** Actual data ko migrate aur continuously sync (CDC) karne ke liye.

---

### Key Scenario Breakdown

* **Source Database:** On-premises Oracle Database.
* **Target Database:** PostgreSQL on AWS (e.g., Amazon RDS for PostgreSQL / Aurora PostgreSQL).
* **Migration Type:** **Heterogeneous** (different engines).
* **Requirements:**
1. Pehle **schema aur code transformation** karna hai.
2. Phir **proper data migration** chalani hai.



---

### Correct Option Explanation

#### ✅ **AWS SCT + AWS DMS**

* **Step 1 (Schema & Code):** **AWS Schema Conversion Tool (SCT)** Oracle ke schema (tables, indexes, stored procedures, triggers) ko read karta hai aur usay target **PostgreSQL** compatible format mein transform/convert kar deta hai.
* **Step 2 (Data Migration):** **AWS Database Migration Service (DMS)** transformed schema par actual table data move karta hai. DMS homogenous aur heterogeneous dono migrations ko support karta hai.

---

### Incorrect Options Breakdown (Elimination)

* ❌ **Launch Template with auto-conversion:** Launch templates EC2 instances launch karne ke configurations ke liye hote hain, in mein automated database schema conversion capabilities nahi hoti.
* ❌ **Amazon Neptune + AWS Batch:** Amazon Neptune ek **Graph Database** service hai. Yeh relational database schemas convert karne ke liye use nahi hota.
* ❌ **Heterogeneous migrations not supported:** Yeh claim bilkul ghalat hai. AWS SCT + DMS heterogeneous database migrations ko fully support karte hain.

---

### Exam Rule for SAA-C03

> **Database Migration Keywords:**
> * **Same Engine (Homogeneous):** Oracle $\rightarrow$ Oracle / Postgres $\rightarrow$ Postgres $\rightarrow$ **AWS DMS alone** (or native database tools like `pg_dump`, Oracle Data Pump)
> * **Different Engine (Heterogeneous):** Oracle $\rightarrow$ Postgres / SQL Server $\rightarrow$ MySQL $\rightarrow$ **AWS SCT + AWS DMS**


26-September-2026

