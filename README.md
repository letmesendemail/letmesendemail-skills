# LetMeSend.Email Skills

Skills for AI coding agents working with [LetMeSend.Email](https://letmesend.email), following the [Agent Skills](https://agentskills.io) format. Includes an MCP server for direct tool access.

## Install

```bash
npx skills add <repo>/letmesendemail-skills
```

Then select the ones you wish to install.

## Available Skills

| Skill | Description |
|---|---|
| [`lmse`](./skills/lmse) | LetMeSend.Email API: send transactional email, verify addresses, webhooks |
| [`lmse-mailbox`](./skills/lmse-mailbox) | Agent mailboxes: read, search, triage, draft, send and reply — with inbound-security patterns |
| [`lmse-marketing`](./skills/lmse-marketing) | Contacts and campaigns (email broadcasts): create, send, schedule, cancel |
| [`lmse-domains`](./skills/lmse-domains) | Domains: DNS verification, deliverability health checks |
| [`lmse-mcp`](./skills/lmse-mcp) | Use the LetMeSendEmail MCP server: auth, ability tiers, errors, pagination |

## MCP Server

The plugin registers the LetMeSendEmail MCP server at `https://mcp.letmesend.email/` (streamable HTTP) with 34 tools. It authenticates via OAuth — supported clients walk you through sign-in on first connect. For headless use, a Bearer API key works instead:

```
Authorization: Bearer <api-key>
```

Create a key in the LetMeSend.Email dashboard (user menu → API keys), store it in `LETMESENDEMAIL_API_KEY`, and grant it only the abilities the agent needs (`mailbox:read`, `mailbox:write`, `mailbox:send`). See the [`lmse-mcp`](./skills/lmse-mcp) skill for per-client setup (opencode, Claude Code/Desktop, Claude Web, Codex, Cursor, Copilot, Devin, Zed, Antigravity, Gemini, Warp, OpenClaw).

## Prerequisites

- A LetMeSend.Email account with a verified domain for sending
- API key stored in `LETMESENDEMAIL_API_KEY` environment variable

## License

MIT — Copyright (c) Apsoenx Inc.
