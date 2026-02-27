# Agent Flow in 3_lab3.ipynb

Below is a Mermaid diagram explaining the agent orchestration and flow in the notebook:

---

```mermaid
graph TD
    User[User Message]
    Guardrail[Guardrail: Name Check]
    SalesManager[Sales Manager Agent]
    SalesAgent1[DeepSeek Sales Agent]
    SalesAgent2[Gemini Sales Agent]
    SalesAgent3[Llama3.3 Sales Agent]
    EmailManager[Email Manager Agent]
    SubjectWriter[Subject Writer Tool]
    HTMLConverter[HTML Converter Tool]
    SendEmail[Send HTML Email Tool]

    User --> Guardrail
    Guardrail -->|Pass| SalesManager
    Guardrail -->|Tripwire| SalesManager
    SalesManager --> SalesAgent1
    SalesManager --> SalesAgent2
    SalesManager --> SalesAgent3
    SalesAgent1 --> SalesManager
    SalesAgent2 --> SalesManager
    SalesAgent3 --> SalesManager
    SalesManager -->|Select Best Draft| EmailManager
    EmailManager --> SubjectWriter
    SubjectWriter --> EmailManager
    EmailManager --> HTMLConverter
    HTMLConverter --> EmailManager
    EmailManager --> SendEmail
    SendEmail --> EmailManager
```

---

**Flow Explanation:**

1. **User** sends a message (e.g., request to send a cold sales email).
2. **Guardrail** checks for personal names in the input (input guardrail).
3. If passed, the **Sales Manager Agent** orchestrates:
    - Uses three **Sales Agent tools** (DeepSeek, Gemini, Llama3.3) to generate drafts.
    - Evaluates drafts and selects the best one.
4. The winning draft is handed off to the **Email Manager Agent**.
    - Uses **Subject Writer** to generate a subject.
    - Uses **HTML Converter** to format the body.
    - Uses **Send HTML Email Tool** to send the email.

This flow ensures structured outputs, model diversity, and input guardrails for safe and effective email generation.
