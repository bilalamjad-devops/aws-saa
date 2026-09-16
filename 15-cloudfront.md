
### 6. One very important exam concept

Remember this distinction:

| Service                     | Think                                                     |
| --------------------------- | --------------------------------------------------------- |
| **CloudFront**              | CDN / cache content near users                            |
| **Lambda@Edge**             | Run custom code at CloudFront edge                        |
| **User-Agent header**       | Information about the requesting browser/device           |
| **Response Headers Policy** | Add/remove/modify HTTP response headers                   |
| **Route 53**                | DNS routing                                               |
| **CloudFront Functions**    | Lightweight, very fast edge request/response manipulation |

For **this question**, the key clue is:

> **"based on User-Agent" + "custom logic" + "CloudFront"**

→ **Lambda@Edge**

### 🧠 Shortcut

| If question says...                                      | Think...                    |
| -------------------------------------------------------- | --------------------------- |
| SQL injection / XSS                                      | **WAF**                     |
| Too many requests from an IP                             | **WAF Rate-based rule**     |
| Run code at CloudFront edge                              | **Lambda@Edge**             |
| Add HTTP response headers                                | **Response Headers Policy** |
| Choose content based on browser/device with custom logic | **Lambda@Edge**             |
| Cache content globally                                   | **CloudFront**              |

So yes, your understanding is basically right: **Lambda@Edge lets you execute custom code at CloudFront edge locations**, and here that code examines the **User-Agent** and helps decide which image version to return.


### 🧠 Shortcut

| Requirement in question        | Immediately think  |
| ------------------------------ | ------------------ |
| Durable object storage         | **S3**             |
| Global content delivery        | **CloudFront**     |
| Application/database caching   | **ElastiCache**    |
| Data warehouse                 | **Redshift**       |
| Temporary EC2 local storage    | **Instance Store** |
| Archive/very infrequent access | **Glacier**        |

Aayein in dono sawalon ko Roman Urdu mein bilkul simple aur clear tarike se samajhte hain.

---

<img width="600" height="336" alt="Amazon_CloudFront_Origin_Access_Control_14March2024 (2)" src="https://github.com/user-attachments/assets/80d26bd5-0fa2-4145-83e4-271b6abf73e9" />


### 1. CloudFront URL Signed vs Unsigned Kya Hota Hai?

Normal halat mein jab aap CloudFront distribution banate hain, toh CloudFront aapko ek **Normal (Unsigned) URL** deta hai (jaise: `[https://d111111abcdef8.cloudfront.net/image.png](https://d111111abcdef8.cloudfront.net/image.png)`).

* **Unsigned (Normal) URL:**
* Yeh **Public** hota hai.
* Jis kisi ke paas bhi yeh link hoga, woh browser mein daal kar file access kar sakta hai. Koi token, key, ya security validation nahi hoti.


* **Signed URL:**
* Jab aapko private content protect karna hota hai (jaise paid courses, premium videos, ya personal client documents), toh aap Normal URL ko **Signed URL** banate hain.
* Backend application code (jaise AWS SDK / Lambda) Normal URL ke sath ek **Cryptographic Signature, Expiration Time (expiry date/time), aur Policy Parameters** attach kar deta hai.
* **Example Signed URL:**
`[https://d111111abcdef8.cloudfront.net/image.png?Expires=1700000000&Signature=xyz...&Key-Pair-Id=K123](https://d111111abcdef8.cloudfront.net/image.png?Expires=1700000000&Signature=xyz...&Key-Pair-Id=K123)...`
* **Kaise Kaam Karta Hai?** Jab client is Signed URL par click karta hai, toh CloudFront signature aur expiry check karta hai. Agar URL expired ho chuka ho ya tampered ho, toh CloudFront request ko access dene se block kar deta hai.



---

### 2. OAC (Origin Access Control) Kya Hai?

**OAC (Origin Access Control)** AWS CloudFront ki ek security feature hai jo **Amazon S3 Bucket ko direct internet exposure se bachati hai**.

#### Problem Without OAC:

Agar aap S3 bucket ko public rakhte hain, toh log S3 ka direct URL (`[https://mybucket.s3.amazonaws.com/file.png](https://mybucket.s3.amazonaws.com/file.png)`) use karke CloudFront ko bypass kar sakte hain. Is se CloudFront ki security (WAF, Signed URLs) aur caching bypass ho jati hai.

#### Solution With OAC:

OAC lagane se yeh setup banta hai:

```
[ User ] ────► [ CloudFront Distribution ] ────► (OAC Authentication) ────► [ Private S3 Bucket ]
                       │
                       └── Direct Public Access BLOCKED ──X──► [ S3 Bucket ]

```

1. Aap **S3 Bucket ko completely Private** kar dete hain (all public access blocked).
2. Aap CloudFront distribution ke andar **OAC create** karte hain.
3. S3 Bucket Policy mein **sirf aur sirf CloudFront ki OAC identity ko Read Permission** dete hain.
4. **Result:** Ab agar koi direct S3 URL se file kholne ki koshish karega toh usay `403 Access Denied` milega. Data **sirf aur sirf CloudFront ke zariye** hi access ho sakega.

> **Note for SAA-C03 Exam:** OAC AWS ka naya aur recommended tarika hai. Is se pehle AWS **OAI (Origin Access Identity)** use karta tha, lekin ab AWS OAC ko prefer karta hai kyunke OAC S3 Server-Side Encryption (KMS) ko bhi support karta hai.

---

30-August-2026

16-September-2026
