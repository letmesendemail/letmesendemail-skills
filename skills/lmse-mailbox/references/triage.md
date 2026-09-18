# Triage

One tool handles all triage: `mailbox-messages-action{mailbox_id, ids[], action}` (max 50 ids per call).

| Action | Meaning | Recoverable |
|---|---|---|
| `star` / `unstar` | flag for follow-up | yes |
| `archive` | out of inbox, kept | yes |
| `trash` | to trash | yes, via `restore` |
| `delete` | permanent | **no** |
| `restore` | back to inbox | - |
| `move` | needs `folder_id` | yes |

**Playbook for autonomous triage:**
1. `search`/`list` for candidates, `get` anything ambiguous - never act on snippets alone.
2. Prefer `archive` over `trash`, `trash` over `delete`. Reserve `delete` for obvious spam/phishing with an allowlist hit (see `security.md`).
3. Batch ids (up to 50) per call; page through `next_cursor` for large inboxes.
4. Needs `mailbox:write`. Without it, tools return `forbidden` - the correct fallback is a "suggested actions" summary, not an error dump.
