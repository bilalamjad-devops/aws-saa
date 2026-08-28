
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


28-August-2026
