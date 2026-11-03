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


---
---
---

29. Question

A media company hosts a news website on an Amazon ECS Cluster that uses the Fargate launch type. All application data is stored in Amazon Keyspaces (for Apache Cassandra) with data-at-rest encryption enabled. To comply with strict security standards, database credentials must be provided via environment variables. As the Solutions Architect, your goal is to secure these credentials so they cannot be viewed in plaintext on the cluster.

Which of the following solutions would be the most appropriate to implement with minimal effort?


- Use the AWS Secrets Manager to store the database credentials and then encrypt them using AWS Certificate Manager (ACM). Create a resource-based policy for your Amazon ECS task execution role (taskRoleArn) and reference it with your task definition which allows access to both ACM and AWS Secrets Manager. Within your container definition, specify secrets with the name of the environment variable to set in the container and the full ARN of the Secrets Manager secret which contains the sensitive data, to present to the container.
- In the ECS task definition file of the ECS Cluster, store the database credentials to Amazon ECS Anywhere to centrally manage these sensitive data and securely transmit it to only those containers that need access to it. Allocate an IAM Role to the cluster to ensure that the passwords are only accessible by the ECS service tasks. Run the AWS IAM Access Analyzer to verify that the credentials can’t be viewed in plaintext.
- Store the database credentials in the ECS task definition file of the ECS Cluster and encrypt it with KMS. Store the task definition JSON file in Amazon Aurora PostgreSQL. Create an IAM role for the ECS task definition script that allows access to the Aurora PostgreSQL database, then pass the --cli-input-json parameter when calling the ECS register-task-definition action. Reference the task definition JSON file in Aurora PostgreSQL, which contains the database credentials.
- `Use the AWS Systems Manager Parameter Store to keep the database credentials and then encrypt them using AWS KMS. Create an IAM Role for your Amazon ECS task execution role (taskRoleArn) and reference it with your task definition, which allows access to both KMS and the Parameter Store. Within your container definition, specify secrets with the name of the environment variable to set in the container and the full ARN of the Systems Manager Parameter Store parameter containing the sensitive data to present to the container.`

<img width="1441" height="1017" alt="aws-systems-manager-parameter-store-securestring (1)" src="https://github.com/user-attachments/assets/81ee689e-8288-448c-ab9e-96fdc68645dd" />

Aaiye is sawal ko apne crisp, fast-track aur keyword-focused breakdown ke sath samajhte hain! 🚀

---

### 🎯 1. Sawal Kya Keh Raha Hai? (Question Breakdown)

Ek media company Amazon ECS (Fargate launch type) par news website host kar rahi hai. Sensitive database credentials (Amazon Keyspaces / Cassandra ke passwords) container ke **environment variables** ke zariye pass hone hain.

* **Constraint & Goal:** Credentials plaintext mein view na hon, KMS encryption ke sath securely store hon, aur minimal effort ke sath ECS Fargate task container ko secret injection ke taur par mill jayein.

---

### ✅ 2. Sahi Jawab Kya Keh Raha Hai? (Correct Answer)

> **Use the AWS Systems Manager Parameter Store to keep the database credentials and then encrypt them using AWS KMS. Create an IAM Role for your Amazon ECS task execution role (taskRoleArn) and reference it with your task definition, which allows access to both KMS and the Parameter Store. Within your container definition, specify secrets with the name of the environment variable to set in the container and the full ARN of the Systems Manager Parameter Store parameter containing the sensitive data to present to the container.**

#### **Deep-Dive Explanation:**

1. **SSM Parameter Store (SecureString) + KMS:** Secrets/passwords ko **SSM Parameter Store** mein `SecureString` type ke taur par KMS encryption ke sath store karte hain.
2. **ECS Task Execution Role:** Task execution role ke paas SSM Parameter Store aur KMS decrypt privileges hoti hain.
3. **Container Definition Integration:** ECS container definition ke `secrets` section mein environment variable ka naam aur Parameter Store ARN link kar diya jata hai. ECS Fargate automatically initialization ke waqt secret retrieve/decrypt karke container ke environment variable mein in-memory inject kar deta hai bina plaintext display kiye.

---

### ❌ 3. Baqi Options Kyun Ghalat Hain?

* **ACM Encryption + Resource-based policy on Task Role:**
* *Ghalat kyun?* ACM SSL/TLS certificates manage karta hai, Secrets Manager ke parameters encrypt karne ke liye nahi. Secrets Manager KMS keys use karta hai.


* **ECS Anywhere + IAM Access Analyzer:**
* *Ghalat kyun?* ECS Anywhere on-premises hybrid workloads ke liye hota hai, secrets management ke liye nahi.


* **Store credentials in task definition file + Aurora PostgreSQL:**
* *Ghalat kyun?* Task definition JSON file mein passwords likhna unhein plaintext expose kar deta hai. Aurora DB mein JSON file rakhna bohot zyada complicated aur irrelevant setup hai.



---

### 🔍 4. Keyword Scanning & Exam Shortcut

| Question Key Phrases | Direct AWS Mapping | Reason / Logic |
| --- | --- | --- |
| **"ECS Fargate" + "Environment variables credentials" + "Not visible in plaintext"** | **SSM Parameter Store / Secrets Manager + ECS Container Secrets Definition** | ECS natively decrypts and injects secrets into container environment variables using the Task Execution Role. |

---

### 🧠 One-Line Memory

> **ECS Environment Variables Secrets ➔ SSM Parameter Store (SecureString) / Secrets Manager + Task Execution Role**

---

29-October-2026

30-September-2026

25-September-2026

3-November-2026
