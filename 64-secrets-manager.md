Dono hi AWS ki **Secrets & Configuration Storage Services** hain jo passwords, API keys, aur configuration data ko secure tareeqe se store karne ke liye use hoti hain.

Inka difference simple Urdu/Hindi mein samajhte hain:

---

### 1. AWS Systems Manager Parameter Store (SSM Parameter Store)

* **Main Purpose:** System configuration settings aur basic secrets (passwords/API keys) ko store karna.
* **Cost:** **Free Tier / Standard Parameters FREE hotay hain** (0$ cost per parameter).
* **Key Features:**
* Simple Key-Value pairs store karta hai (e.g., `/app/db_url` = `mydb.domain.com`).
* Sensitive data ke liye **SecureString** type use hoti hai jo **AWS KMS** se encrypt hoti hai.


* **Limitation:** Automatic password rotation ka built-in feature nahi hota (manual/Lambda ke zariye karna padta hai).

---

### 2. AWS Secrets Manager

* **Main Purpose:** High-security database credentials, API keys, aur OAuth tokens ko manage aur **automatically rotate** karna.
* **Cost:** Paid service hai ($0.40 per secret per month + API requests cost).
* **Key Features:**
* **Built-in Automatic Key Rotation:** Yeh Amazon RDS, Redshift, DocumentDB ke passwords ko bina kisi downtime ke **automatically rotate** (badal) sakta hai.
* Integration: Cross-account access aur random password generation natively supports karta hai.



---

### Easy Comparison Table 💡

| Feature | SSM Parameter Store | AWS Secrets Manager |
| --- | --- | --- |
| **Cost** | Standard Parameters **FREE** | **Paid** ($0.40/secret/month) |
| **Primary Use Case** | App Configs & Static Passwords | Database Credentials & API Keys |
| **Auto-Rotation** | Custom Lambda script likhni padti hai | **Built-in / Automatic** (1-click for RDS) |
| **Encryption** | KMS (SecureString) | KMS (Default) |

---

### Quick Exam Shortcut 🎯

* **Cost-effective / Simple Configs / General Passwords** = **SSM Parameter Store**
* **Database Credentials + Automatic Rotation Needed** = **AWS Secrets Manager**

---
---
---

### Keywords Scan 🔍

1. **"database credentials, API keys, and other secrets"**
* **Trigger:** AWS mein secrets, API keys, aur database credentials store karna.


2. **"encrypted and rotated on a regular basis ... latest version"**
* **Trigger:** Built-in/automated credential rotation.



---

### Correct Answer

**Use AWS Secrets Manager to store and encrypt the database credentials, API keys, and other secrets. Enable automatic rotation for all of the credentials.**

---

### Roman Urdu Explanation 💡

* **AWS Secrets Manager:**
* Secrets Manager specifically sensitive credentials (database passwords, API keys) ko securely store aur encrypt karne ke liye design kiya gaya hai.
* Iska sab se bada feature **Automatic Rotation** hai (jo built-in AWS Lambda integration ke zariye RDS passwords wagerah ko bina application downtime ke automatically rotate/update karta rehta hai).
* Application hamesha AWS SDK ke zariye latest version retrieve kar sakti hai.



---

### Baqi Options Ghalt Kyun Hain? ❌

* **Systems Manager Parameter Store (SecureString):** Parameter Store secrets store kar sakta hai, lekin isme **automatic credential rotation default mein nahi hoti** (is ke liye custom rotation custom logic se banani padti hai).
* **AWS KMS:** KMS encryption keys (CMKs) manage karne ke liye hota hai, direct secrets/passwords ko database credentials ki tarah manage aur rotate karne ke liye nahi.
* **AWS ACM (Certificate Manager):** ACM SSL/TLS certificates (HTTPS) issuing aur management ke liye use hota hai, database passwords store karne ke liye nahi.

---


30-September-2026

12-October-2026
