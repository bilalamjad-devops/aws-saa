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
