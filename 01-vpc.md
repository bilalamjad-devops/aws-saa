


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

No — **S3 Gateway Endpoint is NOT a different type.** 👍

It's just a more specific name.

Think of it like this:

```text
VPC Endpoint
     │
     └── Gateway Endpoint
             │
             ├── S3
             └── DynamoDB
```

So:

* **Gateway Endpoint** = the type
* **S3 Gateway Endpoint** = Gateway Endpoint used for **S3**
* **DynamoDB Gateway Endpoint** = Gateway Endpoint used for **DynamoDB**

### Example

If you create an endpoint for S3:

> **S3 Gateway Endpoint**

If you create one for DynamoDB:

> **DynamoDB Gateway Endpoint**

Both are **Gateway Endpoints**.

### 🧠 Shortcut

| You see                   | Think                              |
| ------------------------- | ---------------------------------- |
| VPC Endpoint              | General/private connection concept |
| Gateway Endpoint          | **S3 + DynamoDB**                  |
| S3 Gateway Endpoint       | **Gateway → S3**                   |
| DynamoDB Gateway Endpoint | **Gateway → DynamoDB**             |
| Interface Endpoint        | ENI/private IP → many AWS services |

So your statement:

> **VPC Gateway = S3 + DynamoDB**

✅ **100% correct.**

And:

> **S3 Gateway Endpoint = the S3-specific Gateway Endpoint**

Also correct.



# 4. What is an Interface VPC Endpoint?

This is the second major concept.

Normally, imagine your resource is inside a private subnet:

```text
Private VPC
    ↓
Internet/NAT
    ↓
Amazon Rekognition
```

But the question says:

> **Don't use the public Internet.**

So we create:

**Interface VPC Endpoint**

```text
Private VPC
     │
     │ private connection
     ↓
Interface VPC Endpoint
     │
     ↓
Amazon Rekognition
```

The endpoint gives your VPC a **private entry point** to the AWS service.

No Internet Gateway is required.

---

# 5. Why is it called "Interface"?

Because AWS creates an **ENI (Elastic Network Interface)** inside your subnet.

Conceptually:

```text
Your Private Subnet

┌──────────────────────────────┐
│                              │
│ EC2 / Lambda                 │
│      │                       │
│      ↓                       │
│ Interface Endpoint (ENI)    │
│      │                       │
└──────┼───────────────────────┘
       │
       ↓
Amazon Rekognition
```

The endpoint has a **private IP address**.

---

# 6. Gateway Endpoint vs Interface Endpoint

This connects directly to what you learned earlier.

### Gateway Endpoint

Used for:

> **S3 + DynamoDB**

```text
VPC
 ↓
Gateway Endpoint
 ↓
S3 / DynamoDB
```

### Interface Endpoint

Used for many other AWS services, such as Rekognition.

```text
VPC
 ↓
Interface Endpoint
 ↓
Rekognition
```

### 🧠 Exam shortcut

| Endpoint               | Main idea                                    |
| ---------------------- | -------------------------------------------- |
| **Gateway Endpoint**   | S3 + DynamoDB                                |
| **Interface Endpoint** | Many AWS services using private connectivity |

So when you see:

> **"Access Rekognition privately from a VPC"**

Think:

**Interface VPC Endpoint.** ✅

---



<img width="1322" height="845" alt="Amazon_VPC_IPv6" src="https://github.com/user-attachments/assets/579fa910-380e-405c-84ac-560e1a8d6c1e" />


**It means, we can't create ipv4-free vpc. but we can create ipv4-free subnet.**


Direct SAA-C03 Takeaway

- IPv4 CIDR Exhaustion in Subnet + Future Scalability Needed: $\rightarrow$ Create an IPv6-only Subnet.
- VPC IPv4 Disable/Removal: $\rightarrow$ Not Allowed / Invalid Action in AWS.

### 🔥 Shortcut

> **Site-to-Site VPN → Customer Gateway needs a static public IP.**

### 🎯 What is being tested?

**VPC subnet basics**

### ✅ Correct answers

**1. Each newly created subnet is, by default, linked to the main route table of the VPC.**

**2. Each subnet maps to a single Availability Zone.**

### 🔑 Key concepts

* **Main route table** → new subnets automatically use it unless you explicitly associate another route table.
* **Subnet = one AZ** → A subnet cannot span multiple AZs.

### ❌ Others

* **Private subnet + Elastic IP** → EIP doesn't make a private subnet Internet-connected. It needs a **NAT Gateway** for outbound Internet access.
* **Subnet spans 2 AZs** → ❌ One subnet = one AZ.
* **/16 to /27** → ❌ The VPC CIDR range is `/16` to `/28` (IPv4); `/28` is the smallest allowed VPC subnet size.

### 🔥 Exam shortcut

**Subnet = single AZ**
**New subnet → main route table by default**

---
---
---

### 🎯 What is being tested?

**VPC peering is non-transitive.**

### ✅ Correct answer

**Create a new VPC peering connection between PROD and DEV with the appropriate routes.**

### 🔑 Key concept

Current:

**DEV ↔ UAT ↔ PROD**

❌ DEV **cannot** communicate with PROD through UAT because **VPC peering does not support transitive routing**.

You need:

**DEV ↔ PROD** ✅

Then add the appropriate routes to both VPC route tables.

### ❌ Others

* **Do nothing** → VPC peering is not transitive.
* **Add PROD to DEV route table using UAT peering** → doesn't make peering transitive.
* **Overlapping CIDRs** → VPC peering requires non-overlapping CIDRs.

### 🔥 Exam shortcut

**VPC Peering = non-transitive.**

`A ↔ B ↔ C` ❌ **A cannot reach C**

Need `A ↔ C` ✅


---
---
---
---


### 🔥 The easiest way to remember

**CloudHub = many ON-PREMISES sites via VPN**

**DX Gateway = ON-PREMISES ↔ AWS via Direct Connect**

**Transit Gateway = MANY AWS NETWORKS (VPCs) + VPN/DX → central hub**

And for your Q20:

> **Hundreds of VPCs + multiple accounts + 5 Regions + VPN + scalable networking**

Think immediately:

**TGW → one per Region → TGW peering between Regions.**

24-August-2026

27-August-2026

28-August-2026

31-August-2026

1-September-2026

5-September-2026

10-September-2026

14-September-2026

16-September-2026

19-September-2026
