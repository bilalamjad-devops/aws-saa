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



30-September-2026
