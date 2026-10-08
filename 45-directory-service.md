Aap ne bilkul sahi pakda hai! **AWS Directory Service** ka main kaam hi cloud ko aap ki company ki **Microsoft Active Directory (AD)** ke sath connect karna ya Cloud mein AD run karna hota hai.


---

### Real-Life Analogy (Company Ka ID Card System)

Jab aap kisi company mein job karte hain, toh aap ka ek **Windows Login ID aur Password** hota hai jisse aap apne office laptop par sign in karte hain, official emails kholte hain, aur private folders access karte hain.

Yeh sab backend par **Microsoft Active Directory (AD)** handle karti hai — yeh central identity manager hoti hai.

---

### AWS Directory Service Kya Karta Hai?

Jab company AWS Cloud par move hoti hai (jaise Amazon WorkSpaces virtual desktops par), toh do options hote hain:

1. **Option 1: Link With On-Premises AD (AD Connector):**
Aap chahte hain ke employees apne **wohi purane office wale ID/Password** se AWS WorkSpaces aur AWS Management Console par login kar sakein. Is ke liye **AD Connector** use hota hai jo AWS ko aap ke local office ki Active Directory se jod (link) deta hai. Users ko naye passwords nahi yaad rakhne padte.
2. **Option 2: Cloud Managed AD (AWS Managed Microsoft AD):**
Aap AWS Cloud ke andar hi poori ek nayi Active Directory chalana chahte hain jiska saara setup, patches, aur backups AWS khud manage kare.

---

### Direct Cheat Sheet for Exam (SAA-C03)

| Requirement | AWS Solution |
| --- | --- |
| **Existing On-Premises AD ko AWS se direct proxy/link karna** (No sync required) | **AD Connector** |
| **Full Managed Microsoft AD Cloud mein chalana** | **AWS Managed Microsoft AD** |
| **Simple, low-cost Linux-based AD directory (For basic user management)** | **Simple AD** |

---
---
---

Teeno components ka clear connection aur difference:

### 1. Active Directory (AD)

* **Kia hai:** Microsoft ka central database jo aapki company ke saare users, passwords, computers, aur groups ko manage karta hai (On-Premises data center mein).
* **Role:** Yeh main "source of truth" hai jahan aapke real credentials save hotay hain.

---

### 2. AWS Directory Service

* **Kia hai:** AWS ki umbrella service (main category) jo cloud mein directory services provide karti hai.
* **Iske under 3 main flavors aatay hain:**
1. **AWS Managed Microsoft AD:** Cloud mein apna poora Microsoft AD banana.
2. **Simple AD:** Small/basic directory (Samba-based), jismein Microsoft AD ke advanced features nahi hotay.
3. **AD Connector:** Direct bridge/proxy.



---

### 3. AD Connector

* **Kia hai:** Ek **gateway / redirector** jo AWS Cloud ko aapke On-Premises Active Directory se connect karta hai.
* **Kaise kaam karta hai:**
* Cloud mein koi user password save **nahi** hota.
* Jab developer AWS Console par login karta hai, **AD Connector** us request ko redirect karke On-Premises Active Directory ke paas bhejta hai verification ke liye.
* Verification successful hone par user ko **IAM Role** assign ho jata hai.



---

### Quick Summary

> **Active Directory** = Jahan users/passwords hain (On-Prem).
> **AWS Directory Service** = AWS ki Directory Management service.
> **AD Connector** = Bridge jo AWS Directory Service ko aapke On-Prem Active Directory se jodta hai.

24-September-2026

08-October-2026
