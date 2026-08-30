
### 6. One very important exam concept

Remember this distinction:

| Service                     | Think                                                     |
| --------------------------- | --------------------------------------------------------- |
| **CloudFront**              | CDN / cache content near users                            |
| **Lambda@Edge**             | Run custom code at CloudFront edge                        |
| **User-Agent header**       | Information about the requesting browser/device           |
| **Response Headers Policy** | Add/remove/modify HTTP response headers                   |
| **Route 53**                | DNS routing                                               |
| **CloudFront Functions**    | Lightweight, very fast edge request/response manipulation |

For **this question**, the key clue is:

> **"based on User-Agent" + "custom logic" + "CloudFront"**

→ **Lambda@Edge**

### 🧠 Shortcut

| If question says...                                      | Think...                    |
| -------------------------------------------------------- | --------------------------- |
| SQL injection / XSS                                      | **WAF**                     |
| Too many requests from an IP                             | **WAF Rate-based rule**     |
| Run code at CloudFront edge                              | **Lambda@Edge**             |
| Add HTTP response headers                                | **Response Headers Policy** |
| Choose content based on browser/device with custom logic | **Lambda@Edge**             |
| Cache content globally                                   | **CloudFront**              |

So yes, your understanding is basically right: **Lambda@Edge lets you execute custom code at CloudFront edge locations**, and here that code examines the **User-Agent** and helps decide which image version to return.

30-August-2026
