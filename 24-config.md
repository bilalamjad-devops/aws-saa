Yes — this one tests the **difference between CloudTrail and AWS Config**.

## 🎯 What is it asking?

The key requirements are:

* Monitor **resource configurations**
* Track configuration changes
* Check **compliance**
* Detect **public S3 buckets**
* Create rules

👉 **AWS Config** is designed for this.

### Options

| Option                | What it does                                                      | Correct? |
| --------------------- | ----------------------------------------------------------------- | -------- |
| IAM Credential Report | Shows IAM users and their credential status                       | ❌        |
| Trusted Advisor       | Gives AWS best-practice recommendations                           | ❌        |
| CloudTrail            | Records **who did what API action and when**                      | ❌        |
| **AWS Config**        | Records resource configurations + evaluates compliance with rules | ✅        |

### 🧠 CloudTrail vs Config — VERY important

```text
CloudTrail → "WHO changed WHAT and WHEN?"
Config     → "WHAT is the resource configured like, and is it COMPLIANT?"
```

Example:

**CloudTrail:**

> User Bilal changed an S3 bucket policy at 10:30 AM.

**AWS Config:**

> This S3 bucket is publicly accessible → **NON-COMPLIANT**.

### 🔥 SAA shortcut

> **Configuration + compliance + rules + public resources → AWS Config** ✅

> **API activity + who/when/what → CloudTrail**


### 🎯 What is being tested?

**Monitoring S3 access and detecting suspicious/unauthorized access.**

### ✅ Correct answer

**Use Amazon GuardDuty to monitor malicious activity on S3.**

🔥 **Exam shortcut:**
**GuardDuty = threat detection / suspicious or malicious activity.**

* **CloudTrail** → records **who did what, when** (API activity/audit logs).
* **GuardDuty** → analyzes activity and identifies **potential threats/suspicious behavior**.
* **Inspector** → vulnerability management for workloads, not S3 access monitoring.
* **Rekognition** → image/video analysis.

👉 Because the requirement specifically says **“risk of unauthorized access or suspicious access patterns”**, choose **GuardDuty**.


8-September-2026

11-September-2026
