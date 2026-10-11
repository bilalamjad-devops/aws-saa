Is question mein **Amazon Aurora / RDS Backup Retention Limits** aur **AWS Backup Integration** ka concept test ho raha hai.

Aayein pehle test hone wale core limits aur elimination strategy ko samajhte hain.

---

## 1. What Is Being Tested Here? (Core Exam Concepts)

Is question mein AWS 2 core database backup concepts test kar raha hai:

1. **Native RDS / Aurora Automated Backup Limits:**
* RDS aur Aurora ke native automated backups ki **maximum retention period limit 35 days** hoti hai.
* Standard RDS console se 35 days se zyada automatic continuous backup retention set **nahi kiya ja sakta**.


2. **Long-Term Backup Retention (>35 Days):**
* Jab bhi requirement 35 days se zyada ki retention (jaise 90 days, 1 year, ya 7 years compliance) ki ho, toh **AWS Backup** use kiya jata hai.



---

## 2. Core AWS Technical Rules

* **RDS Automated Backup Retention Max:** **35 Days** (35 days se bara number choose karna RDS native setting mein disallowed hai).
* **AWS Backup Service:** AWS Backup centralized backup manager hai jo RDS, Aurora, EBS, DynamoDB, aur S3 ke snapshots aur backups ko months ya years tak custom schedule (e.g., 90 days retention) ke under retain kar sakta hai.

---

## 3. Correct Option Explanation

#### ✅ **Create an AWS Backup plan to take daily snapshots with a retention period of 90 days.**

* **Why it works:**
1. **Compliance Ready:** AWS Backup 35-day native RDS limit ko bypass karte hue custom backup lifecycle plans support karta hai (e.g., daily snapshots retained for 90 days).
2. **Least Operational Overhead:** Fully managed service hai, jahan bas rule define karke Aurora cluster ko assign karna hota hai.



---

## 4. Incorrect Options Breakdown (Elimination Strategy)

| Option | Why It Fails the Exam Requirement |
| --- | --- |
| **Configure automated backup... retention period to 90 days** | **Technical Limit Error:** RDS / Aurora native automated backup retention Maximum **35 Days** tak set ho sakti hai. 90 days set karna possible hi nahi hai. |
| **Export automated snapshot to S3... delete object after 90 days** | Snapshot export to S3 manual / async operation hai aur native export lifecycle rules directly backup retention behavior ko handle karne ke muqable extra overhead laate hain. |
| **EventBridge + Lambda to directly download snapshot to S3...** | High operational overhead and unnecessary custom code. AWS Backup jab natively supported hai toh custom scripts banana anti-pattern hai. |

---

## 5. Exam Decision Matrix (RDS Backup Cheat Sheet)

* **RDS / Aurora Native Automated Retention:** $\rightarrow$ **1 to 35 Days**
* **Backup Retention Needed > 35 Days (e.g., 90 days, 1 year):** $\rightarrow$ **AWS Backup**
* **Cross-Account / Cross-Region Centralized Backup Management:** $\rightarrow$ **AWS Backup**

---
---
---


Aayein, is question ko bilkul simple aur step-by-step tod kar samjhte hain!

---

### Question Mein Ho Kya Raha Hai? (The Scenario) 📝

Aap ke paas ek application hai jo **Amazon EKS (Kubernetes)** par chal rahi hai aur iska data **Amazon DynamoDB** database mein save hota hai.

Aap se **2 cheezein** maangi gayi hain:

1. **Private Network Traffic:** DynamoDB ka traffic **Public Internet par na jaye**. EKS aur DynamoDB ke beech jitni bhi database calls ho, wo AWS ke private network ke andar hi rahein.
2. **Cross-Account Backup:** DynamoDB ka backup automatically kisi **dusre AWS Account mein copy/save** ho jaye taake future disaster recovery ya long-term storage ke liye safe rahe.

---

### In Dono Problems Ka Standard Solution Kya Hai? 🛠️

#### Problem 1: Internet Par Traffic Jane Se Kaise Rokna Hai?

* **Solution:** **VPC Gateway Endpoint for DynamoDB**
* **Kyun?** DynamoDB aur Amazon S3 ke liye AWS **Gateway Endpoints** provide karta hai. Jab aap Gateway Endpoint banate hain aur apni Subnet ki **Route Table** mein add karte hain, toh VPC se DynamoDB tak ka sara traffic **Public Internet bypass** karke private AWS network ke andar rehta hai.

#### Problem 2: Backup Dusre AWS Account Mein Kaise Bhejna Hai?

* **Solution:** **AWS Backup**
* **Kyun?** AWS Backup service mein ek feature hota hai jise **Cross-Account Backup** kehte hain. Yeh feature DynamoDB ke backups ko automatically kisi dusre AWS account ke backup vault mein copy kar deta hai.

---

### Baki Options Ghalt Kyun Hain? ❌

* **Interface Endpoint Wali Options:** DynamoDB primary routing ke liye Gateway Endpoints use karta hai. Interface endpoints ko Route Table se attach nahi kiya jata.
* **Amazon Timestream Wali Option:** Timestream ek alag tarah ka database hai, yeh DynamoDB ke backups save karne ke liye use nahi hota.
* **NACL Rules Wali Option:** NACL (Network Access Control List) IP addresses aur CIDR blocks par filtering karta hai, domain names (`dynamodb.us-east-1.amazonaws.com`) par nahi.

---

12-September-2026

11-October-2026
