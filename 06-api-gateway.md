## 1. What is API Gateway?

Think of **API Gateway as the front door of your backend application**.

For example, imagine you have:

```text
Internet Users
      ↓
API Gateway
      ↓
    Lambda
      ↓
   DynamoDB
```

A user might call:

```text
GET /users/123
POST /orders
GET /products
```

API Gateway receives those HTTP requests and sends them to the appropriate backend, such as **Lambda, EC2, ECS, or other AWS services**.

So:

> **API Gateway = manages/receives API requests and sends them to your backend.**

It is NOT your application itself.




## 2. What is API Gateway throttling?

Now imagine your API normally receives:

```text
100 requests/second
```

Suddenly a product becomes viral:

```text
100
500
1,000
10,000
50,000 requests/second 😱
```

Your backend may not be able to handle all of that.

So you can tell API Gateway:

> "Allow only 1,000 requests per second."

That's **throttling**.

```text
Users
 ↓
API Gateway
 ↓
🚦 Throttling
 ↓
Backend
```

If 5,000 requests arrive but your configured limit is 1,000, API Gateway limits the traffic. Excess requests can receive **HTTP 429 (Too Many Requests)**.

### Very important distinction

**API Gateway** = the service.

**API Gateway throttling** = a feature/configuration inside API Gateway that controls how many requests are allowed through.

Think:

> **API Gateway = security guard at the door**
> **Throttling = security guard saying "only 100 people per minute can enter."**

---

3. Now let's understand Question 31

The company already has:

```text
Customers
    ↓
Route 53
    ↓
Custom Domain
    ↓
API Gateway
    ↓
Backend
```

They have an **old API**:

```text
API v1
```

Now developers created:

```text
API v2
```

Maybe v2 has:

* better performance
* new features
* bug fixes

But they **don't want to suddenly send everybody to v2**.

Why?

Because what if v2 has a bug?

Instead:

```text
              ┌── API v1 (90%)
Users → API GW│
              └── API v2 (10%)
```

This is called a **canary deployment**.

---

## 3. Why is it called Canary?

Imagine miners going into a dangerous mine.

Historically, a **canary** was used as an early warning.

If the canary was okay → continue.

If something went wrong → get out.

Same idea here.

Send a **small percentage of customers to the new API** first.

For example:

```text
100% traffic

        ↓

API Gateway

   ┌─────────────┐
   ↓             ↓
 API v1        API v2
  90%            10%
```

Monitor v2:

```text
Errors?
Latency?
Performance?
Customer problems?
```

If everything looks good:

```text
90% → 70% → 50% → 20% → 0%
10% → 30% → 50% → 80% → 100%
```

Eventually:

```text
100% → API v2
```

If v2 is broken:

```text
API v2
  ↓
❌ Problems

Send traffic back to v1
```

That's why **canary deployment** minimizes customer disruption.


# 🧠 Make this table your exam memory

| If question says...                        | Think                 |
| ------------------------------------------ | --------------------- |
| **API / REST API**                         | 🚪 API Gateway        |
| **WebSocket API**                          | 🚪 API Gateway        |
| **API throttling/auth/versioning**         | 🚪 API Gateway        |
| **Pay per API call**                       | 🚪 API Gateway        |
| **Static Anycast IP**                      | 🌍 Global Accelerator |
| **Fixed IP entry point across Regions**    | 🌍 Global Accelerator |
| **GraphQL**                                | GraphQL               |
| **High-performance EC2-to-EC2 networking** | ⚡ EFA                 |

### Q17 answer:

✅ **API Gateway supports RESTful + WebSocket APIs**

✅ **Pay based on API calls/data transferred**

---
---
---

<img width="804" height="778" alt="ddb_as_set_read_1" src="https://github.com/user-attachments/assets/d3e1473b-a0ea-4301-9d93-33cf43fcc4c2" />


Aap ka concept **DAX** ke hawale se bilkul clear ho gaya hai! Ab aayein samajhte hain ke **API Gateway Caching** aur **DAX Caching** mein kya farq hai aur dono alag-alag level par kaise kaam karti hain.

---

### Architecture Mein Caching Kahan Hoti Hai?

Sochein aap ki application ek multi-layer architecture hai:

```
[ Mobile Game / User ]
         │
         ▼
 ┌─────────────────┐
 │   API Gateway   │  ◄── 1. API Gateway Cache (Restricts hits to Lambda)
 └────────┬────────┘
          │
          ▼
 ┌─────────────────┐
 │ AWS Lambda      │
 └────────┬────────┘
          │
          ▼
 ┌─────────────────┐
 │  DynamoDB (DAX) │  ◄── 2. DAX Cache (Restricts hits to DynamoDB Disk)
 └─────────────────┘

```

---

### 1. API Gateway Caching (Frontend / API Layer Cache)

**API Gateway Caching** poori **HTTP API response** ko cache karti hai.

* **Kaise kaam karti hai?** Jab mobile game API Gateway ko koi request bhejta hai (e.g., `GET /leaderboard`), toh API Gateway response ko apne paas save kar leta hai.
* **Fayda:** Agli baar jab koi user same request bhejega, toh API Gateway **Lambda function ko execute kiye bina** aur **DynamoDB ko touch kiye bina** direct response return kar dega.
* **Main Benefit:**
* **Cost Reduction:** Lambda function ke run execution charges bach jate hain.
* **Response Speed:** Round-trip time bohot kam ho jata hai.



---

### 2. DynamoDB Accelerator - DAX (Database Layer Cache)

**DAX** sirf aur sirf **DynamoDB database queries/reads** ko cache karta hai.

* **Kaise kaam karti hai?** Jab Lambda function DynamoDB se data mangta hai (e.g., `GetItem` ya `Query`), toh request pehle DAX mein jati hai. Agar data DAX mein hai, toh mil jata hai; agar nahi hai, toh DAX DynamoDB se la kar save karta hai.
* **Fayda:** Lambda function chalega aur code execute hoga, lekin DynamoDB database disk par load nahi padega.
* **Main Benefit:**
* **Microsecond Latency:** Query response time milliseconds se drop ho kar **microseconds** ho jata hai.
* **Database RCU Saving:** DynamoDB ki Read Capacity Units (RCU) consume nahi hoti.



---

### Comparison Table (Quick Summary)

| Feature | **API Gateway Caching** | **DynamoDB Accelerator (DAX)** |
| --- | --- | --- |
| **Kya Cache Hota Hai?** | Poora HTTP API Response. | Specific Database Items / Queries. |
| **Kahan Hota Hai?** | System ke Frontend (API) level par. | System ke Database level par. |
| **Lambda Run Hota Hai?** | ❌ Nahi (Lambda execution bypass ho jata hai). | ✅ Haan (Lambda run hota hai, par DB saved rehta hai). |
| **Main Objective** | Traffic ko Lambda tak pohenchne se rokna. | DB Reads ko **microseconds** speed dena. |

---

### Exam Rule of Thumb:

* Agar question bole: *"Cache API responses to reduce Lambda execution costs"* $\rightarrow$ **API Gateway Caching**
* Agar question bole: *"In-memory cache for DynamoDB to get microsecond read latency"* $\rightarrow$ **DynamoDB Accelerator (DAX)**

---
---
---

Bilkul tension mat lein! Yeh AWS ka ek fundamental concept hai jo pehli baar thoda confusing lagta hai. Aayein isay step-by-step aur real-life example se samajhte hain.

---

### 1. AWS Regions Kya Hain? (Simple Example)

AWS ne poori dunya mein apne **Data Centers** khole hue hain. Un data centers ki locations ko AWS **Regions** kehta hai aur unhe naam deta hai:

* **`us-east-1`** = N. Virginia, USA mein majood data center.
* **`us-east-2`** = Ohio, USA mein majood data center.
* **`ap-south-1`** = Mumbai, India mein majood data center.

Jab aap AWS par koi bhi service (jaise EC2 instance, Database, ya API Gateway) banate hain, toh aap pehle select karte hain ke aap isay **kis region (data center)** mein chalana chahte hain.

---

### 2. AWS Certificate Manager (ACM) aur SSL Certificate

Aap ne dekha hoga jab aap kisi bank ya secure website par jaate hain, toh browser ke URL ke sath ek **Green Lock Icon (🔒)** aur `https://` aata hai. Yeh lock **SSL/TLS Certificate** ki wajah se aata hai.

AWS mein SSL Certificate **ACM (AWS Certificate Manager)** service ke zariye **mufat (free)** banta hai.

---

### 3. Region Ka Rule (Yeh Confusion Kyun Hui?)

AWS mein bohot si services **Region-Specific** hoti hain. Iska matlab hai agar aap ne ek cheez **Ohio (`us-east-2`)** mein banayi hai, toh us se judi doosri cheezein bhi **Ohio (`us-east-2`)** mein hi honi chahiye.

#### **Rule:**

* Agar aap ki **API Gateway (API)** Ohio (`us-east-2`) ke data center mein chal rahi hai...
* Toh us API ke liye jo **SSL Certificate (🔒)** banega, woh bhi aap ko **Ohio (`us-east-2`)** region mein ja kar hi create karna padega.

Agar aap SSL Certificate N. Virginia (`us-east-1`) mein bana lenge, toh Ohio wali API us certificate ko **use nahi kar payegi** kyunki dono ka region alag hoga.

---

### 4. Summary (Pura Workflow Ek Nazar Mein)

```
[ Step 1 ]
Aap ne Ohio (us-east-2) mein API Gateway banaya.

[ Step 2 ]
Aap ne Ohio (us-east-2) ke ACM mein ja kar "api.tutorialsdojo.com" ka SSL Certificate banaya.

[ Step 3 ]
Dono ko apas mein connect kiya taake website par HTTPS (🔒) chal sake.

```

Bas itni si baat thi! Aayein ab aage chalte hain jab aap ready hon.

24-August-2026

31-August-2026

16-September-2026

22-September-2026
