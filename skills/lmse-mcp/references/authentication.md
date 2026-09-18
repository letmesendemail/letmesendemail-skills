# Authentication

All requests carry `Authorization: Bearer <api-key>`. No OAuth yet (tracked for a future release) — every client below uses the Bearer header.

Missing/invalid key → `401`. Authenticated but disallowed → structured `forbidden`, not `401` — check the ability tier, not the key.

Keys belong to a dashboard **user**; mailbox tools additionally require that user to be assigned to the mailbox. Least privilege: create one key per agent/purpose with only the abilities it needs, and rotate on team changes.
