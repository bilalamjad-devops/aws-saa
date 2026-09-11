**Bilkul, aap ne bilkul sahi samjha hai!**

AWS DMS sirf ek database se doosre database mein data transfer nahi karta, balke is ki ek bohot powerful capability yeh hai ke yeh **Amazon S3 ko as a Target** support karta hai.

---

### **AWS DMS Target Amazon S3 Key Features:**

1. **Automatic Conversion to CSV / Parquet:**
* Jab aap source database (jaise MySQL, Oracle, SQL Server, PostgreSQL) ko AWS DMS se connect karte hain aur target **Amazon S3** select karte hain, toh DMS database ke tables, rows, aur columns ko **automatically `.csv` format files** mein convert kar ke S3 bucket mein dump kar deta hai.
* Aap settings mein option change karke formatting ko **Apache Parquet (`.parquet`)** par bhi set kar sakte hain taake S3 par cost-effective storage aur faster Athena queries ho sakein.


2. **Full Load + Continuous Streaming (CDC):**
* **Full Load:** On-premises database ka saara existing data S3 bucket mein CSV files banakar upload kar deta hai.
* **Change Data Capture (CDC):** Target S3 bucket mein ongoing DB changes (Inserts, Updates, Deletes) ki **alag se incremental CSV files** continuously stream karta rehta hai.


3. **On-Premises to Cloud Direct Sync:**
* DMS Agent / Replication Instance On-Premises database se connect hokar encryption (SSL/TLS) ke sath data securely S3 tak pahunchata hai.



---

### **Exam Summary (AWS SAA-C03 Rule):**

> Jab bhi exam question mein query aaye ke **"On-Premises Database se live continuous changes ko S3 bucket mein CSV/Parquet format mein dump karna hai"**, aap ka immediate answer **AWS DMS (Full Load + CDC)** hona chahiye!
>
> 11-September-2026
