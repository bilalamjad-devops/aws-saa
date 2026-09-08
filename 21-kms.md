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


<img width="765" height="196" alt="s3_sse_customer_key_2" src="https://github.com/user-attachments/assets/85b80096-0718-4093-909d-39c37f28e5c9" />

Absolutely — I’ll keep it **short and crisp** from now on.

## 🎯 What is the question really asking?

The bucket requires **SSE-S3 encryption**.

So we need the HTTP header that tells S3:

> “Encrypt this object using S3-managed keys.”

### ✅ Correct:

`x-amz-server-side-encryption`

---

## 🧠 Remember the 3 S3 encryption types

| Encryption  | Who manages the key?  | Important header                          |
| ----------- | --------------------- | ----------------------------------------- |
| **SSE-S3**  | AWS/S3                | `x-amz-server-side-encryption`            |
| **SSE-KMS** | AWS KMS               | `x-amz-server-side-encryption: aws:kms`   |
| **SSE-C**   | Customer provides key | `x-amz-server-side-encryption-customer-*` |

### 🔥 Exam shortcut

If you see:

> **customer-provided encryption key**

think **SSE-C** → the 3 `customer-*` headers.

If you see:

> **S3-managed encryption keys / AES-256**

think **SSE-S3** → `x-amz-server-side-encryption`.

### Final answer

**`x-amz-server-side-encryption`** ✅



5-September-2026

8-September-2026
