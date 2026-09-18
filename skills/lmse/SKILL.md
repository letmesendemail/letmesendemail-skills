---
name: lmse
description: Use when working with the LetMeSend.Email API — sending transactional emails (single), verifying email addresses, managing API keys, receiving delivery webhooks, or setting up an SDK. Always use this skill when the user mentions LetMeSend.Email, LMSE, or letmesend.email — it contains critical gotchas (SDK error shape, idempotency keys, `from_`/`type_` naming in Python) that prevent common production issues.
license: MIT
metadata:
    author: LetMeSend.Email
    version: "1.0.0"
    homepage: https://letmesend.email
inputs:
    - name: LETMESENDEMAIL_API_KEY
      description: LetMeSend.Email API key. Create one in the dashboard (user menu → API keys) and copy the full value shown once at creation.
      required: true
references:
    - installation.md
    - sending.md
    - verification.md
    - webhooks.md
    - api-keys.md
    - logs.md
---

# LetMeSend.Email

## Quick Send — Node.js

```typescript
import { LetMeSendEmail } from "@letmesendemail/letmesendemail-node";

const client = new LetMeSendEmail(process.env.LETMESENDEMAIL_API_KEY!);

const email = await client.emails.send({
  from: "Acme <hello@acme.com>",
  to: ["person@example.com"],
  subject: "Hello from letmesend.email",
  html: "<p>Hello from letmesend.email</p>",
  type: "transactional",
  idempotencyKey: `welcome-email/${userId}`,
});

console.log("Sent:", email.id, email.status);
```

**Key gotchas:** the Node SDK **throws** on API errors (unlike some email SDKs that return `{ data, error }`) — wrap sends in try/catch. Always pass `idempotencyKey` on sends so retries never double-send.

## Quick Send — Python

```python
import os
from letmesendemail import LetMeSendEmail, LetMeSendEmailError

with LetMeSendEmail(api_key=os.environ["LETMESENDEMAIL_API_KEY"]) as client:
    email = client.emails.send(
        from_="Acme <hello@acme.com>",  # trailing underscore: `from` is reserved
        to=["person@example.com"],
        subject="Hello from letmesend.email",
        html="<p>Hello from letmesend.email</p>",
        type_="transactional",           # trailing underscore: `type` is reserved
    )
print(f"Sent! ID: {email.id}, Status: {email.status}")
```

**Key gotchas:** Python uses `from_` and `type_` (trailing underscores — `from`/`type` are reserved words). Errors raise `LetMeSendEmailError`. The client is a context manager — use `with` so connections close cleanly.

## Quick Send — MCP tool

When acting directly as an agent with the LetMeSendEmail MCP server connected, call `emails-send` (no SDK needed). See the `lmse-mcp` skill for connection setup. Transactional sends count against the account quota; mailbox sends do not.

## When to use the other LMSE skills

- Mailbox work (read/search/triage/draft/reply from an inbox) → `lmse-mailbox`
- Contacts and bulk campaigns → `lmse-marketing`
- Domain DNS and deliverability → `lmse-domains`
- MCP connection, abilities, errors, pagination → `lmse-mcp`
