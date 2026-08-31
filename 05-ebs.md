**EBS →** block storage → EC2

**EFS → shared POSIX filesystem →** Linux → multiple EC2

**FSx for Windows →** shared Windows filesystem

**S3 → object storage →** massive scalable storage



### Your option confusion: FSx vs EFS vs EBS

Use this mental map:

| AWS service         | Think of it as                  | Exam clue                             |
| ------------------- | ------------------------------- | ------------------------------------- |
| **EBS**             | Hard drive for EC2              | One EC2/block storage/high IOPS       |
| **EFS**             | Shared elastic file system      | Multiple Linux EC2s need shared files |
| **FSx for Lustre**  | Super-fast parallel file system | **ML/HPC/parallel processing**        |
| **FSx for Windows** | Windows file server             | **SMB/Windows/AD**                    |
| **S3**              | Object storage                  | Files/objects, massive scalability    |
| **S3 Glacier**      | Cheap archive                   | **Cold/rarely accessed data**         |



# 🧠 The SAA shortcut for this question

When you see:

### **Windows + shared files + Active Directory**

Think:

> 🟢 **FSx for Windows File Server**

When you see:

### **Linux + shared files + NFS**

Think:

> 🟢 **EFS**

When you see:

### **On-premises applications need AWS storage through a file gateway**

Think:

> 🟢 **Storage Gateway**

When you see:

### **Objects + massive scalability + cheap storage**

Think:

> 🟢 **S3**

---

<img width="1449" height="1001" alt="aws-storage-services" src="https://github.com/user-attachments/assets/d2fbdb47-504d-4bfc-9ee7-de84dc7877bc" />



# 12. The FSx family — your exam cheat sheet

This is the table I'd actually memorize:

| Service              | Think                       | Protocol / characteristic | Typical clue                   |
| -------------------- | --------------------------- | ------------------------- | ------------------------------ |
| **EFS**              | Linux shared files          | NFS                       | Linux + shared storage         |
| **FSx Windows**      | Windows file server         | SMB + AD                  | Windows + SMB + AD             |
| **FSx Lustre**       | High-performance parallel   | Lustre                    | ML + HPC + parallel processing |
| **FSx OpenZFS**      | OpenZFS file system         | NFS                       | OpenZFS/Linux workloads        |
| **FSx NetApp ONTAP** | Flexible enterprise storage | NFS + SMB + **iSCSI**     | Windows + block + iSCSI        |

### 🔥 The shortcuts

| If question says...              | Think...         |
| -------------------------------- | ---------------- |
| **Linux + shared storage**       | EFS              |
| **Windows + SMB + AD**           | FSx Windows      |
| **ML/HPC + parallel processing** | FSx Lustre       |
| **OpenZFS**                      | FSx OpenZFS      |
| **Block storage + iSCSI**        | FSx NetApp ONTAP |
| **Objects / photos / backups**   | S3               |

---

## 13. One important correction to keep in your notes

Don't memorize:

> "EFS is for Linux and FSx is for Windows."

That's **too simplistic and can hurt you in the exam.**

Instead memorize:

> **EFS = NFS/shared file storage, primarily Linux workloads.**

> **FSx for Windows = SMB/Windows/AD.**

> **FSx for Lustre = high-performance parallel workloads.**

> **FSx for NetApp ONTAP = flexible enterprise storage, including iSCSI block access.**

That's a much safer SAA mental model.

---


## 🔥 Memorize this EBS cheat sheet

| EBS fact                                   | Correct? |
| ------------------------------------------ | -------- |
| Persistent block storage                   | ✅        |
| Used with EC2                              | ✅        |
| Survives EC2 termination if configured     | ✅        |
| EBS + EC2 must be same AZ                  | ✅        |
| Automatically replicated within AZ         | ✅        |
| Automatically replicated to another Region | ❌        |
| Snapshot stored in S3                      | ✅        |
| Snapshot stored in RDS                     | ❌        |
| Can modify size/type/IOPS while running    | ✅        |
| Instance Store is persistent               | ❌        |

### One sentence for your exam:

> **EBS = persistent block storage for EC2, AZ-scoped, replicated within the AZ, snapshot-backed, and can be modified while in use.**

That's the main lesson from Q14.

31-August-2026

24-August-2026

27-August-2026

28-August-2026

31-August-2026
