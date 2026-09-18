# Deliverability health

- `domain-health-get{id}` — current snapshot (verification, DNS alignment, recent signals).
- `domain-health-check{id}` — triggers fresh checks; use after DNS changes or incidents.
- `domain-health-history{id}` — trend line; the early-warning system for reputation decay.

**Reading the signals:**
- Rising bounces → dirty list: verify + suppress before next send.
- Rising complaints → content/audience mismatch or missing unsubscribe: fix the campaign, not the DNS.
- SPF/DKIM failures after working fine → someone changed DNS: re-check records via `domains-get` and republish.
- Everything green but inboxing drops → warm up gradually, check `email-verification-check` on new addresses, review complaint rate.

Check history after every large send; a healthy trend is the deliverability moat.
