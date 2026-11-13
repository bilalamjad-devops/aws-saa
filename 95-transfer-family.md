**AWS Transfer Family ek standalone (poori alag) AWS service hai.**

Yeh kisi doosri service ka chhota sa feature nahi hai, balkey AWS ki apni ek fully-managed **Serverless File Transfer Service** hai.

---

### Iska Main Kaam Kya Hai?

Aap ke paas koi purana system ya clients hain jo files send karne ke liye traditional protocols use karte hain:

* **SFTP** (SSH File Transfer Protocol)
* **FTPS** (FTP over SSL)
* **FTP** (File Transfer Protocol)
* **AS2** (Applicability Statement 2)

Aap AWS Transfer Family service ko chalate hain, aur yeh service in protocols ke endpoints provide karti hai. Phir yeh aap ki aane wali files ko automatically **Amazon S3** ya **Amazon EFS** mein store kar deti hai.

---

### Real-World Example (Aasan Lafzon Mein)

Maan lein aap ki company ko kisi client se daily basis par files receive hoti hain via **SFTP**:

1. Aap **AWS Transfer Family** service setup karte hain (bina koi EC2 server banaye).
2. Client apne SFTP tool se AWS Transfer Family ke endpoint par file bhejta hai.
3. AWS Transfer Family us file ko pakad kar seedha aap ke **S3 Bucket** ya **EFS Drive** mein drop kar deti hai.

---

### AWS Exam Tip (SAA-C03):

> Jab bhi exam sawal mein **"SFTP"**, **"FTPS"**, ya **"FTP"** ke lafz aayein aur requirement ho ke **"Serverless"** ya **"Fully Managed"** tareeqay se files S3/EFS mein lani hain, toh jawab hamesha **AWS Transfer Family** hi hoga.

---
---
---


26. Question

A company is planning to deploy a Secure File Transfer Protocol (SFTP) service on AWS. The SFTP service must receive traffic only from approved public IP addresses. The company should be able to add users and manage their permissions on the SFTP server. The company seeks a highly available serverless solution that can deliver high IOPS performance.

Which of the following solutions would fulfill the company’s needs?

- Create an Amazon S3 bucket. Set up an SFTP service with a public endpoint in AWS Transfer Family filtered exclusively for trusted IPs. Link the S3 bucket to the service's endpoint, then manage user permissions.
- Set up a server-based SFTP solution using Amazon EC2 instances in a public subnet within a VPC. Secure the setup with security groups that restrict access to approved IP addresses. Attach an encrypted Amazon S3 bucket for storage and configure user access permissions through IAM roles.
- `Launch an encrypted Amazon EFS volume. Set up an AWS Transfer Family for SFTP service utilizing elastic IP addresses with a publicly accessible VPC endpoint. On the endpoint, apply a security group restricting access to trusted IPs. Integrate the EFS volume with the service's endpoint and enable user access.`
- Launch an encrypted Amazon Elastic Block Store (EBS) volume. Set up an SFTP service with a public endpoint in AWS Transfer Family and configure it to allow connections only from verified IP sources. Associate the EBS volume with the SFTP service's endpoint and grant users access.


<img width="1920" height="977" alt="setting-up-SFTP-04-13-2024 (1)" src="https://github.com/user-attachments/assets/ce3f5fe0-289b-4ec9-9d94-80d18449ce40" />


Aayein isay step-by-step bohot simple lafzon mein samajhte hain:

---

### 1. Requirements (Sawal Ki Shartein)

1. **SFTP Service:** Files upload/download karne ke liye SFTP chahiye.
2. **IP Whitelisting:** Sirf specific trusted IPs hi connect kar sakein.
3. **Serverless:** Koi EC2 instance ya server khud manage na karna pare.
4. **Storage:** High performance/IOPS mil sake.

---

### 2. Sahi Option Kyun Sahi Hai?

* **AWS Transfer Family:** Yeh AWS ki fully-managed (serverless) service hai jo SFTP support karti hai. Is se humein koi EC2 server nahi banana parta.
* **VPC Endpoint + Security Group:** trusted IPs ki restriction lagane ke liye Transfer Family ko **VPC Endpoint** ke sath lagaya jata hai, jahan **Security Group** ke zariye hum specific IPs ko allow karte hain (Public endpoint par Security Group nahi lagta).
* **Amazon EFS:** EBS storage ko Transfer Family ke sath direct attach nahi kiya ja sakta. AWS Transfer Family sirf **S3 aur EFS** ko support karta hai. EFS high performance aur file-system structure de deta hai.

---

### 3. Short Summary Table

| Requirement | Solution | Kyun? |
| --- | --- | --- |
| **Serverless SFTP** | **AWS Transfer Family** | Fully managed service hai, no EC2 management. |
| **IP Restrict Karna** | **VPC Endpoint + Security Group** | Trusted IPs ko allow karne ke liye Security Group use hota hai. |
| **Supported Storage** | **Amazon EFS** | EBS support nahi hota, aur EFS high performance deta hai. |

---
---
---


12. Question

A logistics company plans to automate its order management application. The company wants to use SFTP file transfer for uploading business-critical documents. Since the files are confidential, encryption at rest is required, and high availability must be ensured. Additionally, each file must be automatically deleted one month after creation.

Which of the following options should be implemented to meet the company’s requirements with the least operational overhead?

- Create an Amazon Elastic File System (Amazon EFS) and enable encryption. Configure AWS Transfer for SFTP to securely upload files to the EFS file system. Apply an EFS lifecycle policy to delete files after 30 days.
- Provision an Amazon EC2 instance and install the SFTP service. Mount an encrypted Amazon EFS file system on the EC2 instance to store the uploaded files. Add a cron job to delete the files older than a month.
- Create an Amazon S3 bucket with encryption enabled. Configure AWS Transfer for SFTP to securely upload files to the S3 bucket. Configure the retention policy on the SFTP server to delete files after a month.
- `Create an Amazon S3 bucket with encryption enabled. Launch an AWS Transfer for SFTP endpoint to securely upload files to the S3 bucket. Configure an S3 lifecycle rule to delete files after a month.`

### 🧠 Question Kya Keh Raha Hai? (Scenario Breakdown)

1. **Setup:** Ek logistics company ko business-critical documents upload karne ke liye **SFTP file transfer** chahiye.
2. **Requirements:**
* **Encryption at rest:** Files encrypted honi chahiye.
* **High availability (HA):** Service down nahi honi chahiye.
* **Auto-deletion after 1 month:** Har file banne ke 30 din (1 mahine) baad khud-ba-khud delete ho jaye.
* **Key Constraint:** **Least operational overhead** (kam se kam management mehnat).



---

### 🔍 Keyword Scanning & Correct Option Analysis

* **Keywords in Question:** `"SFTP file transfer"`, `"encryption at rest"`, `"high availability"`, `"automatically deleted one month after creation"`, `"least operational overhead"`.
* **AWS Transfer Family (AWS Transfer for SFTP) + Amazon S3 + S3 Lifecycle Rule:**
* **AWS Transfer for SFTP:** Yeh ek fully managed, serverless, aur highly available SFTP service hai—aapko koi EC2 server ya SFTP software install/manage nahi karna padta (**least operational overhead**).
* **Amazon S3 (with Encryption):** S3 native durability (99.999999999%) aur Multi-AZ high availability deta hai, aur default server-side encryption (SSE-S3 ya SSE-KMS) provide karta hai.
* **S3 Lifecycle Rule:** S3 mein aap aasani se ek **Lifecycle Expiration Rule** laga sakte hain jo objects ko creation ke **30 days (1 month)** baad automatically delete kar deta hai.



---

### ❌ Baaqi Options Kyun Galat Hain?

* **EFS + EFS Lifecycle Policy (Option 1):** EFS Lifecycle policy files ko **delete nahi karti**, balki purani files ko Infrequent Access (IA) ya Archive storage class mein **move** karti hai! Deletion ke liye S3 Lifecycle Expiration rule chahiye hota hai (aur EFS S3 ke muqable mehenga bhi hai).
* **EC2 + SFTP + EFS + Cron Job (Option 2):** Single EC2 instance high availability nahi deta, aur OS updates, SFTP server management, aur cron job maintain karne mein bohot zyada **operational overhead** hai.
* **Retention policy on SFTP server (Option 3):** AWS Transfer for SFTP mein khud ka koi file retention/deletion policy feature nahi hota—yeh kaam storage layer (**S3 Lifecycle Rule**) par hota hai.

---

### ✅ Correct Answer:

* **Create an Amazon S3 bucket with encryption enabled. Launch an AWS Transfer for SFTP endpoint to securely upload files to the S3 bucket. Configure an S3 lifecycle rule to delete files after a month.**

---

### 🔑 Direct Memory Trick (Exam Key):

> **Managed SFTP + Least Operational Overhead = AWS Transfer for SFTP**
> **Auto-delete files after X days = Amazon S3 Lifecycle Rule (Expiration)** *(EFS lifecycle sirf tiering karta hai, delete nahi!)*

---

9-November-2026

13-November-2026
