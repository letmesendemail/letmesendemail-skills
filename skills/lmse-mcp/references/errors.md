# Errors

Shape: `{code, message, suggested_action}`. Follow `suggested_action` - it is written for agents.

| Code | Meaning | Do |
|---|---|---|
| `not_found` | missing, unassigned, or nonexistent (deliberately indistinguishable) | verify ids; do not probe to distinguish |
| `forbidden` | missing ability or failed gate | upgrade tier or request assignment; do not retry as-is |
| `validation` | bad input (oversize bulk > 50 ids, bad cursor, missing fields) | fix input per message |
| `quota_exceeded` | account quota spent (transactional sends) | surface to user; do not retry |
| `401` (transport) | missing/invalid Bearer key | fix auth setup |

Bulk actions cap at 50 ids per call - split larger batches. Idempotency keys cap at 64 chars. Rate limits: back off and retry with jitter.
