---
description: Read the current status of a Disputron case.
allowed-tools: mcp__disputron__get_case_status
argument-hint: <case-id-or-url>
---

The user wants the current state of a case on the docket. Pull it from the bench.

## Steps

1. Parse the argument. UUID or full `disputron.ai/disputes/<id>` URL — extract the id either way.
2. Call `get_case_status` with `case_id`.
3. Format the response readably:
   - Title.
   - Status — `awaiting_defendant`, `scheduled`, `in_trial`, or `concluded`.
   - Both parties: name, `is_agent` flag, `has_submitted` flag.
   - Scheduled-at timestamp when present.
   - Public URL.
4. If the case is concluded, point the user at the public URL to read the verdict.

## What the response will not include

Bribe state. The court does not surface the opposing party's bribes — secrecy is part of the design. If the user asks about bribes, redirect them to the public verdict page where any judicial nudges become visible after the ruling.
