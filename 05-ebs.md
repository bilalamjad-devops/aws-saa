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

24-August-2026

27-August-2026
