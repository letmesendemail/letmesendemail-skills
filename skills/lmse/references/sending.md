# Sending transactional email

Single-recipient sends go to `POST /emails` (SDK: `client.emails.send`, MCP: `emails-send`).

## Required fields

- `from` - must be on a verified domain (see `lmse-domains`)
- `to` - array with exactly one recipient for transactional sends
- `subject`, and one of `html` / `text`
- `type: "transactional"`

## Idempotency (do not skip)

Pass a stable `idempotencyKey` (SDK) / `idempotency_key` (API/MCP) on every send - e.g. `welcome-email/${userId}`. Retries with the same key return the original email instead of sending a duplicate. Keys are capped at 64 characters.

```typescript
await client.emails.send({
  from: "Acme <hello@acme.com>",
  to: ["person@example.com"],
  subject: "Welcome",
  html: "<p>Welcome!</p>",
  type: "transactional",
  idempotencyKey: `welcome-email/${userId}`,
});
```

The SDK sends the key as the `Idempotency-Key` header.

## Quotas

Transactional sends count against the account quota. When the quota is exhausted the API/MCP returns a `quota_exceeded` error - surface it to the user, do not retry.

## Bulk / marketing sends

Do not loop `emails.send` for newsletters or announcements - use campaigns (`lmse-marketing` skill) instead. Mailbox replies (`lmse-mailbox` skill) are a separate path with no quota.
