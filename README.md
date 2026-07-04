# n8n Email Support Bot

> Automatically reads incoming support emails, classifies them with AI, drafts a reply, and routes the ticket to the right team — all without human triage.

## 🎯 Use Case
Support teams get flooded with emails across billing, technical issues, refunds, and general questions. Manually reading and routing each one wastes hours. This workflow monitors a Gmail inbox, uses AI to classify each email by type and urgency, creates a ticket in Notion, drafts a personalized reply for agent review, and routes it to the correct team Slack channel — in seconds.

## 🔄 Workflow Overview
1. **Trigger:** Gmail node polls the support inbox every 5 minutes for new unread emails.
2. **Classify:** AI node reads the email subject + body and returns a category (billing, technical, refund, general) and urgency (high/medium/low).
3. **Create Ticket:** A new page is created in a Notion database with all email details and AI classification.
4. **Route:** Based on category, an alert is sent to the correct Slack channel (e.g. #billing-team, #tech-support).
5. **Draft Reply:** A second AI call drafts a professional reply email and saves it as a Gmail draft for agent review before sending.

## 🛠️ Nodes Used
- Gmail Trigger (Poll inbox)
- OpenAI / Claude (Classification + Reply drafting)
- Switch (Category routing)
- Notion (Ticket creation)
- Slack (Team routing alerts)
- Gmail (Draft reply creation)

## ⚙️ Setup
1. Import `workflow.json` into your n8n instance (Workflows → Import from File).
2. Copy `.env.example` to `.env` and fill in your credentials.
3. Connect Gmail, Notion, Slack, and OpenAI inside n8n's credential manager.
4. Update the Notion database ID in the workflow to match your own database.
5. Update the Slack channel IDs to match your workspace.
6. Activate the workflow.

## 📋 Requirements
- n8n v1.0+
- Gmail account with API access (Google Cloud Console)
- OpenAI or Anthropic API key
- Notion account + integration token
- Slack workspace with bot token

## 📂 Project Structure
```
n8n-email-support-bot/
├── README.md
├── workflow.json
├── .env.example
├── docs/
│   └── architecture.md
└── example-payloads/
    └── email-input.json
```

## 🚀 Future Improvements
- Add sentiment analysis to flag angry customers for immediate human escalation
- Connect to Zendesk or Freshdesk instead of Notion for teams already using a helpdesk
- Auto-send replies for simple FAQs without agent review
