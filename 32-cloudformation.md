## 5. Exam Decision Matrix (CloudFormation Helper Scripts Cheat Sheet)

* **Pause stack creation until EC2 software setup finishes:** $\rightarrow$ **`CreationPolicy` + `cfn-signal**`
* **Download and install packages/files from CloudFormation metadata:** $\rightarrow$ **`cfn-init`**
* **Check for updates in metadata and apply them periodically:** $\rightarrow$ **`cfn-hup`**
* **Control resource creation order (Resource A before Resource B):** $\rightarrow$ **`DependsOn`**

14-September-2026
