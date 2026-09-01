

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


## 🧠 Exam shortcut

When you see:

**"only if primary fails"**

→ **Failover**

When you see:

**"90% / 10%"**

→ **Weighted**

When you see:

**"closest/lowest latency Region"**

→ **Latency**

When you see:

**"country/continent/location of user"**

→ **Geolocation**

When you see:

**"geographic distance + bias"**

→ **Geoproximity**

So for Question 25:

> **Primary normally, DR only during outage**

### ✅ Route 53 Failover Routing + Health Check

And importantly, **this is DNS-level failover**. Route 53 isn't moving your application or starting your DR environment; it's changing **which endpoint DNS answers point users toward**.


# 🧠 The key concept

You should now have these three Route 53 routing policies clearly separated:

### Failover

**"Primary or backup?"**

```text
Primary ✅ → Primary

Primary ❌ → Backup
```

### Weighted

**"How much traffic goes where?"**

```text
90% → A
10% → B
```

### Latency

**"Which endpoint gives the user the lowest latency?"**

```text
Pakistan user → Mumbai
US user       → Virginia
```

---

## One-line exam trick

When you see:

> **"If primary fails, automatically send users to backup/DR"**

Think:

### 🚨 Route 53 **Failover Routing**

When you see:

> **"90% traffic here, 10% there"**

Think:

### ⚖️ Route 53 **Weighted Routing**

When you see:

> **"Send users to the Region with lowest latency"**

Think:

### 🌎 Route 53 **Latency-based Routing**

And Question 27 is simply:

**Primary MEAN app → fails → Route 53 automatically sends users to cheap static S3/CloudFront backup.**


1-September-2026

30-August-2026

1-September-2026
