
<img width="594" height="526" alt="aws_licence_manager" src="https://github.com/user-attachments/assets/161e5625-7462-4db5-95f2-76b3e0b6a1f7" />



### 🎯 What is being tested?

**Managing software licenses for EC2.**

### ✅ Correct answer

**Define licensing rules in AWS License Manager → enable “Enforce license limit” → use Amazon SNS for notifications.**

### 🔑 Key concept

**AWS License Manager** is specifically designed to track and control software license usage.

For this scenario:

* License tied to **CPU count** → License Manager can track it.
* **Enforce license limit** → prevents launching instances beyond the available licenses.
* **SNS** → sends notifications when the licenses are fully utilized.

Flow:

**EC2 launch → License Manager checks CPU/license → Allow or block → SNS notification**

### ❌ Others

* **Systems Manager Fleet Manager** → manage/monitor instances, not software licensing.
* **AWS RAM** → share resources across accounts, not license management.
* **ACM** → manages SSL/TLS certificates, not software licenses.

### 🔥 Exam shortcut

**Software licenses + track usage + enforce limit → AWS License Manager.**


18-September-2026

## 5. Exam Decision Matrix (AWS Governance Tools Cheat Sheet)

* **Manage & Enforce Software Licenses (vCPU/Sockets):** $\rightarrow$ **AWS License Manager**
* **Share Resources across AWS Accounts:** $\rightarrow$ **AWS Resource Access Manager (AWS RAM)**
* **Provision & Audit Software Packages / Patching:** $\rightarrow$ **AWS Systems Manager (SSM)**
* **SSL/TLS Certificate Provisioning:** $\rightarrow$ **AWS Certificate Manager (ACM)**
