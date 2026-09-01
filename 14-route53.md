

### 🔥 Your exam shortcut

| If question says...                         | Pick             |
| ------------------------------------------- | ---------------- |
| **Bias / expand or shrink geographic area** | **Geoproximity** |
| **Country/continent/location-based rule**   | **Geolocation**  |
| **Lowest latency / best performance**       | **Latency**      |
| **Percentage / proportion / traffic split** | **Weighted**     |


Exactly. 👍 You already know the **basic Route 53 concept**, and now you're discovering that Route 53 does more than simple DNS resolution.

Think of it as **two layers**:

### 1. What you already know — DNS

You have:

```text
bilalamjad.pk
      ↓
   Route 53
      ↓
   2.2.2.2
```

Route 53 answers:

> "What IP/endpoint should this domain name point to?"

---

### 2. New Route 53 concepts you need to learn

These are **routing policies and health checking** that make Route 53 smarter about *which* endpoint to return.

| Concept                  | Simple meaning                            | Example                             |
| ------------------------ | ----------------------------------------- | ----------------------------------- |
| **Health Check**         | Is my application/endpoint healthy?       | "Is Primary ALB working?"           |
| **Failover Routing**     | Primary normally, DR if primary fails     | Primary → DR                        |
| **Weighted Routing**     | Divide traffic according to percentages   | 90% → A, 10% → B                    |
| **Latency Routing**      | Send user to lowest-latency Region        | Pakistan → Mumbai, US → Virginia    |
| **Geolocation Routing**  | Route based on user's location            | Pakistan → Pakistan endpoint        |
| **Geoproximity Routing** | Route based on geographic distance + bias | Move more traffic toward one Region |

So your current Route 53 learning should expand from:

> **"Route 53 converts domain name → IP."**

to:

> **"Route 53 decides which endpoint should answer DNS queries based on different routing policies."**

### The three you just encountered

**Health Check**

```text
Is Primary healthy?
      ↓
 YES / NO
```

**Failover**

```text
Primary ✅ → Primary
Primary ❌ → DR
```

**Weighted**

```text
90% → Server A
10% → Server B
```

And one very important distinction:

**Health Check is not a routing policy.**
It's something Route 53 can use **with routing policies** to make routing decisions.

For your SAA preparation, **yes — you should learn these Route 53 concepts properly now**, because you'll keep seeing them in questions.


30-August-2026

1-September-2026
