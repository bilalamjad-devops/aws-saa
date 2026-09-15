### 🎯 What is being tested?

**AI services for speech → translation → sentiment analysis**

### ✅ Correct answer

**Convert audio to text using Amazon Transcribe → translate Hindi to English using Amazon Translate → analyze sentiment using Amazon Comprehend.**

### 🔑 Simple flow

```text
Audio
  ↓
Amazon Transcribe
  ↓
Text
  ↓
Amazon Translate
  ↓
English
  ↓
Amazon Comprehend
  ↓
Sentiment: Positive / Negative
```

### Why these services?

* **Transcribe** → Speech/audio → text
* **Translate** → Hindi → English (and supports additional languages)
* **Comprehend** → NLP, including **sentiment analysis**
* No need to build/manage your own ML model.

### 🔥 Exam shortcut

**Audio → Transcribe**
**Language translation → Translate**
**Sentiment/NLP → Comprehend**


### 😊 Sentiment Analysis Report

A **sentiment analysis report** tells you the **emotion/opinion expressed in text**.

For example, a customer says:

> “The support agent was very helpful and solved my problem quickly.”

**Amazon Comprehend** analyzes this and might report:

* **Sentiment:** Positive
* Positive: 95%
* Neutral: 4%
* Negative: 1%

Another customer says:

> “I waited 2 hours and nobody helped me.”

→ **Sentiment: Negative**

### 🔑 Exam shortcut

**Sentiment = customer feeling/opinion**

* 🎤 Audio → **Transcribe**
* 🌍 Language translation → **Translate**
* 😊😡 Customer sentiment/emotion from text → **Comprehend**


15-September-2026

--

## 5. Exam Decision Matrix (AWS AI Services Cheat Sheet)

* **Speech to Text (Audio $\rightarrow$ Text):** $\rightarrow$ **Amazon Transcribe**
* **Text to Speech (Text $\rightarrow$ Audio):** $\rightarrow$ **Amazon Polly**
* **Language Translation (Text $\rightarrow$ Text):** $\rightarrow$ **Amazon Translate**
* **Text Analytics & Sentiment Analysis:** $\rightarrow$ **Amazon Comprehend**
* **Conversational Chatbot Interfaces:** $\rightarrow$ **Amazon Lex**

---
