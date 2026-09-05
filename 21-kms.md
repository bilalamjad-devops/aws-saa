<img width="2017" height="1261" alt="HHs6YsuRKgdFY4TzvN3gygG9Q7M2-p323hiz" src="https://github.com/user-attachments/assets/37fc9a26-b755-4bec-8e7f-78c9eb1f3837" />


## 5. Exam Decision Matrix (Cheat Sheet)

* **Keywords: "Rotate credentials automatically", "RDS DB Passwords Rotation", "Manage API Keys":** $\rightarrow$ **AWS Secrets Manager**
* **Keywords: "Store config settings", "License keys", "Free/Cheap Parameter Storage", "No native auto-rotation needed":** $\rightarrow$ **SSM Parameter Store**
* **Keywords: "Encrypt data at rest", "Manage KMS Master Keys":** $\rightarrow$ **AWS KMS**
* **Keywords: "HTTPS / SSL / TLS Certificates":** $\rightarrow$ **AWS ACM**

# 🆚 6. Secrets Manager vs KMS vs ACM vs Parameter Store

This table is extremely useful for SAA.

| Service             | Main purpose              | Store secrets? |              Automatic secret rotation? |
| ------------------- | ------------------------- | -------------: | --------------------------------------: |
| **Secrets Manager** | **Store/manage secrets**  |              ✅ |                                       ✅ |
| **KMS**             | Encryption key management |              ❌ | KMS rotates keys, not your DB passwords |
| **ACM**             | SSL/TLS certificates      |              ❌ |                  Certificate management |
| **Parameter Store** | Configuration parameters  | ✅ SecureString |          ❌ Not automatically by default |

---

5-September-2026
