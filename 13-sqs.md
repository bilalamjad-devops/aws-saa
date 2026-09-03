

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

3-September-2026
