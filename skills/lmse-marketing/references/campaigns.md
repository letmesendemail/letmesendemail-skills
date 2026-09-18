# Campaigns

Bulk sends. Lifecycle: create → review → schedule/send → (cancel if needed).

- `campaigns-list{}` / `campaigns-get{id}` — inspect content, audience, status.
- `campaigns-create{...}` — content + audience; see the live tool schema for exact fields (they vary by template support).
- `campaigns-update{id, ...}` — edit only while unsent/unscheduled.
- `campaigns-schedule{id, ...}` — queue for a future time.
- `campaigns-send{campaign_id}` — sends now. **Only field: `campaign_id`.** Content and recipients are read from the campaign.
- `campaigns-cancel{id}` — stops a scheduled (not yet sending) campaign.

**Gotchas:**
- A send can be refused on verification status — always `campaigns-get` after send/schedule to confirm state.
- Test with a small seed audience (your own addresses) before the full list.
- Every campaign must include a working unsubscribe path — handled by the platform when using campaign templates; verify for custom HTML.
- Watch domain health (`domain-health-get`) after large sends; a bounce spike means pause and clean the list.
