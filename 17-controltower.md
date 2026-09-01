
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


31-August-2026

1-September-2026
