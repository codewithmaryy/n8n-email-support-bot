# Architecture

```
[Gmail Inbox - Support Email Arrives]
              │
              ▼
     [Gmail Trigger - Poll every 5 min]
              │
              ▼
   [AI Classification Node]
   (OpenAI / Claude)
   Returns: { category, urgency }
              │
              ▼
        [Switch Node]
   ┌─────────┼──────────┬──────────┐
billing   technical  refund    general
   │          │          │         │
   ▼          ▼          ▼         ▼
[Slack]   [Slack]   [Slack]   [Slack]
#billing  #tech     #refunds  #general
   └─────────┴──────────┴──────────┘
              │
              ▼
   [Notion - Create Ticket]
   (stores email + classification + urgency)
              │
              ▼
   [AI Reply Drafting Node]
   (writes professional response)
              │
              ▼
   [Gmail - Save as Draft]
   (agent reviews before sending)
```

## Data Flow Notes
- The Gmail trigger only picks up unread emails and marks them as read after processing.
- Classification response format: `{ "category": "billing|technical|refund|general", "urgency": "high|medium|low", "summary": "one sentence" }`
- The Notion ticket includes: sender, subject, body, category, urgency, timestamp, and a link back to the Gmail thread.
- Drafted replies are NOT auto-sent — they wait in the Gmail Drafts folder for human review.
