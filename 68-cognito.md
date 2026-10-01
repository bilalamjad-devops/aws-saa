Is question ka step-by-step breakdown Roman Urdu mein yeh hai:

---

### Question Ka Summary:

Mobile forex trading app ke confidential financial transactions ko secure karne ke liye **username aur password ke elawa ek second authentication method (Two-Factor / Multi-Factor Authentication)** add karna hai. App authentication ke liye **Amazon Cognito** use kar rahi hai.

Requirement: **AWS ki native capabilities ko use karte hue 2nd layer authentication kaise add ki jaye?**

---

### Options Ka Breakdown:

1. **Option 1 (Add MFA to Cognito User Pool):**
* **Sahi (Correct):** **Amazon Cognito User Pools** natively **Multi-Factor Authentication (MFA)** support karta hai. Aap SMS text messages ya Time-based One-Time Passwords (TOTP) apps (jaise Google Authenticator / Authy) ke zariye second layer of authentication enforce kar sakte hain. Yeh native, out-of-the-box solution hai.


2. **Option 2 (Integrate Cognito with Amazon SNS Mobile Push...):**
* **Galat:** Amazon SNS Mobile Push notifications bhejne ke liye hota hai, direct 2nd layer authentication flow handle karne ke liye nahi. Cognito natively SMS MFA ke liye SNS internal backend integration use karta hai, alag se custom SNS push flow setup karne ki zaroorat nahi hoti.


3. **Option 3 (Add a new IAM policy to a user pool in Cognito):**
* **Galat:** IAM policies AWS resources ke access permissions (Authorization) ko manage karti hain, end-user (app user) ke identity authentication ya MFA credentials check karne ke liye use nahi hotin.


4. **Option 4 (Develop a custom application...):**
* **Galat:** Custom app code likhna redundant overhead hai jab Amazon Cognito natively MFA setup ka built-in feature provide karta hai. Operational efficiency AWS native features pehle leverage karne mein hai.



---

### Sahi Jawab:

**Option 1:** **Add multi-factor authentication (MFA) to a user pool in Cognito to protect the identity of your users.**

> **Exam Tip:**
> * **User Authentication, Sign-in, Social Login, 2FA/MFA for App Users** = **Amazon Cognito User Pools**
> * **AWS Resource Access Permissions for App Users** = **Amazon Cognito Identity Pools (Federated Identities)**



01-October-2026
