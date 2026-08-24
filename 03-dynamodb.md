**Partition key and Cardinality:**


Problem: Database ka Write Capacity Units (WCU) unevenly consume ho raha hai. Iska matlab hai ke data kisi ek jagah bohot ziada ja raha hai (jisey hum AWS mein Hot Partition kehte hain), aur baki partitions khali pade hain.

We should use select those keys as partitioning keys that have high cardinality 


Example:

We have Users Table. The columns are:

- User_ID (e.g., USR-101, USR-102, USR-103...)
- Country (e.g., Pakistan, USA, UK...)
- Status (e.g., Active, Inactive...)

Low-Cardinality (Bad Partition Key): 

We select Country or Status as Partition Keys:

Why: Values will repeat (hazaron users ka country "Pakistan" ya status "Active" hoga).

Result: AWS background mein "Pakistan" waali saari request ek hi server/partition par bhej dega. Woh server over-load ho jayega (Hot Partition).

High-Cardinality (Good Partition Key):

If we select User_ID as Partition Key:

Wajah: Har row/record ke andar jo value hai woh bilkul distinct/unique hai.

Nateeja: AWS har User_ID ke data ko alag-alag physical servers par barabar (spread) kar ke store karega. Dynamic workload perfectly balance ho jayega.


### Exam rule 🧠

> **DynamoDB performance problem + uneven workload / hot partitions → choose a high-cardinality partition key.**

**High cardinality = many unique values → better distribution.**

**Low cardinality = few unique values → risk of hot partitions.**


24-August-2026
