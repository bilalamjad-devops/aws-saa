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


# 🧠 Exam shortcut

When you see:

**"Key-value store"**

👉 **DynamoDB**

When you see:

**"Document database / document model"**

👉 **DynamoDB**

When you see:

**"Relational / SQL"**

👉 **RDS / Aurora**

When you see:

**"Collaborate/edit/share documents"**

👉 **WorkDocs**

---

### Q15 in one line:

> **The application needs a key-value/document database → DynamoDB.**

Don't overthink the ECS/Fargate part. **The database requirement is the giveaway.**


<img width="658" height="406" alt="2018-10-23_05-24-29-74b3e6dadc8ce683ccd2a5bd00f99889" src="https://github.com/user-attachments/assets/11de6d8a-d642-44b5-a6b0-dca0915fd1e2" />


# 13. The most important concepts from this question

You can put this tiny table in your notes:

| Requirement                                  | Service                       |
| -------------------------------------------- | ----------------------------- |
| Private access to DynamoDB from VPC          | **DynamoDB Gateway Endpoint** |
| Private access to S3 from VPC                | **S3 Gateway Endpoint**       |
| Restore DynamoDB to an earlier point in time | **PITR**                      |
| Cross-account DynamoDB backup                | **AWS Backup**                |
| Time-series data                             | **Amazon Timestream**         |
| Network traffic inspection/firewall          | **AWS Network Firewall**      |

---

<img width="1105" height="804" alt="amazon-dynamodb-gateway-endpoint (1)" src="https://github.com/user-attachments/assets/7c77137e-f155-456e-992a-fd0311b206f8" />



24-August-2026

31-August-2026

1-September-2026
