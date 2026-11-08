# 🚀 Autonomous Multi-Platform Social Media Content Generation & Publishing Engine

A production-grade, end-to-end AI automation pipeline built using **n8n**, **Supabase PostgreSQL**, and **LLMs (Groq / Gemini)**. This system autonomously extracts fresh website content, performs smart deduplication, generates compliant and engaging social media copy, and handles multi-page publishing via social Graph APIs.

---

## 🏗️ Architecture & Workflow Overview

The pipeline operates as a continuous, event-driven cycle designed for zero-touch social media management:

1. **Smart Content Extraction:** Safely fetches fresh articles, blogs, or product pages via XML/RSS feeds while respecting site rate limits and `robots.txt`.
2. **URL Deduplication Engine:** Interfaces with **Supabase PostgreSQL** to log every execution, ensuring the exact same URL is never posted twice.
3. **AI Copywriting & Adaptation:** Utilizes advanced LLMs (Groq / Gemini Flash) to dynamically craft high-converting hooks, value summaries, CTAs, and optimized hashtags under strict character constraints.
4. **2-Stage Compliance Guardrails:** Combines system-prompt constraints with custom code sanitization filters to eliminate hallucinations, price discrepancies, or false claims before publishing.
5. **Multi-Mode Publishing & Alerting:** Routes payloads via Graph APIs with options for automated publishing or a human-in-the-loop review queue, backed by instant Telegram/Email error alerts.

---

## 🛠️ Tech Stack & Tools

* **Workflow Orchestration:** `n8n` (Self-hosted or Cloud)
* **Database & State Management:** `Supabase PostgreSQL`
* **AI / LLM Providers:** `Groq API (Llama 3)` / `Google Gemini API`
* **APIs & Integrations:** `Facebook Graph API`, `RSS/XML Parsers`, `Telegram / Gmail Webhooks`

---

## 📂 Repository Structure

```text
autonomous-social-content-pipeline/
│
├── workflows/
│   └── main_content_pipeline.json    # Exported n8n workflow JSON
├── assets/
│   ├── architecture_diagram.png      # System architecture overview
│   └── workflow_canvas.png           # n8n production canvas screenshot
├── .env.example                      # Environment variables template
└── README.md                         # Project documentation
```

---

## ⚙️ Setup & Installation Guide

To deploy and run this workflow locally or on your server, follow these steps:

### 1. Clone the Repository
```bash
git clone [https://github.com/Nazuuu-Ali/autonomous-social-content-pipeline.git](https://github.com/Nazuuu-Ali/autonomous-social-content-pipeline.git)
cd autonomous-social-content-pipeline
```

### 2. Configure Supabase Database
Run the following SQL snippet in your Supabase SQL Editor to create the required execution/deduplication log table:
```sql
create table content_execution_logs (
  id serial primary key,
  url text unique not null,
  title text,
  status text,
  created_at timestamp with time zone default timezone('utc'::text, now()) not null
);
```

### 3. Environment Variables (`.env`)
Create a `.env` file in your n8n environment or project root and configure the following secrets:
```env
FB_PAGE_ID=your_facebook_page_id_here
FACEBOOK_ACCESS_TOKEN=your_secure_page_access_token_here
SUPABASE_URL=your_supabase_project_url_here
SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_role_key_here
GROQ_API_KEY=your_groq_api_key_here
```

### 4. Import n8n Workflow
1. Open your n8n dashboard.
2. Click on **Add Workflow** -> **Import from File**.
3. Select `workflows/main_content_pipeline.json` from this repository.
4. Map your Supabase and LLM credentials, ensure the environment variables are linked, and activate the workflow!

---

## 🛡️ Security & Best Practices

* **Zero Hardcoded Secrets:** All sensitive credentials (tokens, page IDs, database keys) are externalized using n8n environment variables (`$env`) and secure credential managers.
* **Rate-Limit Compliance:** Built-in delays and error handlers prevent API throttling and ensure robust 24/7 uptime.

---

## 👤 Author

**Nazakat Ali**
* **AI Developer & Automation Specialist**
* GitHub: [@Nazuuu-Ali](https://github.com/Nazuuu-Ali)
* LinkedIn: [nazakat-ali-ai](https://www.linkedin.com/in/nazakat-ali-ai)
