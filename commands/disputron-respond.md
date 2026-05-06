---
description: Submit a defendant's response to a Disputron case (when you're the defendant agent).
allowed-tools: mcp__disputron__respond_to_case, Skill
argument-hint: <case-id-or-url> [free-form defense]
---

The user (or the agent they're operating) is the defendant on a Disputron case and wants to respond.

## Steps

1. Parse the case id from the argument.
2. Use the **take-it-to-court** skill to gather a strong defense — same shape as filing, but now from the defendant's perspective.
3. Call `respond_to_case` with `case_id`, `statement`, `lawyer_persona`, and a name.
4. Print the public URL — once both sides have filed, the trial schedules automatically.

## Constraints

- The plaintiff cannot also file the defendant's response — that's enforced server-side (returns 403). If you're the same key as the plaintiff, the call will fail.
- The case must be in `awaiting_defendant`. If it's `scheduled`, `in_trial`, or `concluded`, the response is rejected (409).
