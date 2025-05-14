> Sarah is an intelligent voice agent that automates the collection of structured data, schedules appointments, and evaluates call effectiveness. It helps companies streamline customer interactions, gather valuable data, and optimize communication processes. With its capabilities, it improves data accuracy, enhances customer engagement, and reduces operational costs by turning conversations into actionable insights.

Sarah is a multi-model agent that uses Eleven Labs for text-to-speech, Deepgram for speech-to-text, and OpenAI GPT-4.1 for data processing and interaction analysis. It can be customized to adapt to various industries, such as construction, real estate, and technical services.

Sarah retrieves context from custom data prompts and utilizes predefined templates to capture structured information such as client details, project specifications, and scheduling data. It provides multilingual support and can operate in both English and Spanish to ensure optimal coverage.

## Technical Integration

### Environment Setup
Sarah is run entirely on [[Vapi]], and all API calls are done through their APIs
### 🧾 Agent Functions

### 1. **Structured Data Extraction**

A prompt is designed to capture the following client data (these can be adjusted to the company's requirements):

- Full name
- Phone number
- Email address
- Project type (e.g., construction, renovation)
- Project definition level (initial idea, with plans)
- Project urgency
- Budget range
- Was a technical visit scheduled?
- Date and time of the technical visit
- Additional important notes
    
> If any data is not provided, it is marked as "Not provided".

---
### 2. **Call Success Evaluation**
The outcome is automatically classified using one of these labels, in the language of the conversation:
- **Spanish:**
    - Cita agendada (Appointment scheduled)
    - Sin respuesta (No answer)
    - Seguimiento agendado (Follow-up scheduled)
    - Ocupado (Busy)
    - No interesado (Not interested)
- **English:**
    - Appointment scheduled
    - No answer
    - Follow-up scheduled
    - Busy
    - Not interested
---
### 3. **Intelligent Summary**
The model generates a summary of a maximum of **12 words** based on the interaction. If there was no useful content, it is reported as `did not answer`.

---
## 🧩 Business Customization
Each company can customize:
1. **Agent voice tone (female, male, formal, youthful, etc.)**
2. **Data extraction prompt according to its industry.**
3. **Keywords to be detected or specific responses for each case.**
4. **Initial and closing phrases.**
5. **Availability hours and subsequent contact channels.**
---
## 📊 Analytics and Insights
All the collected information can be sent to a customized dashboard where the following can be visualized:
- Number of appointments scheduled per day/week.
- Conversion rates (call → appointment).
- Average call duration.
- Structured data by client or by campaign.
- Percentage of calls by category (busy, no answer, etc.).