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

Here are the automations currently in this repository:

### 1. Airtable-Claude-DeepL Translation Agent
-   **File:** `Airtable-Claude-DeepL Translation Agent Workflow.json`
-   **Description:** This workflow automates the translation process for a large German ecommerce brand. It's triggered by a webhook with a source text, target language, and other parameters. It uses both DeepL and Claude for translation, and then a final LLM call to compare and produce a superior translation. The results are then saved to an Airtable base.

### 2. Instagram Lead Personalized Email Generator
-   **File:** `Instagram Lead Personalized Email Generator.json`
-   **Description:** This workflow was built for a world-leading Instagram marketer (150K+ followers) to generate personalized emails for new leads. It's triggered by a survey submission, scrapes the lead's Instagram profile using Apify, and then uses an LLM to generate a personalized email. The email is then sent, and a notification is sent to Telegram for quality control.

### 3. ZohoCRM LLM Lead Enrich Agent
-   **File:** `ZohoCRM LLM Lead Enrich Agent.json`
-   **Description:** This workflow enriches lead data in ZohoCRM for a UK-based Capital Venture firm. When a new lead is added, this workflow is triggered. It uses an LLM to find more information about the lead and their company, and then updates the lead's record in ZohoCRM with the new information. It includes a deduplication step to avoid enriching the same lead multiple times.

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