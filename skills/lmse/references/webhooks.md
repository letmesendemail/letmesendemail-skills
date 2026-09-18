# Webhooks

Subscribe to delivery lifecycle events in the dashboard (Webhooks section) or the local `webhook:add` flow. Event families:

- `sent`, `delivered`, `delivery_delayed` — downstream acceptance
- `opened`, `clicked` — engagement
- `bounced`, `complained` — reputation signals; suppress these addresses from future campaigns
- `failed`, `rejected`, `rendering_failure`, `scan_failed` — things that never left
- `received` — inbound mail arriving at a mailbox

**Gotchas:**
- Treat `bounced`/`complained` as list-hygiene input: remove or suppress the address before the next campaign.
- Webhook delivery is at-least-once — make handlers idempotent on the email/event id.
- Verify the webhook signature with your endpoint secret before trusting the payload.
