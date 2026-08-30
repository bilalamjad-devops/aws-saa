
### EKS

**EKS = Elastic Kubernetes Service**

AWS manages the Kubernetes control plane for you.

You still use Kubernetes concepts:

```text
Pod
Deployment
Service
Ingress
kubectl
YAML
Helm
```

And Kubernetes can also run outside AWS.

That's why:

> **Open-source + cloud-agnostic → EKS**

---

### ECS

**ECS = Elastic Container Service**

This is AWS's own container orchestration service.

For example:

```text
ECS
 ├── Cluster
 ├── Service
 └── Task
```

It's excellent if you're happy staying within AWS, but **ECS itself is not Kubernetes** and isn't designed to be portable to Azure/GCP/on-prem in the same way Kubernetes is.

---

# 3. Then what is Fargate?

This is where many beginners get confused.

**Fargate is NOT a container orchestrator.**

Fargate is a **serverless compute engine for containers**.

You can think:

```text
              Container orchestration
                ↓
          ┌───────────────┐
          │ ECS or EKS    │
          └───────┬───────┘
                  │
             Where to run?
                  ↓
          ┌───────────────┐
          │   Fargate     │
          └───────────────┘
```

For ECS:

```text
ECS
 ↓
Fargate
 ↓
Container
```

Instead of managing EC2 servers.

With ECS EC2:

```text
ECS
 ↓
EC2 instances
 ↓
Containers
```

With ECS Fargate:

```text
ECS
 ↓
Fargate
 ↓
Containers
```

**You don't manage the underlying EC2 servers with Fargate.**

---

# 4. What is App Runner?

**AWS App Runner** is for when you basically say:

> "I have a web application/container. Just run it for me."

You give App Runner your:

* source code, or
* container image

and AWS handles much of the infrastructure, deployment, scaling, load balancing, etc.

It's designed to be **simple**.

For example:

```text
Your Docker Image
       ↓
   App Runner
       ↓
   Running Web App
```

But App Runner is **not Kubernetes**.

So if the question says:

> "We need an open-source, cloud-agnostic container orchestration platform."

❌ App Runner

✅ EKS

---

# 5. One very important distinction

Don't memorize:

> Fargate = alternative to EKS/ECS

Instead remember:

### **ECS/EKS = orchestration**

They decide things like:

> Which container should run?
> How many should run?
> Where should they run?
> How should services communicate?

### **Fargate = compute**

It provides the infrastructure needed to actually run containers without you managing EC2 servers.

---

## 🧠 Exam shortcut

| Question clue                                | Think             |
| -------------------------------------------- | ----------------- |
| **Kubernetes**                               | **EKS**           |
| **Open-source container orchestration**      | **EKS**           |
| **Cloud-agnostic / portable containers**     | **EKS**           |
| **AWS proprietary container orchestration**  | **ECS**           |
| **Don't want to manage EC2 for containers**  | **Fargate**       |
| **Simple way to deploy a web app/container** | **App Runner**    |
| **ECS without managing servers**             | **ECS + Fargate** |
| **ECS with your own servers**                | **ECS + EC2**     |

### 🎯 For Question 9

The exam is basically shouting:

**"OPEN-SOURCE + CLOUD-AGNOSTIC + CONTAINER ORCHESTRATION"**

→ **Kubernetes**

→ **Amazon EKS** ✅

And one small correction to keep your mental model clean: **EKS itself is an AWS managed service, but Kubernetes—the orchestration platform it provides—is open-source and portable.**

30-August-2026
