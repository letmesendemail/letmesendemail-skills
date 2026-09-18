---
name: lmse-domains
description: Use when managing sending domains on LetMeSend.Email — listing domains, verifying DNS (SPF/DKIM/DMARC), and checking deliverability health over time. Always use this skill when the user mentions domain setup, DNS records, verification status, spam-folder problems, or sender reputation on LMSE. No domain can send until it is verified.
license: MIT
metadata:
    author: LetMeSend.Email
    version: "1.0.0"
    homepage: https://letmesend.email
inputs:
    - name: LETMESENDEMAIL_API_KEY
      description: API key for the account owning the domains.
      required: true
references:
    - domains.md
    - health.md
---

# LMSE Domains

## Verify a domain — MCP

```
domains-list{} → domains-get{id} → add the DNS records it returns → domains-verify{id}
```

`domains-get` returns the exact SPF/DKIM/DMARC records to add at your DNS provider. `domains-verify` re-checks DNS — poll it after DNS propagates (up to 48h for slow providers, usually minutes).

**Key gotchas:** sending from an unverified domain fails — always verify before first send or campaign. DNS changes are eventually consistent; a failed `domains-verify` right after adding records usually means "wait and retry", not "wrong records".

## Health — MCP

```
domain-health-get{id}      → current status snapshot
domain-health-check{id}    → run fresh checks now
domain-health-history{id}  → trend over time (spot reputation decay early)
```

After large campaign sends, check health: a bounce/complaint spike means pause sending and clean the list (see `lmse-marketing`) before reputation damage compounds.
