# n8n AI Lead Nurturing Workflow

> Automatically captures, qualifies, and routes inbound leads using AI — no manual triage required.

## 🎯 Use Case
Sales teams waste hours manually reading and scoring inbound form submissions. This workflow listens for new lead form submissions, uses an LLM to qualify and score the lead based on intent and fit, then automatically pushes qualified leads into the CRM and alerts the sales team in Slack in real time.

## 🔄 Workflow Overview
1. **Trigger:** Webhook receives a new lead submission (from a website form, landing page, or ad platform).
2. **Enrich:** An AI node (OpenAI/Claude) reads the lead's message and company info, then classifies intent and assigns a 1–10 quality score.
3. **Route:** 
   - If score ≥ 7 → create/update record in HubSpot CRM + send a Slack alert to the sales channel.
   - If score < 7 → tag as "nurture" and add to a follow-up email sequence.
4. **Log:** Every lead and its score is logged to a Google Sheet for reporting.

## 🛠️ Nodes Used
- Webhook (Trigger)
- OpenAI / Anthropic Claude (Lead Scoring)
- IF / Switch (Routing logic)
- HubSpot (CRM)
- Slack (Notifications)
- Google Sheets (Logging)

## ⚙️ Setup
1. Import `workflow.json` into your n8n instance (Workflows → Import from File).
2. Copy `.env.example` to `.env` and fill in your own API credentials.
3. Connect your HubSpot, Slack, OpenAI, and Google Sheets accounts inside n8n's credential manager.
4. Update the webhook URL in your lead capture form to point to this workflow's webhook endpoint.
5. Activate the workflow.

## 📋 Requirements
- n8n v1.0+
- OpenAI or Anthropic API key
- HubSpot account with API access
- Slack workspace with a bot token
- Google account with Sheets API enabled

## 📂 Project Structure
```
n8n-ai-lead-nurturing/
├── README.md
├── workflow.json
├── .env.example
├── docs/
│   └── architecture.md
└── example-payloads/
    └── lead-input.json
```

## 🚀 Future Improvements
- Add lead deduplication check before CRM insert
- A/B test scoring prompt against actual conversion data
- Add SMS notification channel via Twilio
