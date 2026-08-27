

### Very important exam distinction

| Requirement                     | Think of                |
| ------------------------------- | ----------------------- |
| Normal AWS metrics              | **CloudWatch**          |
| EC2 memory/disk/process metrics | **CloudWatch Agent**    |
| RDS detailed OS/process metrics | **Enhanced Monitoring** |

### Easy memory trick

> **CloudWatch = “How is RDS doing?”**
> **Enhanced Monitoring = “What is happening inside RDS?”**

So when you see:

**“individual processes/threads + CPU + memory inside RDS”**

🚨 **Immediately think: Enhanced Monitoring.**


27-August-2026
