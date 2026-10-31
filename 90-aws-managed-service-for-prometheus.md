<img width="738" height="387" alt="images (7)" src="https://github.com/user-attachments/assets/223ba2ef-4fc1-45f4-9fb2-158d314be607" />

Aaiye, is sawal ko bhi apne usi shandar pattern ke sath step-by-step tor kar samajhte hain!

---

### 1. Sawal Kya Keh Raha Hai? (Question Breakdown) 🛑

* **Scenario:** Ek company ne apne containerized workloads (ECS, EKS, aur EC2 with Docker) ko AWS par migrate kar liya hai.
* **Current Tooling:** Company pehle se apne on-premises data center mein **Prometheus** (metrics collect karne ke liye) aur **Grafana** (dashboards aur visualization ke liye) use kar rahi hai.
* **Requirement:** Management chahti hai ke woh AWS cloud par bhi **wahi same tools (Prometheus & Grafana)** use karein, lekin bina kisi extra operational headache ke.

---

### 2. Sahi Jawab Kya Keh Raha Hai? (Correct Answer) 💡

> **Create a workspace on AWS Managed Service for Prometheus to collect container metrics. Set this workspace as the data source in AWS Managed Grafana for monitoring and data visualization.**

#### Deep-Dive Explanation:

1. **AWS Managed Service for Prometheus (AMP):** Yeh AWS ki fully managed monitoring service hai jo Prometheus-compatible metrics ko collect, store, aur query karti hai. Iske liye aap ko servers khud manage nahi karne parte.
2. **Amazon Managed Grafana (AMG):** Yeh fully managed Grafana service hai jo securely AMP (ya doosre data sources) se connect ho kar khoobsurat monitoring dashboards aur alerts banati hai.
3. Yeh dono mil kar AWS par open-source monitoring ka sab se best, scalable, aur zero-maintenance solution provide karte hain.

---

### 3. Baqi Options Kyun Ghalat Hain? ❌

* **Option 2 (Self-hosted Prometheus & Grafana on ECS):**
* *Ghalat kyun?* Khud se containers bana kar ECS par Prometheus aur Grafana run karna bohot zyada operational overhead (maintenance, patching, scaling) peda karta hai jab ke AWS managed services pehle se maujood hain.


* **Option 3 (VM Import/Export):**
* *Ghalat kyun?* Purane on-premise VM ko import kar ke EC2 par chalana cloud-native best practices ke bilkul khilaf hai.


* **Option 4 (Swapped roles):**
* *Ghalat kyun?* Is option mein roles ko ulta kar diya gaya hai (Grafana ko metrics collect karne ke liye kaha gaya hai jab ke metrics **Prometheus** collect karta hai aur Grafana sirf visualize karta hai).



---

### 🔑 Exam Keyword Memory Trick

| Question Keyword / Phrase | Direct AWS Mapping | Logic / Wajah |
| --- | --- | --- |
| **"Prometheus + Grafana monitoring on AWS / Managed Open-Source"** | **AMP (AWS Managed Service for Prometheus) + AMG (Amazon Managed Grafana)** | Metrics ke liye AMP aur visualization ke liye AMG use hota hai. |

---

31-October-2026
