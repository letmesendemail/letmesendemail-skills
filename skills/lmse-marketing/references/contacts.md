# Contacts

- `contacts-list{}` — paginated (`limit`/`cursor`, see `lmse-mcp`); filter per the tool schema.
- `contacts-get{id}` — full record including custom properties.
- `contacts-create{...}` — email required; see the live tool schema for optional fields (name, properties).
- `contacts-update{id, ...}` — patch fields; unsubscribes respected automatically.

**List hygiene (do this or campaigns suffer):**
- Verify new addresses (`email-verification-check`) before adding — especially imports.
- Honor bounces/complaints from webhooks (`lmse` skill): suppress those addresses, never re-add.
- Deleting vs unsubscribing: prefer unsubscribe status over hard delete for compliance history.
