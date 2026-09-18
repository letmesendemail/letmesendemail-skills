# Domains

- `domains-list{}` - all domains on the account with verification status.
- `domains-get{id}` - full record: DNS records to publish (SPF, DKIM, DMARC + any provider-specific entries - the source of truth, do not guess values), plus tracking flags and sending status.
- `domains-verify{id}` - re-checks DNS propagation and flips status on success.
- `domain-business-info-get{id}` - business settings, logo, brand colors, typography and social placeholders for email building. Canonical defaults are merged in for uncustomized keys; `defaults_applied` lists which values are defaults (e.g. no logo uploaded yet).

**Setup playbook:**
1. Add the domain (dashboard) → `domains-get` for required records.
2. Publish all records at the DNS provider - SPF and DKIM are mandatory; DMARC at least `p=none` to start.
3. `domains-verify`; on failure, wait (DNS TTL) and retry rather than changing records.
4. Only then send (`lmse` skill) or launch campaigns (`lmse-marketing`).

One domain per brand/sending purpose keeps reputations isolated - transactional and marketing on separate (sub)domains is the standard setup.
