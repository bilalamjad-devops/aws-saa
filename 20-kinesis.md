

# Kinesis is actually a FAMILY of services

This is extremely important for SAA.

There are several Kinesis services, and they solve different streaming problems.

The main ones you should know are:

| Kinesis service            | Think                                  |
| -------------------------- | -------------------------------------- |
| **Kinesis Data Streams**   | Collect real-time streaming data       |
| **Kinesis Data Firehose**  | Deliver streaming data to destinations |
| **Kinesis Video Streams**  | Stream video from cameras/devices      |
| **Kinesis Data Analytics** | Analyze streaming data in real time    |


# 🔥 Your Kinesis Cheat Sheet

This is the table I would memorize for SAA:

| If the question says...                          | Think...                   |
| ------------------------------------------------ | -------------------------- |
| Continuous real-time events/data                 | **Kinesis Data Streams**   |
| Website clickstream                              | **Kinesis Data Streams**   |
| IoT streaming data                               | **Kinesis Data Streams**   |
| Deliver streaming data to S3/Redshift/OpenSearch | **Kinesis Data Firehose**  |
| Live camera/video stream                         | **Kinesis Video Streams**  |
| Real-time analysis of streaming data             | **Kinesis Data Analytics** |
| Process individual jobs/messages                 | **SQS**                    |
| Move existing on-premises data to AWS            | **DataSync**               |



5-September-2026
