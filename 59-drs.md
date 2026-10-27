15. Question

An e-commerce company plans to optimize its disaster recovery configuration using AWS Cloud to minimize operational disruptions during outages or major system maintenance for its on-premises Microsoft SQL Server-based application. The objective is to achieve a recovery point objective (RPO) of 60 seconds or less and a recovery time objective (RTO) of 1 hour.

Which of the following is the MOST cost-effective solution for this scenario?

- Use Microsoft SQL Server Enterprise with Always On availability groups and set up a multi-site active/active setup between the corporate on-premises application and AWS.
- On AWS, implement a warm standby using Amazon RDS for SQL Server database and configure AWS Database Migration Service (AWS DMS) with change data capture (CDC) to sync the data from the on-premises application.
- Back up SQL Server to AWS Storage Gateway for hybrid storage and fast disaster recovery. Enable fast snapshot restore in Amazon Elastic Block Store (Amazon EBS).
- `Set up a pilot light strategy using AWS Elastic Disaster Recovery (AWS DRS) to replicate the changes of the on-premises application to AWS`

### 1. Sawal Kya Keh Raha Hai? (Question Breakdown) ❓

* **Scenario:** Ek e-commerce company apne on-premises **Microsoft SQL Server-based application** ke liye AWS par Disaster Recovery (DR) solution optimize karna chahti hai.
* **Requirements:**
1. **RPO (Recovery Point Objective):** $\le 60$ seconds (data loss 1 minute se kam hona chahiye).
2. **RTO (Recovery Time Objective):** $\le 1$ hour (system 1 ghante ke andar wapis up & running ho jaye).
3. **Constraint:** Sab se **MOST cost-effective** solution hona chahiye jo minimum operational disruption de.



---

### 2. Sahi Jawab Kya Keh Raha Hai? (Correct Answer) 💡

* **Option:** *Set up a pilot light strategy using AWS Elastic Disaster Recovery (AWS DRS) to replicate the changes of the on-premises application to AWS*
* **Wazahat:**
* **AWS Elastic Disaster Recovery (AWS DRS)** block-level continuous data replication use karta hai jo sub-second se le kar seconds tak ka **RPO** easily meet karta hai.
* **Pilot Light strategy** sab se zyada cost-effective hoti hai kyunke yeh continuous replication ke waqt sirf low-cost compute aur storage (jaise staging resources) use karti hai. Full-capacity resources (jaise high-spec EC2/RDS instances) sirf failover (disaster) ke waqt launch hote hain.
* Active-Active ya Multi-Site setups bohot expensive hote hain, jabke AWS Storage Gateway + EBS snapshots se RPO/RTO meet karna aur failover manage karna slow/complex ho sakta hai.



---

### 3. Keyword Scanning Cheat Sheet 🔑

| Question Keyword / Phrase | Direct Exam Mapping | Logic / Wajah |
| --- | --- | --- |
| **"On-premises application DR to AWS"** | **AWS Elastic Disaster Recovery (AWS DRS)** | AWS DRS (pehle CloudEndure DR) specifically on-prem/hybrid servers ko AWS par continuous replicate aur recover karne ke liye bani hai. |
| **"RPO $\le$ 60 seconds" + "Cost-effective"** | **Pilot Light Strategy (AWS DRS)** | Continuous block-level replication (DRS) RPO ko seconds mein rakhti hai, aur Pilot Light strategy ongoing costs ko bare minimum rakhti hai. |
| **"Active/Active setup"** | **Costly / Over-engineered (Eliminate)** | Active/Active RTO/RPO near zero deta hai lekin sab se mahanga hota hai, jo "cost-effective" constraint ko fail karta hai. |

---
---
---

In charon terms ko aasan alfaz mein aur real-life examples ke sath samajhte hain, taake exam mein yeh kabhi na bhoolein:

---

### 1. RPO — **Recovery Point Objective** ⏱️ (Data Loss Limit)

* **Kya hai?** RPO batata hai ke **aap kitna data loss bardasht kar sakte hain** jab koi disaster (crash) ho jaye. Iska measurement waqt (time) mein hota hai.
* **Misal:** Agar aap ka RPO **60 seconds** hai, iska matlab hai ke disaster ke waqt agar system down hua, toh pichle 1 minute (60 seconds) ka data zaya ho sakta hai, lekin us se pehle ka sara data safe hona chahiye.
* *Note:* Jitna chota RPO hoga (jaise near-zero), utna hi data safe rahega lekin utna hi system expensive hoga.

---

### 2. RTO — **Recovery Time Objective** 🚀 (Recovery Time Limit)

* **Kya hai?** RTO batata hai ke disaster hone ke baad **system ko kitni der mein wapis on (recover) ho jana chahiye**. Iska measurement bhi waqt mein hota hai.
* **Misal:** Agar aap ka RTO **1 hour** hai, iska matlab hai ke agar subah 10 baje server crash hua, toh 11 baje tak application har halat mein dobara live aur running honi chahiye.

---

### 3. Pilot Light Strategy 🕯️ (DR Strategy)

Disaster Recovery (DR) ki mukhtalif strategies hoti hain (Backup/Restore, Pilot Light, Warm Standby, Active-Active). **Pilot Light** sab se popular aur cost-effective hai:

* **Kaise kaam karti hai?** Is strategy mein core cheezein (jaise database ki continuous replication) hamesha on rehti hain (yeh "pilot light" ya choti si jot ki tarah background mein chalti rehti hain).
* Lekin application servers (compute layer) band rehte hain aur koi heavy resource paise zaya nahi kar raha hota. Jab disaster aata hai, toh AWS automation ke zariye un band servers ko foran on kar deta hai aur database ke sath connect kar deta hai. Yeh **kam kharch mein behtareen backup** deta hai.

---

### 4. AWS DRS — **AWS Elastic Disaster Recovery** 🔄 (The Tool)

* **Kya hai?** Agar aap ne ise pehle use nahi kiya toh koi baat nahi — AWS DRS aaj ke دور mein AWS ka **main aur sab se powerful automated Disaster Recovery tool** hai (isne purane CloudEndure service ko replace kiya hai).
* **Kaise kaam karta hai?** Aap apne on-premises servers (ya doosre cloud ke servers) par ek chota sa agent install karte hain. Yeh agent aap ke server ka data **block-level par continuous replicate** kar ke AWS mein bhejta rehta hai.
* Jab asli disaster aata hai, toh aap aik click kar ke AWS par apne servers ko foran launch kar lete hain. Iski replication itni fast hoti hai ke yeh **RPO seconds mein aur RTO minutes mein** achieve kar leta hai.

---
---
---

Bilkul theek samjhe aap! 🎯 Aap ka concept bilkul on-point hai.

### Agent Kahan Install Hota Hai? 🖥️

* Agent hamesha **on-premises servers** par install hota hai (woh servers jo aap ke apne office ya data center mein chal rahe hain).
* Yeh agent background mein chupchaap aap ke server ka data block-by-block copy kar ke **AWS (Staging Area)** mein bhejta rehta hai.

### Database Failover ke Hawalay se Choti si Clarification 💡

* **Agar aap ka SQL Server on-premises kisi Virtual Machine (VM) ya Physical Server par chal raha hai:**
Toh **AWS DRS** poore ke poore server (OS + Database files + Application) ko AWS par replicate kar raha hota hai. Jab on-prem server down hota hai, toh aap DRS ke zariye AWS par foran failover kar ke wahi server live kar lete hain.
* **Agar aap managed database (jaise Amazon RDS) use kar rahe hain:**
Toh RDS ke apne built-in features hote hain (jaise Multi-AZ ya Cross-Region Read Replicas) jo hum ne thori dair pehle discuss kiye thay. Lekin is specific sawal mein on-premises SQL Server ki baat ho rahi thi, is liye wahan **AWS DRS (Pilot Light)** sab se best aur cost-effective option tha.

---

25-October-2026

26-October-2026

27-October-2026



---
---
---

Bilkul! **AWS DRS (Elastic Disaster Recovery)** ko ek simple real-life misaal se samajhte hain.

### Real-Life Misaal: "Generator aur Aap ka Ghar" 🏡🔌

Maan lijiye aap ke ghar (On-Premises Data Center) mein WAPDA ki bijli (Main Server) aa rahi hai. Aap chahte hain ke agar bijli chali jaye (Disaster), toh aap ka ghar thodi dair baad dobara roshan ho jaye, lekin aap **generator chalane ka zyada kharcha bhi nahi karna chahte**.

**Baqi DR (Disaster Recovery) Options (Mehnge):**

* **Active/Active:** Aap WAPDA ke sath sath, 24/7 ek mehnga generator bhi chala ke rakhein. (Faida: Bijli 1 second ke liye bhi nahi jaye gi. Nuqsan: Kharcha boht zyada).
* **Warm Standby:** Aap ek chota UPS/generator har waqt "On" rakhein (RDS Database 24/7 chalta rahe). Kharcha medium hai.

**AWS DRS (Pilot Light Strategy - Sasta aur Behtareen):**
Yeh aise hai ke aap ne apna generator **band (OFF)** rakha hua hai (no compute cost on AWS), lekin us ka ek automatic switch aap ke ghar ke main board se connected hai.

* Jab WAPDA ki bijli chalti rehti hai, toh AWS par server band rehta hai (sirf data ki sasti copy S3 jaisi jagah par save ho rahi hoti hai). Is wajah se bill boht **kam** aata hai.
* Jaise hi WAPDA ki bijli fail (Disaster) hoti hai, **AWS DRS** foran us generator ko (EC2 instances ko) "START" kar deta hai.
* Ek ghante (ya minutes) ke andar aap ki application cloud par zinda ho jati hai.

### Simple Words Mein AWS DRS Kya Hai?

**AWS DRS (Elastic Disaster Recovery)** ek aisa service hai jo aap ke apne office ke server ke poore data/software ka har waqt ek sasta "snapshot/copy" AWS mein chhupa kar rakhta hai. Jab aap ka apna server down hota hai, yeh us data ko utha kar AWS par jaldi se naye servers bana kar system dobara chala deta hai, taake aap ka system ziada dair band na rahay, aur bill bhi kam aaye.

---


---
---
---

Koi baat nahi! Aayein isay bilkul simple Urdu/English mein aur ek zordar real-life example se samajhte hain.

---

### Pehle 2 Simple Terms Samajh Lein:

1. **RPO (Data Loss Time):** Question keh raha hai ke disaster aaye toh ziada se ziada **60 seconds (1 minute)** ka data ghoomna chahiye, us se ziada nahi. Is ka matlab data **sath ke sath copy (replicate)** hota rahe.
2. **RTO (System Wapas Up Karne Ka Time):** System fail hone ke baad **1 ghante (1 hour)** ke andar poori application cloud par dobara live ho jani chahiye.

---

### DRS (AWS Elastic Disaster Recovery) Kya Hai?

Aap ne **RDS (Relational Database Service)** parha hai jo AWS ka Cloud Database hai.

Lekin **DRS (Disaster Recovery Service)** ek aisi service hai jo aap ke **On-Premises (Aap ke apne physical office/data center ke servers)** ko target karti hai:

* Yeh aap ke physical server ke poore data (Disk/Files/Database) ki ek **chhoti si, sasti copy (replication)** AWS par har waqt sync rakhti hai.
* Jab tak aap ke office ke servers chal rahe hain, AWS par koi mehnga server **Nahi Chalega** (sirf sasti storage use hogi — isay hum **Pilot Light** kehte hain).
* Jaise hi office mein aag lag jaye ya server blast ho jaye, **DRS** minute ke andar AWS par auto-servers start karke aap ki application wapas live kar deta hai.

---

### Teeno Galat Options Kyun Fail Hue?

1. **Option 1 (RDS + DMS):** Agar aap AWS par 24/7 RDS SQL Server database chalta chhor denge, toh bill **boht zyada (expensive)** aaye ga. Question ne poocha hai **MOST cost-effective** (sab se sasta).
2. **Option 2 (Backups):** Pehle backup banana aur phir AWS par poora database restore karna — is mein **boht ghante lag jate hain**, RTO requirement poori nahi hoti.
3. **Option 3 (Active/Active Setup):** Dono jagah 24/7 full expensive servers chalanay parenge — yeh sab se mehnga option hai.

---

### Aasan Khulasa (Bottom Line) 💡

> **On-Premises se AWS par Disaster Recovery (DR) + Minimal Cost + Fast RPO/RTO** $\rightarrow$ **AWS DRS (Elastic Disaster Recovery) using Pilot Light Strategy**.


28-September-2026
