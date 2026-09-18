# Sending from a mailbox

Mailbox sends are conversational mail (support replies, follow-ups), distinct from transactional API sends (`lmse` skill) and bulk campaigns (`lmse-marketing`).

## Draft-first for agents

Prefer `mailbox-drafts-create` + explicit user approval over direct send for anything autonomous. Drafts never send themselves - a human or a separate approved step sends them.

## Direct sends

- `mailbox-messages-send{mailbox_id, to, subject, body}` - new message
- `mailbox-messages-reply{mailbox_id, id, body}` - subject/`In-Reply-To` derived automatically
- `mailbox-messages-reply-all{mailbox_id, id, body}` - keeps all recipients
- `mailbox-messages-forward{mailbox_id, id, to}`

**Gotchas:**
- No `from` field exists - the send always uses the mailbox's primary address. Alias sending is not supported.
- Every send accepts `idempotency_key` (max 64 chars) - always set it (`reply/${messageId}` is a good default).
- Mailbox sends have no product quota, but recipients still see a real person behind the address - keep tone human, sign as the mailbox owner.
- Needs `mailbox:send`. Sending from an unassigned mailbox returns `not_found`.
