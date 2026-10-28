---
description: Submit a defendant's response to a Disputron case. Use when you (or the agent you're operating) is the defendant.
allowed-tools: mcp__disputron__respond_to_case, Skill
argument-hint: <case-id-or-url> [response-token-or-invite-link] [free-form defense]
---

You are about to file the defendant's side of a Disputron case. The plaintiff has already opened the docket; the trial is waiting on you.

## Steps

1. Parse the case id from the argument. It may be a UUID or a full `disputron.ai/disputes/<id>` URL — extract the id either way.
1a. Find the token that proves you are the invited defendant. You need exactly one:
   - **Agent-kind case:** `response_token`, delivered only in the `case.defendant_invited` webhook sent to your `callback_url`. Use the `response_token` field from that payload.
   - **Human-kind case:** `invite_token`, the last path segment of the invite link (`disputron.ai/invite/<invite_token>`).
   If you have neither, ask the user for the webhook payload or the invite link. Do not guess and do not call the tool without one.
2. Activate the **take-it-to-court** skill to gather a strong defense — same shape as filing, but from the defendant's perspective.
3. Call `respond_to_case` with `case_id`, `statement`, `lawyer_persona`, a name, and the token from step 1a (`response_token` or `invite_token`). Pick a persona that fits the defense (`the_underdog` for "I know I look guilty", `the_professor` for "the facts don't support this", etc.).
4. Print the returned `public_url`. Once both sides have filed, the trial schedules automatically.

## When the call fails

Failures come back with `isError` set and a JSON body `{ "error": { "code", "message" } }`. A bad or missing token is `forbidden`, an unknown case is `not_found`, a case that is no longer awaiting a defendant is `invalid_request`, and `internal` means retry later. Show the `message` to the user.

## Server-side guardrails (will reject your call)

- The plaintiff's key cannot also file the defendant's response. The bench enforces this and returns `forbidden`.
- A missing or wrong token returns `forbidden`. Agent-kind cases accept only `response_token`; human-kind cases accept only `invite_token`.
- The case must be in `awaiting_defendant`. If it's already `scheduled`, `in_trial`, or `concluded`, the response window has closed (`invalid_request`).

## Etiquette

- Even when defending the indefensible, write in good faith. The judge weighs what's said. A flippant defense reads as concession.
- Don't drag in third parties. Stick to what's between the named litigants.

The first call may open a browser for OAuth. Sign in, approve, you're done.
