
# 2. What is AD?

**AD = Active Directory.**

Microsoft's directory service commonly used by organizations to manage:

* users
* passwords
* computers
* groups
* permissions

Example:

```text
Company AD

Users:
Bilal
Ali
Ahmed
Sara

Groups:
Developers
Finance
HR
Architects
```

So when Question 63 says:

> "corporate AD"

think:

> **The company's existing user database.**

---

# 3. What is LDAP?

**LDAP = Lightweight Directory Access Protocol.**

It's a protocol used to communicate with directory services.

Very simplified:

```text
Application
     |
    LDAP
     ↓
Directory
     |
Users / Groups / Credentials
```

AD can support LDAP.

So for the exam, you can roughly think:

> **AD = directory system**

> **LDAP = protocol used to communicate with directory services**

Don't confuse LDAP with S3 or IAM. They solve completely different problems.

---

# 4. What is Federation?

This is the BIG concept.

Normally, without federation:

```text
Employee
   ↓
AWS IAM User
   ↓
AWS
```

You would have to create AWS identities.

But with federation:

```text
Employee
   ↓
Corporate AD
   ↓
Federation
   ↓
AWS
```

AWS trusts the company's identity system.

So the employee can use their **existing corporate identity**.

### Simple definition:

> **Federation = allowing users from an external identity system to access AWS without creating separate IAM users for them.**


# 🧠 Shortcut table

| Term              | Simple meaning                              | Think                              |
| ----------------- | ------------------------------------------- | ---------------------------------- |
| **AD**            | Company's user directory                    | "Where our employees exist"        |
| **LDAP**          | Protocol for communicating with directories | "Talk to directory"                |
| **Federation**    | Use external identity to access AWS         | "Use company login in AWS"         |
| **SSO**           | Login once using existing identity          | "No separate AWS login"            |
| **SAML**          | Standard used for federation                | "Identity information exchange"    |
| **IdP**           | Identity Provider                           | "I verify who you are"             |
| **STS**           | Issues temporary AWS credentials            | "Temporary access"                 |
| **IAM Role**      | Set of AWS permissions                      | "What can you do?"                 |
| **IAM Policy**    | Detailed permission rules                   | "Exactly what can you access?"     |
| **Okta/OneLogin** | Third-party identity/SSO solutions          | "Optional IdP products"            |
| **IAM Users**     | Permanent AWS identities                    | Avoid creating 1,200 unnecessarily |

### ⭐ Exam shortcut

If you see:

**"Existing corporate AD + SSO + AWS access"**

→ **Federation / SAML**

If you see:

**"temporary credentials for federated users"**

→ **STS**

If you see:

**"what can the user access?"**

→ **IAM Role + IAM Policy**

If you see:

**"1200 employees already exist in corporate directory; don't create IAM users"**

→ **Federation, not 1,200 IAM users.**


<img width="845" height="475" alt="saml-based-federation diagram (1)" src="https://github.com/user-attachments/assets/5b05b398-5b61-4515-8e51-80cb63cecbac" />


28-August-2026

You're **very close** 👍 — just one important correction.

### 1. IAM Policy → IAM Role

Yes ✅

```text
IAM Policy
     ↓ attach
 IAM Role
```

This is an **identity-based policy**.

> "This role can read from S3."

---

### 2. S3 Bucket Policy

Here, don't call it an "IAM policy attached to S3."

It is specifically a **resource-based policy** created for the S3 bucket.

```text
S3 Bucket
   ↓
Bucket Policy
```

> "This IAM role/account/service is allowed to access this bucket."

So technically:

❌ "IAM policy attached to S3"

✅ "S3 Bucket Policy"

---

### 3. Endpoint Policy

Same idea:

```text
VPC Endpoint
     ↓
Endpoint Policy
```

It controls what can be accessed **through that endpoint**.

And again:

❌ "IAM policy attached to VPC"

✅ "Endpoint Policy attached to the VPC endpoint"

---

### 🧠 Your mental model

Think of **policy = permission rules**, but AWS has different places/types of policies:

```text
                 POLICY
                   │
       ┌───────────┼────────────┐
       ↓           ↓            ↓
 IAM Policy   Bucket Policy   Endpoint Policy
       │           │            │
       ↓           ↓            ↓
 IAM Role       S3 Bucket    VPC Endpoint
```

The **big distinction** for your SAA exam:

> **IAM policy → identity-based permissions**

> **Bucket policy → S3 resource-based permissions**

> **Endpoint policy → controls access through the VPC endpoint**

You're building the right mental model. Just don't say **"IAM policy attached to bucket"**—call it a **bucket policy**.

31-August-2026
