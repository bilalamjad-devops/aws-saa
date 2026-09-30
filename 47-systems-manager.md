Is question ka correct answer **Run Command** hai.

Aayein point-to-point comparison aur concept ko samajhte hain:

---

### Key Scenario Breakdown

* **Requirement:** On-demand EC2 instances (jo Auto Scaling mein hain) ko secure configuration/commands bhejni hain.
* **Constraint:** Instances ke andar **SSH (Linux) ya RDP (Windows)** connection establish **NAHI** karna (inbound ports 22/3389 open kiye bina kaam karna hai).

---

### Correct Option Explanation

#### ✅ **Run Command**

* **Why it works:** **AWS Systems Manager (SSM) Run Command** aap ko EC2 instances par remotely aur securely administrative tasks/scripts execute karne deta hai.
* Is ke liye instances par **SSM Agent** running hona chahiye. Request outbound HTTPS (Port 443) ke zariye AWS Systems Manager API se milti hai, is liye aap ko **SSH/RDP ports open karne ya SSH keys manage karne ki koi zaroorat nahi hoti**.

---

### Incorrect Options Breakdown (Elimination)

* ❌ **AWS App Runner:** Fully managed service hai jo containerized web applications ko deploy karti hai, EC2 instances ko manage karne ke liye nahi hai.
* ❌ **EC2Config:** Legacy service/agent hai jo older Windows Server instances par use hota tha (ab isay SSM Agent ne replace kar diya hai).
* ❌ **AWS CodePipeline:** CI/CD orchestration service hai jo code deploy/build automation ke liye use hoti hai, instance administration ke liye nahi.

---
---
---


<img width="1441" height="1017" alt="aws-systems-manager-parameter-store-securestring" src="https://github.com/user-attachments/assets/5884826f-a880-4c43-a479-44ad6b1e991a" />


Is question ka step-by-step breakdown Roman Urdu mein yeh hai:

---

### Question Ka Summary:

Media company ka website **Amazon ECS on AWS Fargate** par chal raha hai aur database **Amazon Keyspaces** hai.
Security policy ke mutabiq database credentials ko **environment variables** ke zariye pass karna hai, lekin shart yeh hai ke credentials ECS task definition file ya container mein **plaintext mein nazar na aayein** aur minimal effort ke sath secure ho jayein.

---

### Options Ka Breakdown:

1. **Option 1 (ECS Anywhere + IAM Access Analyzer):**
* **Galat:** ECS Anywhere on-premises infrastructure ko ECS se connect karne ke liye hota hai. Yeh container level secrets management ke liye nahi hai.


2. **Option 2 (Aurora PostgreSQL + KMS + CLI JSON):**
* **Galat:** Aurora PostgreSQL mein JSON store karke CLI commands se fetch karna zaroorat se zyada complex aur impractical hai (is me minimal effort bilkul nahi hai).


3. **Option 3 (Secrets Manager + ACM Encryption):**
* **Galat:** ACM (AWS Certificate Manager) SSL/TLS certificates manage karta hai, Secrets Manager ke secrets ko encrypt karne ke liye **AWS KMS** use hota hai, ACM nahi.


4. **Option 4 (SSM Parameter Store + KMS Encryption + ECS task execution role):**
* **Sahi (Correct):**
* **AWS Systems Manager Parameter Store** (SecureString) mein credentials ko **AWS KMS** se encrypt karke store kiya jata hai.
* **ECS Task Execution Role** ko KMS aur Parameter Store ka access diya jata hai.
* ECS Task Definition mein `secrets` block ke andar Parameter Store ka ARN aur Environment Variable ka naam de diya jata hai.
* Fargate container launch hotay waqt background mein Parameter Store se secret fetch karke environment variable mein **decrypt karke pass kar deta hai**, bina task definition mein plaintext password dikhaye!





---

### Sahi Jawab:

**Option 4:** **Use the AWS Systems Manager Parameter Store to keep the database credentials and then encrypt them using AWS KMS. Create an IAM Role for your Amazon ECS task execution role (taskRoleArn) and reference it with your task definition, which allows access to both KMS and the Parameter Store. Within your container definition, specify secrets with the name of the environment variable to set in the container and the full ARN of the Systems Manager Parameter Store parameter containing the sensitive data to present to the container.**

> **Exam Tip:** ECS / Fargate container ko environment variables ke zariye secure credentials pass karne ke do hi standard tarike hote hain: **AWS Secrets Manager** ya **SSM Parameter Store**. ECS Task Definition ke `secrets` array mein Parameter Store/Secrets Manager ka ARN de diya jata hai.

30-September-2026

25-September-2026
