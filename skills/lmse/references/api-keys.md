# API keys

Create and manage keys in the dashboard: user menu → API keys.

- Keys are shown once at creation - copy the full value (format `{id}|{secret}`, no fixed prefix). Store in `LETMESENDEMAIL_API_KEY`; never commit to source.
- **Abilities:** each key grants a subset of `mailbox:read`, `mailbox:write`, `mailbox:send`. Grant the minimum the integration needs - a key that only lists mailboxes needs just `mailbox:read`. Keys are never granted abilities automatically.
- **Assignment:** mailbox tools additionally require the key's owner to be assigned to the mailbox. A key with `mailbox:send` still cannot send from a mailbox it isn't assigned to.
- Rotate keys on team changes or suspected leaks; revocation is immediate.
