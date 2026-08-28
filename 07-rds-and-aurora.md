**RDS Event:** "Something happened to my database service."

```rdsevent
Instance failure
Failover
Backup
Maintenance
Configuration changes
```



**Aurora Lambda integration:** "Something happened to data inside my database."

```auroraLambdaIntegration
INSERT
UPDATE
DELETE
```


**Multi-AZ:** Standby + Synchronous + HA

**Read Replica:** Read scaling + Asynchronous

**RDS Read Replica =** DynamoDB Global Tables


## Exam shortcut 🧠

When you see:

**“frequent schema changes”**

→ **DynamoDB**

When you see:

**“complex relationships / SQL / transactions”**

→ **RDS / Aurora**

When you see:

**“high-performance relational database”**

→ **Aurora**

When you see:

**“data warehouse / OLAP / analytics”**

→ **Redshift**

When you see:

**“massive scale + millisecond/low-latency + NoSQL”**

→ **DynamoDB**

### For Question 52:

**Frequent schema changes** → NoSQL
**High traffic** → DynamoDB
**Low latency** → DynamoDB
**Global scalability** → DynamoDB

✅ **Answer: Amazon DynamoDB**



## 6. Your SAA memory table

| Service/concept           | Think                                   |
| ------------------------- | --------------------------------------- |
| **IAM Role**              | Give AWS permissions to EC2             |
| **STS**                   | Temporary AWS credentials               |
| **IAM DB Authentication** | Temporary authentication token for RDS  |
| **SSL/TLS**               | Encrypt data in transit                 |
| **Secrets Manager**       | Store/rotate database passwords/secrets |
| **RDS Multi-AZ**          | High availability                       |
| **RDS Read Replica**      | Read scaling                            |


24-August-2026

27-August-2026

28-August-2026
