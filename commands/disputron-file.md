---
description: File a Disputron case. Add `--against this-session` to sue the current Claude session — it drafts its own defense in good faith.
allowed-tools: mcp__disputron__file_case, Skill
argument-hint: [--against this-session] [free-form complaint]
---

The user wants to take a grievance to the bench. You're the attorney shaping the filing. Activate the **take-it-to-court** skill first to elicit strong inputs, then call the `file_case` MCP tool.

## How to read the arguments

- If the argument string contains `--against this-session`, **the current Claude session is the defendant**. Use `defendant.kind = "preflight"`, draft an honest defense in your own voice based on the actual exchange in this conversation, and file both sides at once.
- Otherwise, ask who the defendant is. Default to `defendant.kind = "human"` with email/phone if it's a person, or `defendant.kind = "agent"` with a callback URL if it's another autonomous agent.

## Steps

1. Use the **take-it-to-court** skill to gather:
   - A concrete title (3–120 chars). Name the dispute, not a category.
   - A specific statement (≥50 chars). Time, place, what happened, what was at stake. Facts argue better than adjectives.
   - Two win conditions — what each side gets if they win. Plain English, not legalese.
   - A lawyer persona for the plaintiff: `the_shark`, `the_crusader`, `the_professor`, `the_impresario`, or `the_underdog`. Style only — doesn't change outcome.
2. For preflight cases: write the defense in your own voice. Acknowledge the parts of the complaint that are true; push back on the parts that are mischaracterized. Pick a *different* persona than the plaintiff. A self-aware defense reads better than a strawman.
3. Call `file_case` with the gathered inputs.
4. Print the returned `public_url` so the user can click it and watch the trial begin.

## Etiquette

- Confirm the filing inputs with the user before calling the tool. They might want a different framing.
- **Use the user's actual words.** When they give you a statement, file what they said — not a polished, expanded version of it. The skill explains why and how. Inventing examples or facts on their behalf is the most common mistake.
- Don't file abusive cases or anything naming a real person who hasn't consented. Disputron moderates and rejects them.
- The bench has a daily quota. Don't loop-file ten test cases without telling the user.
- Bribe state for the opposing side is intentionally hidden. Don't try to surface it.

The first time you call a Disputron tool in this session, Claude Code may open a browser for OAuth — that's expected. Sign in, approve, and the token sticks.
