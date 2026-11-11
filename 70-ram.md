
Aaiye Question 3 ke **Keywords Scan** karke fast answer nikalte hain:

---

### Step 1: Keywords Scan 🔍

1. **Multi-Account Central Management:** `"multiple AWS accounts"`, `"centrally manages their AWS resources"`
* **Trigger:** Multiple accounts ko ek jagah consolidate aur manage karne ke liye **AWS Organizations** required hota hai.


2. **Resource Sharing Across Accounts:** `"share resources such as AWS Transit Gateways... across their various accounts"`
* **Trigger:** AWS resources ko cross-account share karne ke liye specific AWS service **AWS Resource Access Manager (AWS RAM)** hai.



---

### Step 2: Correct Answers (Select TWO)

1. **Consolidate all of the company's accounts using AWS Organizations.**
2. **Use the AWS Resource Access Manager (RAM) service to easily and securely share your resources with your AWS accounts.**

---

### Step 3: Fast Elimination Rules ❌

* **AWS IAM (Cross-account access):** Roles/Permissions share karne ke liye hota hai, infrastructure resources (Transit Gateways, Route 53 Resolver rules) share karne ke liye RAM use hota hai.
* **AWS Control Tower:** Governance, Landing Zones, aur Guardrails set karne ke liye hai, resource sharing engine nahi hai.
* **AWS ParallelCluster:** HPC (High Performance Computing) cluster management tool hai, account consolidation tool nahi hai.

---
---
---
---




4. Question

An enterprise company uses multiple AWS accounts for different business units. The AWS accounts are set up and consolidated into an organization via the AWS Organizations service.

The company sites are distributed globally across different countries and regions. There is a need to centrally manage security group rules across the organization to allow CIDR ranges of new office locations and remove old CIDR ranges as needed.

What design should the solutions architect propose to meet the requirements in the MOST cost-effective manner?


- Build an AWS-managed prefix list in Amazon VPC containing the CIDR blocks to allow or block. Enable Security Hub for the AWS accounts and define a policy that specifies the desired security group updates. Create a Lambda function to call the modify_managed_prefix_list API that can be triggered by Amazon EventBridge when updating the CIDR blocks.
- Leverage AWS Firewall Manager to create a common security group policy. Select the security groups previously created as the primary group in the policy.
- Enable Route 53 Application Recovery Controller (Route 53 ARC) in the AWS account. Create a Recovery Control Panel to define the routing control states and configurations of the CIDR ranges of each business unit or company site. Define routing control states within the RCP to indicate how traffic should be routed. Enable Zonal Shift functionality in Route 53 ARC to shift traffic from one set of resources to another with the defined CIDR ranges.
- `Provision a VPC customer-managed prefix list using the AWS CLI or the Amazon VPC console and add the CIDR blocks to be included in the list. Share the prefix list ID to other AWS accounts using the AWS RAM (Resource Access Manager) API, or the AWS RAM Console. Add the prefix list to the security groups used across the organization.`


<img width="619" height="375" alt="ManagedPrefixList (2)" src="https://github.com/user-attachments/assets/6aa1c32f-441a-4cc6-bedb-bf2f75c1d77b" />

<img width="611" height="401" alt="ResourceShares (2)" src="https://github.com/user-attachments/assets/76a4b0f7-5f6b-4079-a5fb-f6b83c3d214a" />


Koi baat nahi! Aaiye isay ek bohot hi aasan aur mazedaar misaal se samajhte hain:

---

### 🏢 Real-World Analogy (Company ki Central VIP List)

Maan lein aap ki ek bari company hai jiske poori dunya mein **50 alag-alag daftarein (AWS Accounts)** hain. Har daftar ke gate par ek guard (**Security Group**) baitha hai jo check karta hai ke kaun se naye log ya office locations (**CIDR Ranges**) andar aa sakti hain.

* **Masla (Problem):** Jab bhi koi naya daftar banta hai ya purana band hota hai, aapko 50 daftaron ke guards ke paas ja kar alag-alag list update karni parti hai. Isme waqt bhi lagta hai aur kharcha bhi hota hai.
* **Behtareen Hal (Prefix Lists + AWS RAM):**
1. Aap head office mein ek **Central Register (Customer-Managed Prefix List)** bana lete hain jismein saare allowed office addresses likhe hote hain.
2. Phir aap **AWS RAM (Free Delivery Service)** ke zariye yeh register apne baaqi saare 50 daftaron ko **bilkul muft (Cost-Effective)** bhej dete hain.
3. Ab jab bhi koi naya address aata hai, aap sirf head office ki central register mein ek line add karte hain, aur woh automatically sab daftaron mein update ho jati hai!



---

### ❌ Baaqi Options Itne Complex Kyun Hain?

* **Lambda / EventBridge / Security Hub (Option 1):** Yeh aisa hi hai jaise ek choti si list update karne ke liye aap ghar mein ek poora robot software engineer hire kar lein — ismein code likhna parta hai, extra services ka bill aata hai, aur yeh **cost-effective** nahi hai.
* **Route 53 ARC (Option 2):** Yeh traffic aur disaster recovery ke liye hota hai, iska security groups ya office IP addresses se koi taluq hi nahi hai!

---

05-October-2026

11-November-2026
