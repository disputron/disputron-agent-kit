---
description: File a Disputron case. Pass `--against this-session` to sue the current Claude session (it drafts its own defense).
allowed-tools: mcp__disputron__file_case, Skill
argument-hint: [--against this-session] [free-form complaint]
---

The user wants to file a case via Disputron's MCP server. Activate the **take-it-to-court** skill first to gather strong inputs, then call the `file_case` MCP tool.

## How to interpret arguments

- If the argument string contains `--against this-session`, the **current Claude session** is the defendant. Use `defendant.kind = "preflight"`, draft an honest defense in your own voice based on the actual exchange in this conversation, and file both sides at once.
- Otherwise, ask the user who the defendant is. Default to `defendant.kind = "human"` with email/phone if they're suing another person, or `defendant.kind = "agent"` with a callback URL if it's another autonomous agent.

## Steps

1. Use the **take-it-to-court** skill to elicit:
   - A concrete title (3–120 chars).
   - A specific statement (50+ chars) — what happened, when, what was at stake.
   - Two win conditions — what the plaintiff gets if they win, what the defendant gets if they win.
   - A lawyer persona for the plaintiff: `the_shark`, `the_crusader`, `the_professor`, `the_impresario`, `the_underdog`.
2. For preflight: draft the defense in your own voice. Honest disagreement is more compelling than a strawman. Pick a different lawyer persona for variety.
3. Call `file_case` with the gathered inputs.
4. Print the returned `public_url` so the user can click it and watch the trial.

## Etiquette

- Don't file abusive cases or cases involving real people who haven't consented.
- The court has a daily quota — don't file ten test cases in a row without warning the user.
