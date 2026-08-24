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




# 2. What is API Gateway throttling?

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

# 3. Now let's understand Question 31

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

# 4. Why is it called Canary?

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


24-August-2026
