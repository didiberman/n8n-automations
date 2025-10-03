# 🌀 n8n Automations by Didi

This repository contains a collection of **custom automation workflows** I’ve built for myself and for clients.  
They combine **n8n**, **Airtable**, **AI APIs** (Claude, OpenAI, DeepL), and **Azure services** to solve real-world business problems in marketing, content, and operations.

---

## 📌 Overview

These workflows are designed to:
- Save time by automating repetitive tasks  
- Connect APIs and services that don’t talk to each other out of the box  
- Bring AI (Claude, OpenAI, DeepL, etc.) into business processes  
- Leverage **Azure cloud automation** for scalability and enterprise integrations  
- Provide reliable, production-ready flows with error handling and logging  

I use them both in my **personal productivity stack** and in **client projects** where automation creates direct business value.

---

## ⚡ Workflows Included

Each workflow lives in its own JSON export (ready to import into n8n) or cloud pipeline configuration.  
Highlights:

### 🔄 AI Translation Workflow (n8n + Airtable + Claude + DeepL)
- Input: Airtable form (Source text, target language, tone, style)  
- Processing: Claude + DeepL translations → Claude comparison → Final result  
- Output: Writes back to Airtable with all versions, status updates, and error handling  

### 📩 Automated Lead Capture & Enrichment
- Scrape or receive leads → enrich with LinkedIn / Clearbit → push to CRM (Zoho, Airtable, HubSpot)  

### 📊 Content Repurposing Pipelines
- Convert YouTube videos into Medium drafts or blog posts using LLMs  
- Summarize transcripts and generate multiple content formats automatically  

### 🤖 Telegram & Voice Agents
- Chatbots for lead generation, structured Q&A, or internal knowledge base queries  

### 📑 Document Processing (Azure + n8n)
- Integrates **Azure Form Recognizer** and **Azure Cognitive Services** for document parsing and classification  
- Uses n8n for orchestration and routing results into Airtable / Google Sheets  

### ☁️ Azure Automations
- Built custom pipelines with:  
  - **Azure Logic Apps** for enterprise workflow automation  
  - **Azure Functions** for serverless tasks (data cleaning, API integration)  
  - **Azure Cognitive Services** for OCR, translation, and sentiment analysis  
- Integrated Azure pipelines with n8n workflows for hybrid automation setups  

---

## 🛠 Tech Stack

- [n8n](https://n8n.io/) as the workflow engine  
- Airtable (databases, forms, interfaces)  
- Claude / OpenAI / DeepL (LLM & translation APIs)  
- **Microsoft Azure**: Logic Apps, Functions, Cognitive Services, Form Recognizer  
- Google Cloud APIs (Docs, Sheets, Console integrations)  
- CRM integrations (Zoho, HubSpot, etc.)  

---

## ✅ Features

- **Error handling**: failed API calls update Airtable with error details instead of breaking the flow  
- **Extensibility**: modular design, easily adaptable to other APIs and cloud providers  
- **Hybrid cloud**: workflows that mix **n8n** flexibility with **Azure’s enterprise reliability**  
- **Transparency**: intermediate outputs logged (Claude vs DeepL vs Final) for debugging and quality control  

---

## 🚀 Getting Started

1. Clone this repo  
2. Import any workflow JSON into your n8n instance (or deploy the Azure pipelines)  
3. Update credentials:  
   - Airtable API tokens  
   - API keys for Claude / OpenAI / DeepL  
   - Azure credentials (service principals / keys for Logic Apps, Functions, Cognitive Services)  
   - CRM / SaaS integrations  
4. Run and test with sample data  

---

## 👤 Author

Built by **Didi Berman** – DevOps / AI Automation Engineer.  
I design workflows that combine **AI, APIs, and automation** across **n8n** and **Azure** to solve real business problems.  

- 💡 Portfolio (https://didiberman.com)

---

⚡ Always experimenting with new integrations.  
This repo will grow as I add more of my personal and client automations.
