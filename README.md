# 📬 Intelligent Gmail Automation Agent (n8n + Ollama)

An autonomous email triage and workflow automation pipeline built with **n8n** and powered by local **Ollama LLMs**. 

▶️ [Watch Workflow Demonstration Video](./Gmail_Automation.mp4)

This system monitors your Gmail inbox, classifies incoming messages into contextual categories, applies labels, extracts structured information, and routes them to dedicated AI sub-agents to draft tailored replies, log data into Google Sheets, or auto-archive unwanted noise.

---

## 🚀 Overview & Workflow

```
[ Gmail Trigger ] 
       │
       ▼
[ Ollama Text Classifier ]
       │
       ├──► 🏷️ Promotions     ──► Label & Mark as Read
       ├──► 💬 Social         ──► Label ──► AI Analysis ──► Append to Google Sheets
       ├──► 👤 Personal       ──► Label ──► AI Agent (Ollama) ──► Create Draft Reply
       ├──► 💼 Sales          ──► Label ──► AI Agent (Ollama) ──► Create Draft Reply
       ├──► 🎯 Recruitment    ──► Label ──► AI Agent (Ollama) ──► Create Draft Reply
       ├──► 🧾 Receipts       ──► Label ──► Send Auto-Ack / Archive
       └──► 📁 Miscellaneous  ──► Label & Mark as Read
```

---

## ✨ Features

- **Local LLM Privacy:** Uses **Ollama** locally for zero data leakage when classifying and generating drafts.
- **Dynamic Semantic Classification:** Automatically routes emails into 7 distinct branches based on intent:
  - `Promotions`
  - `Social`
  - `Personal`
  - `Sales`
  - `Recruitment`
  - `Receipts`
  - `Miscellaneous`
- **Context-Aware AI Responders:** Dedicated AI agents equipped with **Structured Output Parsers** generate context-specific draft replies without auto-sending (keeping human-in-the-loop control).
- **Google Sheets Integration:** Automatically parses data from relevant leads or notices and logs rows directly into spreadsheets.
- **Inbox Zero Automation:** Labels and marks routine promotional or low-priority emails as read.

---

## 🛠️ Tech Stack & Integrations

- **Orchestration:** [n8n](https://n8n.io/) (Self-hosted or Cloud)
- **Language Models:** [Ollama](https://ollama.com/) (e.g., Llama 3, Mistral, Gemma)
- **Services & Tools:**
  - Gmail API (Triggers, Labeling, Drafting, Sending)
  - Google Sheets API (Data logging)
  - n8n Advanced AI / LangChain Nodes (Text Classifier, AI Agent, Structured Output Parser)

---

## 📋 Prerequisites

Before running the workflow, make sure you have:

1. **n8n** installed and running (v1.x+ recommended):
   ```bash
   npx n8n
   # or via Docker
   docker run -it --rm --name n8n -p 5678:5678 -v ~/.n8n:/home/node/.n8n n8nio/n8n
   ```
2. **Ollama** installed and serving models locally:
   ```bash
   ollama serve
   ollama pull llama3:8b
   ```
3. **Google Cloud Console Credentials:**
   - OAuth2 Client configured with access to Gmail and Google Sheets APIs.

---

## ⚙️ Installation & Configuration

### 1. Import Workflow
1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/gmail-ai-automation.git
   cd gmail-ai-automation
   ```
2. In your n8n interface, open the **Workflows** dashboard.
3. Click **Import from File** and select `workflow.json`.

### 2. Configure Credentials

Set up the following credentials in your n8n workspace:
- **Gmail OAuth2 API:** Connect your target Gmail account.
- **Google Sheets OAuth2 API:** Connect your Google account.
- **Ollama API:** 
  - Base URL: `http://localhost:11434` (or `http://host.docker.internal:11434` if running n8n in Docker).

### 3. Setup Models & Prompts
- Ensure each **Ollama Chat Model** sub-node references an installed model (e.g., `llama3`, `mistral`, or `qwen2.5`).
- Customize the system prompt in the **Text Classifier** node to adjust category detection criteria to fit your inbox.

---

## 🗂️ Category Handling Logic

| Category | Action Pipeline | Goal |
|---|---|---|
| **Promotions** | Add label `Promotions` ➔ Mark as Read | Declutter inbox |
| **Social / Notifications** | Add label `Social` ➔ Extract Key Details ➔ Append to Sheet | Track interactions |
| **Personal** | Add label `Personal` ➔ AI Agent ➔ Generate Draft | Fast human-reviewed reply |
| **Sales** | Add label `Sales` ➔ AI Agent ➔ Generate Draft | Evaluate pitch / schedule meeting |
| **Recruitment** | Add label `Recruitment` ➔ AI Agent ➔ Generate Draft | Candidate screening & outreach |
| **Receipts** | Add label `Receipts` ➔ Process & Record | Expense tracking |
| **Miscellaneous** | Add label `Misc` ➔ Mark as Read | General catch-all |

---

## 🔒 Safety & Privacy

- **Human-in-the-Loop:** High-impact responses (Sales, Personal, Recruitment) create **drafts** in Gmail rather than sending immediately, ensuring you review every email before delivery.
- **Local Inference:** Running Ollama ensures private email contents are processed on-premise without exposing sensitive client communication to third-party proprietary APIs.

---

## 🤝 Contributing

Contributions, feedback, and pull requests are welcome!
1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.
