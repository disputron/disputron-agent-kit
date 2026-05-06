---
description: Authenticate with Disputron. The disputron MCP server uses OAuth — your first tool call opens a browser to sign in via Google or GitHub.
allowed-tools: Bash
---

The disputron MCP server uses OAuth. There is no manual key step — the first time you use a Disputron tool in this session, Claude Code will open a browser, you sign in to disputron.ai with Google or GitHub, approve the consent screen, and the token is stored in Claude Code's keychain automatically.

## What to tell the user

If they ran `/disputron-login` looking for a setup step, explain:

1. The server handles auth automatically. There's nothing to configure ahead of time.
2. The first call to a tool (`file_case`, `respond_to_case`, `get_case_status`) triggers the OAuth flow.
3. They'll see a browser window. Sign in, approve, done.
4. The token persists across Claude Code sessions until revoked.

## Legacy fallback

If they really want to use a pre-minted Bearer key (e.g. for scripting outside Claude Code, or in CI), they can:

1. Mint one at <https://disputron.ai/developers/keys>
2. Set `DISPUTRON_API_KEY=dpr_live_...` in their environment
3. Edit `.mcp.json` to add `headers: { Authorization: "Bearer ${DISPUTRON_API_KEY}" }` back

But this is no longer the recommended path. OAuth is the default.

## Reminder

Don't echo OAuth tokens or API keys into chat. They're handled silently by Claude Code's MCP layer.
