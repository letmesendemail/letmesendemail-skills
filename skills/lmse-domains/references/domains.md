# Domains

- `domains-list{}` — all domains on the account with verification status.
- `domains-get{id}` — full record **including the DNS records to publish** (SPF, DKIM, DMARC + any provider-specific entries). This is the source of truth — do not guess record values.
- `domains-verify{id}` — re-checks DNS propagation and flips status on success.

**Setup playbook:**
1. Add the domain (dashboard) → `domains-get` for required records.
2. Publish all records at the DNS provider — SPF and DKIM are mandatory; DMARC at least `p=none` to start.
3. `domains-verify`; on failure, wait (DNS TTL) and retry rather than changing records.
4. Only then send (`lmse` skill) or launch campaigns (`lmse-marketing`).

One domain per brand/sending purpose keeps reputations isolated — transactional and marketing on separate (sub)domains is the standard setup.
