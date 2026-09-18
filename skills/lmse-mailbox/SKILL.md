---
name: lmse-mailbox
description: Use when building any system where an AI agent works from a LetMeSend.Email mailbox - reading and searching messages, triaging (star/archive/move/delete), drafting, sending, replying and forwarding. Always use this skill when the user wants an agent inbox, support handler, or email-to-task pipeline on LMSE - it contains critical security patterns (sender allowlists, content filtering, sandboxed processing) that prevent untrusted email from controlling the agent.
license: MIT
metadata:
    author: LetMeSend.Email
    version: "1.0.0"
    homepage: https://letmesend.email
inputs:
    - name: LETMESENDEMAIL_API_KEY
      description: API key whose owner is assigned to the mailbox, with mailbox:read/write/send abilities as needed.
      required: true
references:
    - reading.md
    - triage.md
    - sending-from-mailbox.md
    - security.md
---

# LMSE Mailbox (agent inbox)

## Read - MCP

```
mailboxes-list{}                       → pick a mailbox id
mailbox-messages-list{mailbox_id, limit} → newest first, cursor-paginated
mailbox-messages-search{mailbox_id, query} → full-text search
mailbox-messages-get{mailbox_id, id}   → full body + headers
mailbox-messages-thread{mailbox_id, id} → whole conversation
```

## Triage - MCP (needs `mailbox:write`)

```
mailbox-messages-action{mailbox_id, ids[], action}  → star | unstar | archive | trash  (max 50 ids)
```

Archive instead of delete for anything that might be needed later; trash is recoverable (`restore`), delete is not.

## Send - MCP (needs `mailbox:send`)

```
mailbox-drafts-create{mailbox_id, to, subject, body}  → review, then send via your own approval step
mailbox-messages-send{mailbox_id, to, subject, body}
mailbox-messages-reply{mailbox_id, id, body}          → headers derived automatically
mailbox-messages-forward{mailbox_id, id, to}
```

**Key gotchas:** there is no `from` field - sends always go out as the mailbox's primary address. Drafts never send on their own. Every send needs an `idempotency_key`.

## Ability tiers (grant minimum)

- **Reader** (`mailbox:read`): list/get/search/thread - safe default for summarizers
- **Organizer** (+ `mailbox:write`): drafts, star/archive/move/delete/restore
- **Full assistant** (+ `mailbox:send`): everything above plus send/reply/forward

## Security is mandatory, not optional

Untrusted email content must never drive privileged actions directly - read `security.md` before building any autonomous flow.
