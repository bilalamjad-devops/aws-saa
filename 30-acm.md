Is question mein **SSL/TLS Certificates (AWS Certificate Manager - ACM)**, **Application Load Balancer (ALB)**, aur **Server Name Indication (SNI)** ka concept test ho raha hai.

Aayein pehle question aur is ke saare options ko bilkul aasan lafzon mein samajhte hain.

---

## 1. Question Ka Matlab (Simple Words)

* **Current Setup:** Travel company ki multiple websites/domains hain:
* `i-love-manila.com`
* `i-love-boracay.com`
* `i-love-cebu.com`
*(Ghor karein: Yeh **different domains** hain, sub-domains nahi).*


* **Requirement:**
1. Unhein in tamam domains par **HTTPS (SSL/TLS)** enable karna hai security aur SEO ranking ke liye.
2. Jab bhi koi **naya domain** add ho, toh purane certificate ko re-authenticate/re-provision na karna pade (low operational overhead).
3. Sab se **cost-effective** tarika choose karna hai.



---

## 2. Core AWS Concepts: SNI vs Wildcard vs SAN vs Dedicated IP

```
┌─────────────────────────────────────────────────────────────────────────┐
│                      SSL / TLS CERTIFICATE METHODS                      │
├──────────────────────────┬──────────────────────┬───────────────────────┤
│ Server Name Indication   │ Wildcard Certificate │ SAN (Subject Alt Name)│
│ (SNI)                    │                      │                       │
│ Load balancer par        │ *.domain.com         │ single certificate    │
│ MULTIPLE certificates    │ Single domain ke     │ containing list of    │
│ bind karo. ALB auto-     │ multiple SUB-DOMAINS │ multiple different    │
│ choose karta hai.        │ ke liye work karta   │ domains (requires     │
│                          │ hai.                 │ re-issuing on change).│
└──────────────────────────┴──────────────────────┴───────────────────────┘

```

1. **Server Name Indication (SNI):**
* SNI TLS protocol ka ek extension hai. Yeh **Application Load Balancer (ALB)** ko allow karta hai ke woh ek hi Secure Listener (Port 443) par **multiple individual SSL certificates** bind kar sake.
* Jab koi client (browser) request bhejta hai, ALB SNI header dekh kar automatically correct SSL certificate serve kar deta hai.
* **AWS ACM Certificates ALB par FREE hote hain**, is liye yeh sab se cost-effective aur scaleable solution hai.


2. **Wildcard Certificate (`*.domain.com`):**
* Wildcard sirf ek specific domain ke **sub-domains** ke liye kaam karta hai (e.g., `app.i-love-manila.com`, `blog.i-love-manila.com`).
* Yeh do **alag domains** (`i-love-manila.com` aur `i-love-boracay.com`) ke liye kaam **nahi** kar sakta.


3. **SAN Certificate (Subject Alternative Name):**
* Ek hi certificate mein multiple domains add kiye ja sakte hain. LEKIN jab bhi koi **naya domain** add hoga, aap ko poora certificate re-issue / re-provision karna padega, jo question ki requirement ko violate karta hai.



---

## 3. Correct Option Explanation

#### ✅ **Upload all SSL certificates of the domains in the ALB using the console and bind multiple certificates to the same secure listener on your load balancer. ALB will automatically choose the optimal TLS certificate for each client using Server Name Indication (SNI).**

* **Why it works:**
1. **SNI Support:** ALB par SNI use karke aap har alag domain ka apna SSL certificate bind kar sakte hain.
2. **Zero Re-Authentication of Existing Domains:** Jab naya domain aaye, bas uska naya ACM certificate bana kar ALB par attach kar dein. Baaki purane domains/certificates ko cheedna nahi padega.
3. **Most Cost-Effective:** ACM certificates AWS Load Balancers ke sath **FREE** hotay hain.



---

## 4. Incorrect Options Breakdown (Elimination Strategy)

| Option | Why It Fails the Exam Requirement |
| --- | --- |
| **Use a wildcard certificate...** | **Technical Limitations:** Wildcard (`*.example.com`) sub-domains ke liye hota hai. Different domains (`domainA.com`, `domainB.com`) ke liye wildcard use nahi ho sakta. |
| **CloudFront web distribution with dedicated IP addresses...** | **Extremely Costly & Unnecessary:** CloudFront mein Dedicated IP Custom SSL options **thousands of dollars per month** consume karte hain. Simple ALB + SNI se kaam ho sakta hai. |
| **Add a Subject Alternative Name (SAN)...** | **Fails Operational Requirement:** Multi-Domain SAN certificate mein jab bhi naya domain add karenge, certificate ko update aur re-provision karna padega. |

---

## 5. Exam Decision Matrix (SSL / ALB Cheat Sheet)

* **Multiple DIFFERENT domains on same ALB listener:** $\rightarrow$ **ALB with SNI (Server Name Indication)**
* **Multiple SUB-DOMAINS of same parent domain (`*.example.com`):** $\rightarrow$ **Wildcard Certificate**
* **Free Managed SSL Certificates in AWS:** $\rightarrow$ **AWS Certificate Manager (ACM)**

---


12-September-2026
