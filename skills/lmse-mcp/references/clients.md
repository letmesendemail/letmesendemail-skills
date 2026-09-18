# Client setup

Server: `https://mcp.letmesend.email` (streamable HTTP), 35 tools.

OAuth is the primary path: point the client at the server URL and it
discovers `https://mcp.letmesend.email/.well-known/oauth-protected-resource`
on its own, registers via DCR, and walks the user through consent (mailbox
ability tiers are chosen there). Bearer is the headless alternative:
`Authorization: Bearer ${LETMESENDEMAIL_API_KEY}` (omit the header/auth
options below when using OAuth).

- **Claude Web**: Settings → Connectors → Add custom connector → server URL.
- **Claude Code**: `claude mcp add --transport http letmesendemail <url>` (+ `--header "Authorization: Bearer <key>"` for Bearer mode)
- **Claude Desktop**: Settings → Connectors → Add custom connector → server URL.
- **Codex CLI**: `codex mcp add letmesendemail --url <url>` (+ `--bearer-token-env-var LMSE_API_KEY` for Bearer mode)
- **Cursor** (MCP settings → `mcpServers.letmesendemail`): `{url}` (+ `headers` for Bearer mode)
- **GitHub Copilot** (VS Code `mcp.servers.letmesendemail`): `{type: http, url}` (+ `headers` for Bearer mode)
- **opencode** (`opencode.json` → `mcp.letmesendemail`): `{type: remote, url, enabled: true}` (+ `headers` for Bearer mode)
- **Devin** (`mcpServers.letmesendemail`): `{transport: HTTP, url}`
- **Zed** (`context_servers.letmesendemail`): `{url}`
- **Antigravity** (`mcpServers.letmesendemail`): `{serverUrl}`
- **Gemini** (`mcpServers.letmesendemail`): `{httpUrl}`
- **Warp** (`letmesendemail`): `{serverUrl}`
- **OpenClaw**: `openclaw mcp add letmesendemail --url <url> --transport streamable-http`

After connecting, verify with `tools/list` (35 tools across pages) then `tools/call mailboxes-list {}`.
