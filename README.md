# AI Email Automation Workflow with n8n


This workflow automatically processes incoming emails using **Gmail**, classifies them using an **AI agent (Groq)**, and handles **customer support queries** intelligently. Emails not related to support are ignored or logged, allowing you to focus only on actionable messages.

---
<img src="https://github.com/razzaq-99/customersupport_email_automation/blob/master/email_automation_pinecone.png" alt="n8n Workflow Screenshot">


<img src="https://github.com/razzaq-99/customersupport_email_automation/blob/master/customersupport_email_automation.png" alt="n8n Workflow Screenshot">

---
## 📌 Features

- 📥 **Triggers on New Gmail Emails**
- 💡 **Uses AI to classify if the email is a customer support request**
- 🤖 **Answers customer queries using Groq + Pinecone + Embeddings**
- 🧠 **Builds replies using pre-defined customer support policy and context**
- 📭 **Creates response drafts in Gmail**
- 🚫 **Ignores or logs non-support-related emails**

---

## 🔧 Workflow Structure

### 1. **Gmail Trigger**
- Listens for new emails using Gmail.
- Passes data to the content parser.

### 2. **Content (Manual Node)**
- Prepares or formats the email content for processing.
- Could include `subject`, `from`, `body`, etc.

### 3. **Customer Support (Groq Chat Model)**
- A custom AI node that classifies whether the message is a customer support issue.
- The output is passed into the `Switch` node.

### 4. **Switch**
- Determines whether the message is:
  - `True` → Proceed to support
  - `False` → End silently or log (via NoOp)

### 5. **Customer Support Agent (Groq + Tools)**
- Handles AI generation of customer support responses using:
  - `Groq Chat Model`
  - `Vector Store` (Pinecone)
  - `Embeddings from Mistral Cloud`
- Queries internal docs or FAQs for accurate answers.

### 6. **Gmail Draft Creation**
- Creates a professional and context-aware **email draft** using the AI-generated content.

### 7. **No Operation Node**
- Used when the email is **not** support-related.
- Placeholder to end the path cleanly.

---

## 📄 Customer Support Policies & FAQs

This workflow references a company’s support policies for accurate AI response generation. Some highlights include:

### Support Channels
- Email: `support@[yourcompany].com`
- Live Chat: Mon–Fri, 9 AM–6 PM
- Ticket System: `yourcompany.com/support`

### Response Time
| Priority | Description                 | Response Time    |
|----------|-----------------------------|------------------|
| High     | Outages, critical errors    | Within 2 hours   |
| Medium   | Feature issues, bugs        | Within 6 hours   |
| Low      | Questions, feedback         | Within 24 hours  |

> Full FAQ available in [customersupport.docx](./customersupport.docx)

---

## 📷 Included Visual

You can refer to the architecture above in the embedded workflow screenshot to better understand how each node connects and functions together.

---

## 🚀 Setup Instructions

1. Clone or build the workflow inside n8n
2. Connect Gmail and Groq credentials
3. Add your Pinecone vector index & embeddings provider
4. Upload support policy documents if using vector store
5. Activate the workflow and you're good to go!

---

## 📬 Optional Enhancements

- Add **Telegram or WhatsApp notification nodes** for manual review
- Store non-support emails in **Notion, Google Sheets, or Airtable**
- Replace `NoOp` with logging or notification systems

---

## 👨‍💻 Created By

**Abdul Razzaq**  
For automation and AI-powered customer communication

---

## 📎 Files

- `customersupport.docx` – Full customer support policies


