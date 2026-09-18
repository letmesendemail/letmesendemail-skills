# Reading mail

- `mailboxes-list{}` — all mailboxes the key owner can access. `mailboxes-get{id}` for one.
- `mailbox-messages-list{mailbox_id, limit, cursor}` — newest first. Default 25, max 100 per page; follow `pagination.next_cursor` while `has_more` is true.
- `mailbox-messages-search{mailbox_id, query}` — full-text search across subject/body/sender.
- `mailbox-messages-get{mailbox_id, id}` — full body plus headers (use for acting on one message).
- `mailbox-messages-thread{mailbox_id, id}` — whole conversation for context before replying.

**Gotchas:**
- All mailbox tools take an explicit `mailbox_id` — there is no ambient "current mailbox".
- Unknown or unassigned mailboxes return `not_found` (indistinguishable from missing — do not leak which).
- List responses are summaries; always `get` before quoting content or acting on it.
