
# 5. Your exam shortcut

Memorize this:

| Priority | ASG asks                                                            |
| -------- | ------------------------------------------------------------------- |
| **1️⃣**  | Which AZ has the most instances?                                    |
| **2️⃣**  | Within that AZ, which instance uses the **oldest launch template**? |
| **3️⃣**  | If tied, which is **closest to next billing hour**?                 |
| **4️⃣**  | If still tied → **random**                                          |

### 🔥 One-line shortcut

> **Scale-in → Most crowded AZ → Oldest Launch Template → Closest to billing hour → Random**

And don't memorize **"oldest EC2 instance."**

Memorize:

> **Oldest Launch Template first.**

## 5. Decision Matrix (Exam Cheat Sheet)

* **Default Auto Scaling Cooldown:** $\rightarrow$ **300 seconds (5 minutes)**.
* **Main Objective of Cooldown:** $\rightarrow$ Prevent launch/termination of extra instances before previous scaling takes effect.
* **What happens during Cooldown?** $\rightarrow$ ASG pauses simple scaling activities until the timer expires.

---

28-August-2026

5-September-2026
