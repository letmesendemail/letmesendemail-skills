---
name: lmse-marketing
description: Use when managing LetMeSend.Email marketing — contacts (list, create, update) and campaigns, i.e. bulk email broadcasts (create, send, schedule, cancel). Always use this skill when the user mentions newsletters, announcements, broadcasts, subscribers, or contact lists on LMSE. Campaign language matters: LMSE calls them `campaigns`, never broadcasts.
license: MIT
metadata:
    author: LetMeSend.Email
    version: "1.0.0"
    homepage: https://letmesend.email
inputs:
    - name: LETMESENDEMAIL_API_KEY
      description: API key for the account owning the contacts/campaigns.
      required: true
references:
    - contacts.md
    - campaigns.md
---

# LMSE Marketing

## Contacts — MCP

```
contacts-list{} → contacts-get{id} → contacts-create{...} → contacts-update{id, ...}
```

Verify risky addresses with `email-verification-check` (see `lmse` skill) before importing a list — bounces hurt domain reputation (see `lmse-domains`).

## Campaigns — MCP

```
campaigns-create{...} → campaigns-get{id} → campaigns-schedule{id, ...} → campaigns-send{campaign_id}
campaigns-cancel{id}   → stops a scheduled campaign
```

**Key gotchas:**
- LMSE calls them **campaigns**, not broadcasts — use `campaigns-*` tools.
- `campaigns-send` takes **only** `{campaign_id}` — the content and audience come from the created campaign. There is no inline send.
- Sending is gated on verification status — check `campaigns-get` before assuming a send went out.
- Never loop transactional `emails-send` for bulk mail — campaigns handle batching, unsubscribes, and reputation correctly.

## Flow

1. Build/select audience (`contacts-*`)
2. `campaigns-create` with content + audience
3. Review via `campaigns-get`
4. `campaigns-schedule` for later, or `campaigns-send{campaign_id}` now
5. Track delivery via campaign status and domain health (`lmse-domains`)
