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

24-August-2026
