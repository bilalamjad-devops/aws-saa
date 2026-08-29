


**Site-to-Site VPN:** We use this when we want to connect our on-premises data center's VPC to AWS VPC. We use 2 gateways. Customer Gateway and VPC Gateway. 


**SG:** Stateful firewall at instance level.

**EC2 traffic** → Security Group

**NACL:** Stateless firewall at subnet level.



**Subnet traffic** → NACL


VPC Peering (Incorrect): VPC Peering sirf do AWS VPCs ke darmiyan hota hai. On-premises network ko VPC se connect karne ke liye AWS Direct Connect ya AWS Site-to-Site VPN lagta hai, VPC Peering kaam nahi karta!

Absolutely 👍

From now on, for every SAA question we discuss, I’ll end with a **“⚡ Shortcut for Exam”** table.

For example, for Question 58:

| Clue in question              | Think of                              |
| ----------------------------- | ------------------------------------- |
| On-premises → AWS storage     | **Storage Gateway**                   |
| SMB / Windows files           | **File Gateway**                      |
| NFS / Linux files             | **File Gateway**                      |
| Local cache + low latency     | **File Gateway**                      |
| Transfer/migrate lots of data | **DataSync**                          |
| Dedicated network connection  | **Direct Connect**                    |
| Long-term cheap archive       | **S3 Glacier / Glacier Deep Archive** |
| Virtual tape backup           | **Tape Gateway**                      |
| Block storage / iSCSI         | **Volume Gateway**                    |

**🔥 One-line memory:**
**File Gateway = on-prem files + SMB/NFS + local cache + S3.**
**DataSync = move data.**
**Direct Connect = network connection.**

I'll keep this format for the remaining questions so your final 65-question revision will be much easier.


24-August-2026

27-August-2026

28-August-2026
