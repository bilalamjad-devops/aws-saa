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

9-November-2026
