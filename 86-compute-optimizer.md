

<img width="738" height="414" alt="images (3)" src="https://github.com/user-attachments/assets/44a462d9-9ffd-4912-997b-e470b8d4859f" />

### 1. Sawal Kya Keh Raha Hai? (Question Breakdown) ❓

* **Scenario:** Ek FinTech company ne AWS par compute workloads (EC2 instances, Auto Scaling groups, aur Lambda functions) deploy kiye hain.
* **Problem:** Users slow performance ki shikayat kar rahe hain, aur QA engineers ko shak hai ke **servers traffic handle nahi kar pa rahe (overutilized / resource bottleneck)**.
* **Goal:** Aisa action lena hai jo is performance issue ko **verify aur resolve** kar sake.

---

### 2. Sahi Jawab Kya Keh Raha Hai? (Correct Answer) 💡

* **Option:** *Enable AWS Compute Optimizer to see recommendations on optimal sizing of compute-related resources. Implement changes based on the recommendations.*
* **Wazahat:**
* **AWS Compute Optimizer:** Yeh machine learning par mabni service hai jo historical utilization metrics (jaise CPU, memory, EBS performance) ko analyze karti hai aur yeh batati hai ke konsa EC2 instance, Auto Scaling group, ya Lambda function **underprovisioned (chota pad raha hai / slow hai)** ya **overprovisioned** hai.
* Yeh na sirf performance issues ko verify karti hai balkay **optimal rightsizing recommendations** bhi deti hai taake issues resolve kiye ja saken.



*Kyunki baqi options ghalat hain:*

* *Trusted Advisor (Cost Optimization category):* Trusted Advisor ka Cost optimization category **underutilized / idle** resources ko identify karta hai (cost bachane ke liye), jabke yahan problem slow performance (overutilization / high load) ki hai.
* *AWS Cost Explorer:* Yeh sirf cost tracking aur budgeting ke liye hai, performance metrics ya server sizing recommendations ke liye nahi.
* *CloudWatch:* CloudWatch metrics dikha sakta hai aur dashboard bana sakta hai, lekin yeh khud se machine-learning powered optimal sizing recommendations generate nahi karta jo Compute Optimizer karta hai. (Exam mein jab optimal sizing aur automated recommendations ki baat ho, toh Compute Optimizer correct choice hota hai).

---

### 3. Keyword Scanning Cheat Sheet 🔑

| Question Keyword / Phrase | Direct Exam Mapping | Logic / Wajah |
| --- | --- | --- |
| **"Optimal sizing" / "Resource recommendations" / "Handle traffic / performance tuning"** | **AWS Compute Optimizer** | Compute resources ki performance analyze karke unhein right-size karne ke liye Compute Optimizer use hota hai. |
| **"Cost optimization category" (Trusted Advisor trap)** | **Cost reduction vs Performance** | Trusted Advisor ka cost check underutilized resources dhoondta hai, performance bottleneck ke liye nahi. |

---

30-October-2026
