- `Create an Amazon Pinpoint journey for the multi-engagement SMS marketing campaign and an Amazon Kinesis Data Stream for analysis. Configure Amazon Pinpoint to send events to the Kinesis data stream for collection, processing, and analysis. Set the retention period of the Kinesis data stream to 365 days.`


<img width="1174" height="937" alt="amazon-pinpoint-journey-console-aws" src="https://github.com/user-attachments/assets/a269da21-444e-4768-afc0-2598c2504c6d" />


Is question ka correct answer: **Create an Amazon Pinpoint journey for the multi-engagement SMS marketing campaign and an Amazon Kinesis Data Stream for analysis. Configure Amazon Pinpoint to send events to the Kinesis data stream for collection, processing, and analysis. Set the retention period of the Kinesis data stream to 365 days.**

Aap ne sahi pehchana! Exam mein aksar marketing/SMS campaigns ke liye **Amazon Pinpoint** hi correct answer hota hai.

---

### Scenario Breakdown & Key Requirements

1. **2-Way SMS / Marketing Campaign:** Mobile app users ko multi-engagement SMS bhejna aur **subscribers ke replies receive karna**.
2. **Near-Real-Time Analysis:** SMS responses ko real-time / near-real-time mein collect aur analyze karna.
3. **1 Year Retention:** Data ko 365 days ke liye preserve rakhna.
4. **Least Operational Overhead:** Minimum custom development aur maintenance.

---

### Correct Option Explanation

#### ✅ **Amazon Pinpoint + Amazon Kinesis Data Stream**

* **Amazon Pinpoint:** AWS ki dedicated service hai jo **two-way SMS campaigns, mobile app push notifications, aur email marketing journeys** ke liye design ki gayi hai. Yeh built-in customer engagement handle karti hai bina custom coding ke.
* **Kinesis Data Streams:** Pinpoint easily Kinesis Data Stream ke sath integrate ho jata hai taake SMS event data (deliveries, replies, customer responses) ko near-real-time mein stream kar sake.
* **365 Days Retention:** Kinesis Data Stream data retention up to 365 days support karta hai, jo exactly 1 year retention ki requirement poori karta hai.

---

### Incorrect Options Breakdown (Elimination)

* ❌ **SQS + Step Functions + Lambda + S3 Glacier:** SQS SMS send nahi kar sakta (yeh message queueing service hai, delivery channel nahi). Is architecture mein boht zyaada custom coding/overhead hai.
* ❌ **Amazon SNS + Kinesis (Default Settings):** SNS 1-way mass SMS notifications bhej sakta hai, par complex **multi-engagement audience journeys / targeted campaigns** ke liye Amazon Pinpoint behtar hai. Iske alawa, Kinesis Data Stream ki **default retention period sirf 24 hours (1 day)** hoti hai, 365 days nahi.
* ❌ **Amazon Connect:** Connect ek cloud **call center / customer service contact center** solution hai, automated targeted marketing SMS campaigns ke liye nahi.

---

### SAA-C03 Exam Rule

> **Marketing & Customer Engagement Rule:**
> * **Amazon SNS:** Simple, transactional notifications (e.g., OTPs, system alerts, 1-way broadcast SMS).
> * **Amazon Pinpoint:** Targeted marketing campaigns, multi-channel customer journeys, **two-way SMS**, and user analytics.
> 
> 

---

27-September-2026
