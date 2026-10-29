### 1. Sawal Kya Keh Raha Hai? (Question Breakdown) ❓

* **Scenario:** Ek airline company customer support requests (flight booking, updating details, check-in) ko handle karne ke liye **self-service automated solution** banana chahti hai bina human agent ke.
* **Requirements:**
1. Solution **text-based conversational chatbot** hona chahiye.
2. AI user ke **intentions (intents)** ko analyze kare, answers de, aur predefined actions fulfill kare.
3. Backend par actions perform karne ke liye **AWS Lambda** integration chahiye.



---

### 2. Sahi Jawab Kya Keh Raha Hai? (Correct Answer) 💡

* **Option:** *Deploy a conversational chatbot using Amazon Lex. Define conversation flow for specific user intentions. Integrate AWS Lambda functions as code hooks to perform actions based on user requests.*
* **Wazahat:**
* **Amazon Lex:** AWS ki conversational AI service hai jo Natural Language Understanding (NLU) aur Automatic Speech Recognition (ASR) use karti hai conversational interfaces (chatbots/voicebots) banane ke liye. Yeh intents, slots, aur utterances parse kar ke AWS Lambda ko trigger karti hai taake flight booking ya check-in jaise actions perform kiye ja sakein.



*Kyunki baqi options ghalat services use kar rahe hain:*

* *Amazon Polly:* Text-to-speech service hai (text ko awaz mein badalti hai), chatbot/NLU intent recognition nahi karti.
* *Amazon Rekognition:* Computer vision service hai (images aur videos analyze karti hai), text chatbots ke liye nahi.
* *Amazon Comprehend:* NLP service hai jo text analytics (sentiment analysis, entity recognition) ke liye use hoti hai, full conversational chatbot flow build karne ke liye nahi.

---

### 3. Keyword Scanning Cheat Sheet 🔑

| Question Keyword / Phrase | Direct Exam Mapping | Logic / Wajah |
| --- | --- | --- |
| **"Conversational chatbot" + "Analyze intentions / Intents" + "Text-based chat box"** | **Amazon Lex** | Chatbots aur conversational interfaces banane ke liye dedicated AWS service Amazon Lex hai. |
| **"Text-to-speech" / "Spoken responses"** | **Amazon Polly** | Amazon Polly likhe huye text ko audio/speech mein convert karti hai. |
| **"Sentiment analysis" / "Keyphrase extraction"** | **Amazon Comprehend** | Comprehend text analytics ke liye hai, dialog flow control ke liye nahi. |
| **"Image / Video analysis"** | **Amazon Rekognition** | Rekognition visual data/photos analyze karti hai. |

---

29-October-2026
