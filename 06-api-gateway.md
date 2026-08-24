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


24-August-2026
