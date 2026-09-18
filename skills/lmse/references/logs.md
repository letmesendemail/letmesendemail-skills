# Logs

Inspect what was sent and what happened to it:

- SDK/API: `client.emails.list(...)` / `GET /emails` — filterable send history (MCP: `emails-list`, `emails-get` for one record).
- Campaign delivery: see the `lmse-marketing` skill.
- Domain-level deliverability trends: see the `lmse-domains` skill (`domain-health-history`).

When debugging "did my email go out?", check in this order: send response (id + status) → email record (`emails-get`) → domain health (suppression/bounce signals) → webhook log for the terminal event (`delivered`/`bounced`/`failed`).
