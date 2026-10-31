
<img width="764" height="401" alt="images (6)" src="https://github.com/user-attachments/assets/a08026f2-aad8-43c4-a6df-1bd11456089e" />


Fikar bilkul mat karein! AWS mein hazaron services hain, isliye shuru mein yeh dekh kar confuse hona bilkul natural hai. Lekin exam ke point of view se Migration family ki in 3 services ka farq samajhna bohot aasan hai.

Inko ek real-life **"Ghar Shift Karne (Relocation)"** ki example se samajhte hain:

---

### 1. Simple Real-World Analogy 🚚

Maaniyan aap ne apna purana ghar (On-Premises Data Center) chhor kar naye ghar (AWS Cloud) mein shift hona hai:

1. **AWS Application Discovery Service = (Ghar Ka Saman Ginne Wala Inspector 📋)**
* Actual shifting shuru karne se pehle ek banda aata hai jo list banata hai: *"Aap ke paas kitne kamre hain, kitna saman hai, aur konsa sofa kis TV ke sath connected hai?"*
* **AWS mein kaam:** Yeh aap ke data center ke saare VMs/servers ko scan karta hai, unki **inventory (list)** banata hai, aur check karta hai ke kon sa server kis se baatein kar raha hai.


2. **AWS Application Migration Service (AWS MGN) = (Shifting Waali Mover Truck 🚛)**
* Jab list ban jati hai, toh mover truck aati hai jo aap ke saare saman ko pack karke naye ghar mein shift karti hai.
* **AWS mein kaam:** Yeh actual **Lift-and-Shift** tool hai! Yeh aap ke server ki exact copy (image) bana kar use AWS EC2 par run kar deta hai.


3. **AWS Migration Hub = (Ghar Ke Malik Ka Progress Control Room / Board 📌)**
* Malik boardroom mein baith kar check karta hai: *"Kitna saman shift ho gaya hai, kitna baqi hai?"*
* **AWS mein kaam:** Yeh ek single dashboard/console hai jo aap ko **progress track** karke dikhata hai.



---

### 2. Quick Exam Cheat Sheet 🔑

Exam mein question parhte hi in 3 words ko dhoondna hai:

| Agar Sawal Mein Yeh Words Aayein: | Toh Sahi Jawab Yeh Hoga: | Kyun? |
| --- | --- | --- |
| **"Inventory / Discover on-premises servers"** | **AWS Application Discovery Service** | Shuruati scan aur list banane ke liye. |
| **"Replicate / Lift-and-Shift EC2 instances"** | **AWS Application Migration Service (AWS MGN)** | Data aur VM ko copy/migrate karne ke liye. |
| **"Track / Monitor progress in one central place"** | **AWS Migration Hub** | Sab tools ki status ek jagah dekhne ke liye. |

---

31-October-2026













Is question ka step-by-step breakdown Roman Urdu mein yeh hai:

---

### Question Ka Summary:

On-premises data center mein hundreds of virtual machines (VMs) hain jinhe AWS cloud par migrate karna hai.

Migration shuru karne se pehle management ki **do key requirements** hain:

1. Sabhi on-premises servers/VMs ki **inventory/discovery** tayyar karna.
2. Har application ki migration progress ko ek jagah **centralize karke track** karna.

---

### Options Ka Breakdown:

1. **Option 1 (AWS DataSync + Amazon S3 + QuickSight):**
* **Galat:** AWS DataSync file/object level data transfer (storage migration) ke liye use hota hai. Yeh servers ki inventory discover nahi karta aur na hi application migration tracker hai.


2. **Option 2 (AWS Application Discovery Service + AWS Migration Hub):**
* **Sahi (Correct):**
* **AWS Application Discovery Service** (Discovery Connector / Agent ke zariye) on-premises data center ke servers, VMs, OS details, aur network dependencies ki poori **inventory** automatically collect karti hai.
* **AWS Migration Hub** ek central dashboard hai jahan aap Application Discovery Service ke data ko view kar sakte hain aur alag-alag AWS migration tools (jaise AWS MGN, Database Migration Service) ki overall **migration progress ko single pane of glass se track** kar sakte hain.




3. **Option 3 (AWS Application Migration Service - MGN + QuickSight):**
* **Galat:** AWS MGN actual block-level server replication/lift-and-shift migration ke liye use hota hai. Phir bhi discovery aur overall portfolio tracking ke liye Migration Hub + Application Discovery Service standard approach hai, aur MGN data ko QuickSight se tracking ke liye link karna unnecessary overhead hai.


4. **Option 4 (AWS DataSync + Migration Hub):**
* **Galat:** Again, DataSync storage data move karne ke liye hai, server VM discovery ke liye nahi.



---

### Sahi Jawab:

**Option 2:** **Use AWS Application Discovery Service and deploy the discovery connector to the on-premises data center to create an inventory of virtual machines to be migrated. Use the AWS Migration Hub console to track the migration of each application.**

> **Exam Tip:**
> * **On-premises server inventory & dependency mapping** = **AWS Application Discovery Service**
> * **Single dashboard for tracking overall migration progress** = **AWS Migration Hub**



30-September-2026
