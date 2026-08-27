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

24-August-2026

27-August-2026
