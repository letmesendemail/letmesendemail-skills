---
name: lmse-domains
description: Use when managing sending domains on LetMeSend.Email - listing domains, verifying DNS (SPF/DKIM/DMARC), checking deliverability health over time, and fetching business info (logo, brand colors, typography) for email building. Always use this skill when the user mentions domain setup, DNS records, verification status, spam-folder problems, sender reputation, or branding placeholders on LMSE. No domain can send until it is verified.
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

## Verify a domain - MCP

```
domains-list{} → domains-get{id} → add the DNS records it returns → domains-verify{id}
```

`domains-get` returns the exact SPF/DKIM/DMARC records to add at your DNS provider. `domains-verify` re-checks DNS - poll it after DNS propagates (up to 48h for slow providers, usually minutes).

**Key gotchas:** sending from an unverified domain fails - always verify before first send or campaign. DNS changes are eventually consistent; a failed `domains-verify` right after adding records usually means "wait and retry", not "wrong records".

## Health - MCP

```
domain-health-get{id}      → current status snapshot
domain-health-check{id}    → run fresh checks now
domain-health-history{id}  → trend over time (spot reputation decay early)
```

After large campaign sends, check health: a bounce/complaint spike means pause sending and clean the list (see `lmse-marketing`) before reputation damage compounds.

## Business info - MCP

```
domain-business-info-get{id} → business_info + styles + typography + fonts
```

Use before building any email: it returns the exact placeholder keys (`__BUSINESS_NAME__`, `__STYLE_PRIMARY_BRAND_COLOR__`, `__TYPO_BODY_FONT_SIZE__`, …) with stored values and canonical defaults merged in. `defaults_applied` flags values the account never customized - if the logo keys are defaults, ask the user for a logo rather than shipping a generic email.
