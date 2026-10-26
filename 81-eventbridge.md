<img width="1017" height="655" alt="td-example-eventbridge-rule-for-acm-01-08-25 (1)" src="https://github.com/user-attachments/assets/371b5162-8d39-45bd-b020-0c962c9b6377" />

<img width="1017" height="411" alt="td-daystoexpiry-metric-01-08-25 (1)" src="https://github.com/user-attachments/assets/5bfc6efb-cdff-44c5-baa6-eb39189de9f9" />


### 🎯 Key Takeaway:

1. **CloudWatch `DaysToExpiry` Metric:**
* **ACM (AWS Certificate Manager) khud** Amazon CloudWatch mein `DaysToExpiry` metric publish karta hai (din mein do baar) taake yeh pata chal sakay ke certificate expire hone mein kitne din baqi hain.


2. **ACM Events & EventBridge:**
* ACM apnay expiration events directly **Amazon EventBridge** (jisay pehle CloudWatch Events kehte thay) ko emit karta hai.



Isi wajah se, TutorialsDojo ke sawal mein yeh dono tareeqay theek maane gaye hain:

* **Tareeqa 1 (Metrics/Scheduled):** CloudWatch ki `DaysToExpiry` metric ya scheduled EventBridge rule ke zariye check karna.
* **Tareeqa 2 (Event-driven):** ACM ke apnay native expiration events ko EventBridge ke zariye pakar kar SNS par alert bhej dena.


26-October-2026
