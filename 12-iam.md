
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


28-August-2026
