**DDoS →** Shield

**SQL injection / XSS / malicious HTTP request →** WAF


**Multiple AWS accounts →** Firewall Manager


# 🧠 The important SAA distinction

Memorize this:

| Requirement                                | Think                   |
| ------------------------------------------ | ----------------------- |
| SQL injection                              | **WAF**                 |
| XSS                                        | **WAF**                 |
| HTTP request filtering                     | **WAF**                 |
| Block requests based on HTTP conditions    | **WAF regular rule**    |
| Too many requests from an IP               | **WAF rate-based rule** |
| Subnet-level network filtering             | **NACL**                |
| Instance-level filtering                   | **Security Group**      |
| DDoS protection                            | **AWS Shield**          |
| Private connectivity between VPCs/services | **PrivateLink**         |



# 🧠 The important comparison

| Service              | What does it do?                         | Think                              |
| -------------------- | ---------------------------------------- | ---------------------------------- |
| **AWS WAF**          | Inspects/filters web requests            | 🛡️ SQL injection, XSS             |
| **AWS X-Ray**        | Traces application requests              | 🔍 Find where app is slow          |
| **Firewall Manager** | Centrally manages security policies      | 🏢 Multiple AWS accounts           |
| **NACL**             | Controls network traffic at subnet level | 🌐 IP/port/network                 |
| **Security Group**   | Controls traffic to ENI/instance         | 🔐 Instance-level network firewall |

### 🔥 SAA shortcut

When you see:

**SQL injection / XSS / malicious HTTP request**

→ **WAF**

When you see:

**trace request / troubleshoot latency / distributed application**

→ **X-Ray**

When you see:

**centrally apply WAF/security policies across multiple AWS accounts**

→ **Firewall Manager**

When you see:

**allow/deny IP, subnet, port traffic**

→ **NACL / Security Group**

---

### One more important distinction

Don't think:

> "Firewall Manager blocks attacks."

Think:

> **WAF blocks web attacks. Firewall Manager manages/enforces WAF/security policies centrally.**

That's the distinction this question wants you to learn.


27-August-2026

28-August-2026

29-August-2026
