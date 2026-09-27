**AWS Global Accelerator** ek **standalone AWS service** hai (yeh kisi doosri service ka feature nahi hai).

Is ka main kaam aap ki application ki **speed, performance, aur availability ko global scale par improve karna** hota hai.

---

### Iska Simple Concept (Yeh Kaise Kaam Karta Hai?)

1. **2 Static Anycast IP Addresses:**
Jab aap Global Accelerator banate hain, toh AWS aap ko **2 unique, static IP addresses** deta hai.
2. **AWS Global Network:**
Normal internet traffic multiple public routers se ho kar slow travel karti hai. Global Accelerator users ke traffic ko unke kareeb tareen **AWS Edge Location** par enter karwa deta hai. Us ke baad poora traffic AWS ke apne super-fast private fiber-optic network par travel karta hai.
3. **Instant Health Check Failover:**
Agar aap ka application server (e.g., Application Load Balancer ya EC2) ek AWS Region mein down ho jaye, toh Global Accelerator **10 seconds ke andar** traffic ko doosre healthy Region mein route kar deta hai.

---

### Main Use Cases for Exam (SAA-C03)

* **Multi-Region Failover:** Agar aap ki app 2 alag AWS Regions mein chal rahi hai aur aap instantaneous failover chahte hain.
* **Low Latency for Gaming/IoT/HTTP:** Non-HTTP (TCP/UDP) ya HTTP traffic ke latency ko worldwide kam karne ke liye.
* **Static IP Requirement:** Jab client-side firewall par aap ko fix IPs whitelist karvani hoon jo kabhi change na hoon.

---

### AWS Global Accelerator vs Route 53 (Exam Difference)

| Feature | AWS Global Accelerator | Route 53 |
| --- | --- | --- |
| **Kaam Kaise Karta Hai?** | **Network level (IP/Anycast)** par traffic route karta hai. | **DNS level (Domain Name)** par resolution karta hai. |
| **Failover Speed** | Boht fast (**< 10 seconds**) | Thoda slow (DNS Caching / TTL par depend karta hai, ~60-300s). |
| **Protocol Support** | TCP aur UDP dono | Pure DNS resolution |


27-September-2026
