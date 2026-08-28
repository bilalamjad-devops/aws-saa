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



27-August-2026

28-August-2026
