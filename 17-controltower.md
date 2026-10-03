
# 🧠 The 4 services you should separate in your head

| Service                       | Simple meaning                                   |
| ----------------------------- | ------------------------------------------------ |
| **Control Tower**             | 🏢 Set up + govern multi-account AWS environment |
| **AWS RAM**                   | 🤝 Share resources between accounts              |
| **AWS Config**                | 🔍 Check resource configuration/compliance       |
| **Systems Manager OpsCenter** | 🛠️ Manage operational issues                    |

And:

> **Guardrails = governance controls/rules**

<img width="1179" height="865" alt="aws-control-tower-landing-zone" src="https://github.com/user-attachments/assets/735256df-7c94-458e-8ae8-2b0cfd70106d" />



### Memorize these four:

**AWS Organizations**
→ Manage **multiple AWS accounts**

**IAM Identity Center**
→ Centralized **AWS account login/access**

**AD Connector**
→ Connect AWS to existing **Microsoft Active Directory**

**Cognito**
→ User authentication for **your applications/web/mobile apps**

---

## One-line exam trick 🧠

When you see:

> **"Multiple AWS accounts + existing corporate directory + centralized login"**

Think:

**AWS Organizations + IAM Identity Center + Active Directory Connector**

And when you see:

> **"Users need to log into our web/mobile application"**

Think:

**Amazon Cognito**.


### ✅ Option 1

> On the master account, use AWS Organizations to create a new organization with all features turned on. Invite the child accounts to this new organization.

Correct.

Why?

Because the company wants to consolidate multiple AWS accounts.

**AWS Organizations = account management.**

```text
Organization
   ├── Account A
   ├── Account B
   ├── Account C
   └── Account D
```

---

### ✅ Option 2

> Configure AWS IAM Identity Center for the organization and integrate it with the company's directory service using the Active Directory Connector.











<img width="2123" height="1505" alt="aws-organizations-scp-demo" src="https://github.com/user-attachments/assets/a4f7e3ec-7730-4a0b-a3a3-42b1ebf2b2cc" />

### 🎯 What is being tested?

**AWS Organizations + Service Control Policies (SCPs)** → centrally restrict what users/accounts can do.

### ✅ Correct answer

**Add the developers' AWS accounts to an Organizational Unit (OU). Attach a Service Control Policy (SCP) to the OU that restricts access to AWS Config.**

### 🔑 Key concept

**SCP = central permission guardrail**

The company can put all developer accounts into an **OU** and attach an SCP that prevents them from:

* Modifying AWS Config rules
* Deleting AWS Config rules
* Disabling AWS Config

The developers can still have IAM permissions, but the **SCP sets the maximum permissions allowed**.

**Organization → OU → Developer accounts → SCP**

### ❌ Why others are wrong

* **Config rule in root account** ❌ → can detect changes but doesn't prevent them.
* **IAM role/trust relationship** ❌ → trust policies control *who can assume a role*, not Config permissions.
* **Control Tower + IAM trust relationship** ❌ → unnecessary complexity; SCP directly solves the requirement.

### 🔥 Exam shortcut

> **Centrally prevent actions across AWS accounts → SCP**

**SCP = Prevent**
**AWS Config = Detect/assess compliance**

So when the question says **“developers must be unable to modify/delete a service”**, think **SCP**.

---
---
---

Is question ka simple matlab yeh hai:

Ek company ne apne AWS accounts ko **AWS Organizations** ke under **Organizational Units (OUs)** mein group karke rakha hua hai taaki alag-alag teams/departments ke workloads ko isolate rakha ja sake.

Ab woh chahte hain ki:

1. Jab bhi is **OU hierarchy/structure mein koi badlaav (change ya drift)** ho, toh system use **monitor (track)** kare.
2. Relevant stakeholders ko **automatic alerts/notifications** mil jayein.
3. Is pure setup ko karne mein **kam se kam administrative mehnat (LEAST administrative overhead)** lagni chahiye.

---

### Iska Solution **AWS Control Tower** kyun hai?

AWS Control Tower inherently AWS Organizations ko govern karta hai. Isme **Account Drift Detection** ka built-in feature hota hai—jaise hi koi OU structure ya governance rules ko chedta hai, Control Tower bina kisi custom script ya extra monitoring rule ke automated alert generate kar deta hai.


31-August-2026

1-September-2026

12-September-2026

03-October-2026
