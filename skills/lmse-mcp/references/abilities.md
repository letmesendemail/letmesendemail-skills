# Ability tiers

Mailbox tools are gated on key abilities **and** mailbox assignment. Abilities are never granted automatically.

| Tier | Abilities | Unlocks |
|---|---|---|
| Reader | `mailbox:read` | `mailboxes-list/get`, `mailbox-messages-list/search/get/thread` |
| Organizer | + `mailbox:write` | `mailbox-drafts-create/update`, `mailbox-messages-action` (star/archive/move/delete/restore) |
| Full assistant | + `mailbox:send` | `mailbox-messages-send/reply/reply-all/forward` |

Non-mailbox tools (emails, domains, contacts, campaigns) authorize against the account - no ability needed beyond a valid key.

**Choosing a tier:** summarizers → Reader. Triage bots → Organizer (draft-first sending needs no `send`). Anything that sends mail itself → Full assistant, with the `lmse-mailbox` security patterns applied.
