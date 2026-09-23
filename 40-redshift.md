### 5. Cheat Sheet for AWS Disaster Recovery (SAA-C03)

* **Cross-Region DR for Redshift:** $\rightarrow$ **Enable Cross-Region Snapshot Copy**
* **Cross-Region DR for RDS / Aurora:** $\rightarrow$ **Cross-Region Read Replicas** or **Aurora Global Database**
* **Cross-Region DR for S3:** $\rightarrow$ **S3 Cross-Region Replication (CRR)**

---
Aayein is question ko bilkul aasan aur simple real-life example se samajhte hain:

---

### Question Ki Kahani (Real-World Context)

Ek company hai jo real-time data process kar ke **Amazon S3 bucket mein JSON files** ki shakal mein save kar rahi hai.

1. **Problem / Scenario:**
S3 mein bohot saara data (JSON files) jama ho chuka hai. Company is data par **Big Data Analytics / Deep Analysis** karna chahti hai.
2. **Sab Se Badi Shart (Constraint):**
Question mein saaf bola gaya hai: **"Without moving them into a separate analytics system"**.
Matlab, data jahan pada hai (S3 bucket mein), usko **wahan se kisi doosre database ya data warehouse mein copy/move kiye bina** directly S3 par hi SQL queries chalanay ka tareeqah chahiye.

---

### Iska Sahi Hal Kya Hai? (In-Place S3 Querying)

AWS mein 3 aisi specific services hain jo S3 par pare data ko bina move kiye analyze karne ke liye design ki gayi hain:

#### 1. Amazon Athena

* Yeh ek **Serverless SQL tool** hai. Aap bas S3 bucket par Athena ko point karte hain aur direct SQL query likh kar results haasil kar lete hain (data ko kahin copy nahi karna padta).

#### 2. Amazon Redshift Spectrum

* Standard Redshift mein pehle data ko Redshift ke andar import/load karna padta hai.
* Lekin **Redshift Spectrum** ka kamaal yeh hai ke yeh Redshift ko **directly S3 bucket mein pari files par SQL query** chalane deta hai (bina data import kiye).

#### 3. AWS Glue (Data Catalog)

* JSON files mein data aage-peeche ho sakta hai. AWS Glue automatically S3 files ko scan kar ke unka **Schema (Tables, Columns)** samajhta hai taake Athena aur Redshift Spectrum unhe aasan table format mein query kar sakein.

---

### Exam Rule (Yaad Rakhne Ke Liye)

* Jab bhi question mein aye: **"Analyze data directly in S3 WITHOUT moving / loading it into a database"** $\rightarrow$ Hamesha **Amazon Athena**, **Amazon Redshift Spectrum**, aur **AWS Glue** select karein!

---

23-September-2026
