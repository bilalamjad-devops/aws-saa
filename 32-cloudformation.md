## 5. Exam Decision Matrix (CloudFormation Helper Scripts Cheat Sheet)

* **Pause stack creation until EC2 software setup finishes:** $\rightarrow$ **`CreationPolicy` + `cfn-signal**`
* **Download and install packages/files from CloudFormation metadata:** $\rightarrow$ **`cfn-init`**
* **Check for updates in metadata and apply them periodically:** $\rightarrow$ **`cfn-hup`**
* **Control resource creation order (Resource A before Resource B):** $\rightarrow$ **`DependsOn`**

---
---
---

Is question ka correct answer **The Resources section is missing.** hai.

---

### Scenario Breakdown & Key Requirements

1. **AWS CloudFormation Template Review:** Template review karne par pata chala ke yeh stack deployment ke waqt **fail** ho jaye gi.
2. **Template Code Analysis:** Provided JSON snippet mein `AWSTemplateFormatVersion`, `Parameters`, aur `Outputs` sections dikhai de rahe hain.
3. **Missing Section Identification:** Pata karna hai ke is template mein sab se major structural error kya hai jis waja se yeh template invalid hai.

---

### Correct Option Explanation

#### ✅ **The Resources Section is MANDATORY**

* **Only Mandatory Section:** AWS CloudFormation template mein boht se optional sections hotay hain (Parameters, Outputs, Mappings, Conditions, Description, AWSTemplateFormatVersion), LEKIN **`Resources` section wahid MANDATORY (fard/zaroori) section hai**.
* `Resources` section ke bina CloudFormation ko yeh pata hi nahi chalta ke kon sa AWS infrastructure (EC2, S3, VPC, RDS, etc.) deploy ya create karna hai.
* Isi waja se yeh template stack create karne ki koshish par immediately validation failure error de gi.

---

### Incorrect Options Breakdown (Elimination)

* ❌ **Option 1 (AWSTemplateFormatVersion is incorrect):** `2010-09-09` CloudFormation ka filhal sab se latest aur official format version string hai. Format version `2017-06-06` jaisa koi valid version exist nahi karta.
* ❌ **Option 3 (Conditions section is missing):** `Conditions` section completely optional hota hai, is ke missing hone se template fail nahi hoti.
* ❌ **Option 4 (Invalid Parameters section):** `Parameters` ek bilkul valid aur standard CloudFormation section hai jo user inputs ne ke liye use hota hai.

---

### SAA-C03 CloudFormation Template Structure Cheat Sheet 💡

> * **MANDATORY Section:** **`Resources`** (Must declare at least one resource).
> * **OPTIONAL Sections:** `AWSTemplateFormatVersion`, `Description`, `Parameters`, `Mappings`, `Conditions`, `Transform`, `Outputs`.
> * **Template Format Version:** Always `"2010-09-09"` (if specified).
> 
> 

---


14-September-2026

28-September-2026
