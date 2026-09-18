# Email verification

Check whether an address is deliverable before sending (SDK: `client.emails.verify(email)`, MCP: `email-verification-check`). Verification is informational — it never blocks sending.

Use it to:
- Validate signup forms before creating contacts
- Scrub a list before a campaign to protect sender reputation

Do not gate transactional sends on verification in user-facing flows — a false negative blocks a legitimate user, while sending to a bad address just bounces.
