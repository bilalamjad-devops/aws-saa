<img width="764" height="401" alt="images (5)" src="https://github.com/user-attachments/assets/1e31a5ac-ee8f-4626-a748-9999d7279108" />

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
