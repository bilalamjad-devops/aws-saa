

There are 2 types of SQS:

**Standard Queue (Default):**

- Throughput: Unlimited messages per second.

- Ordering: Best-effort ordering (messages kabhi-kabhi out of order a sakte hain).

- Delivery: At-least-once delivery (ek message kabhi 2 baar deliver ho sakta hai, is liye app ko duplicate-safe hona chahiye).

**FIFO Queue (First-In-First-Out):**

- Throughput: High throughput (up to 300 msg/sec or 3,000 with batching).

- Ordering: Strict First-In-First-Out order guaranteed.

- Delivery: Exactly-once processing (no duplicates).


**SQS Key Uses:**

- Asynchronous background tasks (e.g., Image processing, Email sending).

- Traffic spikes ko handle karna (Load Leveling).

- Decoupling hybrid systems (On-Premises server message put karta hai, AWS EC2 consumer process karta hai).




### Decoupled Architecture Kya Hota Hai?

**Tightly Coupled (Purana Tarika):** App A direct App B ko request bhejti hai. Agar App B slow hai ya crash ho gayi, toh App A bhi ruk jati hai ya crash ho jati hai.

**Decoupled (AWS Best Practice):** App A aur App B ke beech mein ek Message Buffer / Queue (jaise SQS) rakh diya jata hai.

- App A message queue mein daal kar aage nikal jati hai.

- App B jab free hoti hai, queue se message utha kar process kar leti hai.

- Is se dono components independently kaam karte hain.









Yes. These are **two different SQS concepts**, and the names can be confusing.

### 1. Priority queue

A **priority queue** means:

> Some messages should be processed before other messages.

For example:

```text
Premium → HIGH priority
Free    → LOW priority
```

In the question you just solved, SQS doesn't provide a simple per-message priority setting, so we create:

```text
Premium Queue → process first
Free Queue    → process if premium is empty
```

**Exam clue:**

> Premium / urgent / VIP / high-priority requests → think **separate queues + priority processing**

---

### 2. Customer order queue

If by **"customer order queue"** you mean a queue used to process **customer orders**, that's simply an SQS use case.

Example:

```text
Customer places order
       ↓
   SQS Queue
       ↓
EC2 / Lambda worker
       ↓
Process order
```

SQS stores the order message while the worker processes it.

For example:

```text
Order #101
Order #102
Order #103
```

The queue helps ensure the application doesn't lose orders if the processing system is temporarily busy.

### Don't confuse these

| Concept                  | Meaning                                                |
| ------------------------ | ------------------------------------------------------ |
| **Priority queue**       | Process some messages before others                    |
| **Customer order queue** | SQS queue containing customer-order messages           |
| **SQS**                  | Message queue used to decouple producers and consumers |

### 🔥 SAA exam shortcut

If the question says:

> **"VIP customers must be served before normal customers"**

Think:

**Separate SQS queues → VIP queue first → normal queue second.**

If it says:

> **"Customer orders must not be lost while workers process them"**

Think:

**SQS → decouple order submission from order processing.**

**Yes, for a very simple mental model, you can think of SWF as somewhat similar to Terraform's `depends_on` — but don't treat them as the same thing.**

### Your analogy

Terraform:

```text
A
│
└── depends_on → B
                 │
                 ▼
                C
```

Meaning:

> **First A must happen, then B, then C.**

SWF:

```text
Step 1
   ↓
Step 2
   ↓
Step 3
   ↓
Step 4
```

Meaning:

> **Coordinate a multi-step workflow and keep track of what has happened.**

### But the important difference

| Terraform `depends_on`                     | SWF                                        |
| ------------------------------------------ | ------------------------------------------ |
| Controls **infrastructure creation order** | Controls **application/business workflow** |
| "Create A before B"                        | "Do payment before shipping"               |
| Infrastructure as Code                     | Workflow orchestration                     |
| Usually seconds/minutes                    | Can coordinate long-running workflows      |
| Doesn't manage business tasks              | Tracks tasks and workflow state            |

### 🎯 For your SAA exam

When you see:

> **"This must happen → then this → then this, across multiple distributed components"**

Think:

**SWF / Step Functions → workflow orchestration**

When you see:

> **"Application A needs to send work to Application B without depending on B being immediately available"**

Think:

**SQS → decoupling/message queue**

So your shortcut is:

> **`depends_on` = infrastructure order**
> **SWF = application workflow order**
> **SQS = application message waiting line**



29-August-2026


### 3. Don't confuse messaging services

| Service           | Think                               |
| ----------------- | ----------------------------------- |
| **SQS**           | Queue / buffer / decouple workloads |
| **Amazon MQ**     | Managed traditional message broker  |
| **Data Firehose** | Streaming data delivery             |
| **AppStream 2.0** | Stream desktop applications         |

---
---
---

**Aap ne 100% Sahi Samjha Hai!**

In dono patterns ko bilkul asan alfaaz mein divide karte hain:

---

### **1. SNS Fanout Pattern (Sub ko Bhejo)**

* **Requirement:** Ek hi message **sab subscribers / SQS queues** ke paas jana chahiye.
* **How it works:** Publisher 1 message SNS Topic mein daalta hai. SNS us message ki **exact copies** sari subscribed SQS queues mein push kar deta hai.
* **Example:** Ek nayi Order Placement hui. Is order ka message **Inventory Queue**, **Billing Queue**, aur **Shipping Queue** — teeno ko chahiye.

---

### **2. SNS Filter Policies (Sahi Wale Ko Bhejo)**

* **Requirement:** Message sirf usspecific subscriber ke paas jaye jo us ke matlab ka ho (e.g., Mouse message $\rightarrow$ Mouse Queue, Keyboard message $\rightarrow$ Keyboard Queue).
* **How it works:** Single SNS Topic par message bhejte waqt ek attribute add kar diya jata hai (e.g., `item_type: "mouse"`). Subscriptions par **Filter Policy** lagi hoti hai. SNS check karta hai aur message **sirf matching SQS Queue** mein bhejta hai.
* **Example:** Electronics store par jab product order ho, toh *Mouse* wala order sirf **Mouse Fulfillment Queue** mein jaye, *Keyboard* wala sirf **Keyboard Queue** mein.

---

### **Exam Cheat Sheet (Quick Recall)**

| Scenario | Architectural Pattern |
| --- | --- |
| **Broadcast to EVERY subscriber** | **SNS Fanout** (No Filter Policy) |
| **Route to SPECIFIC subscriber based on attributes** | **SNS Fanout + Subscription Filter Policies** |

**SQS Message Retention Period** woh time duration hai jitni der tak Amazon SQS kisi message ko queue mein **sambhal kar (store karke)** rakhta hai, agar application (consumer) usay read karke process na kar sakay.

Simple lafzon mein: Yeh message ki **"Expiry Date"** ya **"Life Span"** hai.

---

### **Key Rules (Exam Cheat Sheet):**

1. **Default Retention Period:** **4 Days** (Agar aap change na karein, toh message 4 din tak queue mein pada rahega).
2. **Minimum Retention:** **60 Seconds (1 Minute)**.
3. **Maximum Retention:** **14 Days**.

---

### **Yeh Kaise Kaam Karta Hai?**

1. Application (Publisher) SQS Queue mein message daalti hai.
2. SQS retention timer start kar deta hai.
3. Agar aap ka Consumer app kisi waja se **down / crash** ho gaya hai, toh message delete nahi hoga — woh SQS mein safe rahega.
4. Jaise hi Consumer application wapis online aayegi, woh queue se message read kar ke process kar legi.
5. **If Retention Limit Expires:** Agar 4 din (ya jo limit aap ne set ki ho, e.g. 14 days) guzar jayein aur consumer message process na kare, toh SQS us message ko **automatically delete** kar deta hai.

---

### **Real-Life Analogy (Mailbox):**

Sochein aap ke ghar ke bahar ek **Letter Box (SQS)** hai. Postman us mein letter daal kar chala jata hai.

* Agar aap 4 din tak ghar se bahar hain (Consumer Down), letter box mein letter safe pada rahega.
* Jab aap 4th day wapis aayenge, aap letter nikal lenge.
* Agar 14 days tak koi letter na nikale, toh box manager automatically purane letters ko clear/throw kar deta hai.

---

### **Question 59 Se Connection:**

Question 59 mein shart thi: **"The entire message processing should not exceed 24 hours."**
SQS ki default retention (4 days) 24 hours se zyada hai, is liye SQS is requirement ko naturally fulfill karta hai bina kisi extra configuration ke!

3-September-2026

11-September-2026

12-September-2026
