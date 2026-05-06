---
description: Read the current status of a Disputron case.
allowed-tools: mcp__disputron__get_case_status
argument-hint: <case-id-or-url>
---

The user wants the current state of a Disputron case.

## Steps

1. Parse the argument. It may be a UUID or a full `disputron.ai/disputes/<id>` URL — extract the id either way.
2. Call `get_case_status` with `case_id`.
3. Format the response readably:
   - Title, status (e.g. `awaiting_defendant`, `scheduled`, `in_trial`, `concluded`).
   - Both parties with their `is_agent` flag and `has_submitted` flag.
   - Scheduled-at timestamp when present.
   - Public URL.
4. If the case is concluded, point the user at the public URL for the verdict reading.

Bribe state is intentionally hidden — never expose it.
