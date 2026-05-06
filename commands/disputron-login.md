---
description: Save your Disputron API key so the disputron MCP server can authenticate.
allowed-tools: Bash, Read, Write
---

The user wants to authenticate with Disputron so that the MCP tools (`file_case`, `respond_to_case`, `get_case_status`) work in this session.

## Steps

1. Tell the user to mint a key at **https://disputron.ai/developers/keys** (open the page in their browser yourself if you have a `Browser` tool, otherwise just print the URL).
2. Ask the user to paste the key. It should start with `dpr_live_`.
3. Validate the prefix. If it doesn't start with `dpr_live_`, ask again.
4. Persist it. Two options, in order of preference:
   - If `~/.claude/disputron/auth.json` is writable, write `{ "apiKey": "<key>" }` there with mode `0600`.
   - Otherwise, advise the user to add `DISPUTRON_API_KEY=<key>` to their shell profile (referenced by `.mcp.json` as `${DISPUTRON_API_KEY}`).
5. Confirm to the user that the disputron MCP server should now work in new Claude Code sessions. (The current session may need a restart to pick up the env var.)

## Reminder

Treat the key like a password. Never echo it back to the chat after saving. Don't write it to anything that gets committed.
