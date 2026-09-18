# Client setup

Server: `https://mcp.letmesend.email/` (streamable HTTP), 34 tools.

OAuth is the primary path: supported clients discover
`https://mcp.letmesend.email/.well-known/oauth-protected-resource`
automatically, register via DCR, and walk the user through consent (mailbox
ability tiers are chosen there). Bearer header below is the headless
alternative: `Authorization: Bearer ${LETMESENDEMAIL_API_KEY}`.

- **opencode** (`opencode.json` → `mcp.letmesendemail`): `type: remote`, `url`, `enabled: true`, `headers: {Authorization}`
- **Claude Code**: `claude mcp add --transport http letmesendemail <url> --header "Authorization: Bearer <key>"`
- **Claude Desktop** (`claude_desktop_config.json` → `mcpServers.letmesendemail`): `type: http`, `url`, `headers`
- **Codex CLI** (`~/.codex/config.toml` → `[mcp_servers.letmesendemail]`): `url` + `bearer_token_env_var = "LETMESENDEMAIL_API_KEY"`, or one-liner `codex mcp add … --bearer-token-env-var`
- **Cursor** (MCP settings → `mcpServers.letmesendemail`): `url` + `headers`
- **GitHub Copilot** (VS Code `mcp.servers.letmesendemail`): `type: http`, `url` + `headers`
- **Claude Web** custom connectors: Bearer-header connectors are beta/unreliable — use a desktop/CLI client until OAuth ships.

After connecting, verify with `tools/list` (34 tools across pages) then `tools/call mailboxes-list {}`.
