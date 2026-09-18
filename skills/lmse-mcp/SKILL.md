---
name: lmse-mcp
description: Use when connecting an AI client to the LetMeSendEmail MCP server or debugging its responses - authentication setup per client, the three mailbox ability tiers, error codes with suggested actions, and cursor pagination. Always use this skill when tools/list or tools/call against https://mcp.letmesend.email misbehaves, or when choosing what key abilities an agent needs.
license: MIT
metadata:
    author: LetMeSend.Email
    version: "1.0.0"
    homepage: https://letmesend.email
inputs:
    - name: LETMESENDEMAIL_API_KEY
      description: Bearer API key sent as `Authorization: Bearer <key>` on every MCP request.
      required: true
references:
    - authentication.md
    - abilities.md
    - errors.md
    - clients.md
---

# LetMeSendEmail MCP

- **URL:** `https://mcp.letmesend.email` (streamable HTTP), server name `LetMeSendEmail`, 35 tools
- **Auth:** `Authorization: Bearer <api-key>` - dashboard user menu → API keys (copy the full value shown once at creation)
- **Discovery:** `GET https://letmesend.email/mcp.json` (also served as `/.well-known/mcp.json`) lists tools + client configs live

## Pagination (all list tools)

Request `{limit, cursor}` (`limit` default 25, max 100). Response carries `pagination: {next_cursor, has_more}` - pass `next_cursor` as `cursor` until `has_more` is false. `tools/list` itself paginates the same way.

## Errors

Every error is structured: `{code, message, suggested_action}` - read `suggested_action` before retrying. Common codes: `not_found`, `forbidden`, `validation`, `quota_exceeded`. Details in `errors.md`.

## Ability tiers

`mailbox:read` → Reader · +`mailbox:write` → Organizer · +`mailbox:send` → Full assistant. Details in `abilities.md`.
