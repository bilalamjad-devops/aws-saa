**Haan, bilkul 100% sahi!**

Is question ke **TWO correct answers** yahi dono hain:

1. ✅ **Write an AWS Lambda function that refreshes the AWS Trusted Advisor Service Limits checks and set it to run every 24 hours.**
2. ✅ **Capture the events using Amazon EventBridge (Amazon CloudWatch Events) and use an Amazon Simple Notification Service (Amazon SNS) topic as the target for notifications.**

---

### In Dono Ka Mil Kar Architecture Kaise Kaam Karta Hai?

* **Lambda Function:** Har 24 ghante baad Trusted Advisor ki Service Limits checks ko **refresh** karta hai taake latest quota data fetch ho sakay.
* **EventBridge:** Jab Trusted Advisor dekhta hai ke koi resource service limit ke kareeb (e.g., 80% ya 90%) pahunch chuki hai, toh EventBridge us event ko detect kar leta hai.
* **SNS Topic:** EventBridge us event ko SNS topic par bhejta hai jo team ko alert/notification send kar deta hai.

Dono mil kar ek complete **Automated Quota Monitoring Solution** banate hain!

---

---
---
---


**AWS Trusted Advisor** ek automated tool hai jo aap ke poore AWS account ko continuously scan karta hai aur aap ko **AWS Best Practices** ke mutabiq recommendations aur warnings deta hai.

Aap isay apna **"Personal AWS Consultant"** samajh sakte hain jo aap ke account par nazar rakhta hai.

---

### Trusted Advisor Ke 5 Main Pillars (Checks)

Yeh 5 alag-alag categories mein aap ke account ko analyze karta hai:

1. **Cost Optimization (Paisa Bachana):**
* Batata hai ke konse EC2 instances, EBS volumes, ya RDS databases bina kisi use ke chal rahe hain (idle/unused) taake aap unhe band karke bill kam kar sakayn.


2. **Performance (Raftar & Efficiency):**
* Track karta hai ke kahin aap ke resources over-utilized toh nahi ho rahe ya DB instances par high load toh nahi hai.


3. **Security (Hifazat):**
* Detect karta hai ke kahin aap ne koi S3 bucket publicly open toh nahi kar di, S3 bucket default encryption disable hai, ya root account par MFA (Multi-Factor Authentication) missing hai.


4. **Fault Tolerance (High Availability):**
* Check karta hai ke aap ke EBS snapshots recent hain ya nahi, Multi-AZ databases enabled hain ya nahi, aur backups proper ban rahe hain ya nahi.


5. **Service Limits / Quotas (Jo Humare Question Mein Tha):**
* Check karta hai ke aap apne AWS account ki **Max Limits** (jaise maximum 20 EC2 instances per region, ya max VPC limits) ke kitne karib pohnch chuke hain (e.g., 80% limit cross hone par warning deta hai).



---

### SAA-C03 Exam Rule for Trusted Advisor

* **Basic/Developer Support Plan:** Is mein sirf **7 Core Security & Cost Checks** milte hain.
* **Business or Enterprise Support Plan:** Is mein **Full 100+ Checks** milte hain (jis mein Service Limits Check aur API Access `DescribeTrustedAdvisorChecks` bhi shamil hai).

---


---
---
---

Is question ke correct answers **Capture the events using Amazon EventBridge (Amazon CloudWatch Events) and use an Amazon Simple Notification Service (Amazon SNS) topic as the target for notifications** aur **Query the AWS Trusted Advisor Service Limits check every 24 hours by calling the DescribeTrustedAdvisorChecks API operation. Ensure that your AWS account has a Business Support+ plan** hain.

---

### Key Scenario Breakdown

* **Goal:** Multiple research departments ki AWS resource usage track karni hai taake **AWS Service Quotas / Limits** unexpectedly hit na hon.
* **Requirement:** Automated mechanism banana hai jo limits check kare aur thresholds breach hone par notification bhej sake.
* **Selection:** TWO options choose karne hain.

---

### Correct Options Explanation

#### ✅ **1. Query the AWS Trusted Advisor Service Limits check every 24 hours by calling DescribeTrustedAdvisorChecks... (Requires Business/Enterprise Support)**

* **Why it works:** **AWS Trusted Advisor** dedicated service limits / quotas tracking capabilities provide karta hai. Iski service limits check API ko programmatic query karne ke liye **Business ya Enterprise Support plan** lazmi hota hai. By querying it daily, aap active usage ko monitor kar sakte hain.

#### ✅ **2. Capture the events using Amazon EventBridge (CloudWatch Events) and use an Amazon SNS topic as the target for notifications**

* **Why it works:** Jab Trusted Advisor ya Service Quotas limit warning event trigger karta hai (jaise usage 80% ya 90% tak pahunch sakti hai), **Amazon EventBridge** us event ko intercept karta hai aur automated alerts bhejney ke liye **Amazon SNS topic** par route kar deta hai.

---

### Incorrect Options Breakdown (Elimination)

* ❌ **Create an SNS topic and configure it as a target for notifications (Standalone):** Yeh option अधूरा (incomplete) hai kyunki yeh nahi batata ke SNS topic ko trigger kahan se kiya jayega (EventBridge middleman ke bagair events capture nahi hote).
* ❌ **Write a Lambda function that refreshes Trusted Advisor checks:** Trusted Advisor Service Limits checks ko AWS khud background mein periodically refresh karta hai; refresh API call har check ke liye available nahi hoti aur Lambda ki direct zaroorat nahi hai.
* ❌ **Utilize AWS managed rule on AWS Config...:** AWS Config resource compliance aur configuration drift check karta hai, service quota monitoring ke liye AWS Config rule use nahi kiya jata.

---

### Exam Rule for SAA-C03

> **Service Quota Alerting Architecture:**
> **Trusted Advisor (Service Limits Check)** $\rightarrow$ **EventBridge Rule** $\rightarrow$ **Amazon SNS Topic**
> *(Note: Trusted Advisor API access requires Business or Enterprise Support plan).*

---

27-September-2026
