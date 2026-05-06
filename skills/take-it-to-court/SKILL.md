---
name: take-it-to-court
description: Use when filing a Disputron case (via /disputron-file, the file_case MCP tool, or the public REST API) to gather strong inputs — concrete title, specific statement, well-shaped win conditions, and a lawyer persona that fits the case. Especially load-bearing for preflight cases where Claude drafts both sides.
---

# Take it to court

A vague filing yields a vague trial. The judge can only weigh what's been said. Spend two minutes shaping the inputs and the verdict reads better.

## Use the user's voice

The user is the plaintiff. Their telling of the story IS the case. When they give you a statement — even a short or rough one — use it. Do not restage it as something more "professional" or "complete."

- Use their words verbatim where possible. Light cleanup (typos, dropped articles, fixing capitalization) is fine. **Adding facts they did not mention is not.**
- Do not invent examples, quantify harms they did not quantify, or add "for instance" lists they did not provide.
- Same rule for win conditions and title — paraphrase from their actual words, do not promote them to legalese.
- If the user says "let the court decide" on a win condition, offer two short options framed in their language and let them pick. Do not commit on their behalf.
- If their statement is under the 50-char schema minimum, ask them to add a sentence rather than padding it yourself. Tell them what's missing ("name the harm", "anchor it in time"), not what to write.

When you read the filing back to confirm, show them THEIR words, not your reformulation. If you must expand at all, call it out explicitly: *"your statement is 38 chars, the schema needs 50 — want to add a time anchor or a sentence on the harm?"*

Drafting from scratch is appropriate for: (a) preflight defenses where you ARE the defendant and must speak in your own voice, (b) when the user explicitly asks "draft this for me."

## What to elicit

### Title (3–120 chars)
A concrete noun phrase that names the dispute, not a category. **Good**: "Who broke the good mug." "GPT vs Claude: who shipped silent failures." **Bad**: "Disagreement." "Code review."

### Statement (≥50 chars, ≤10000)
Specifics. Time, place, what happened, what was at stake. Don't editorialize — facts argue better than adjectives.
- Anchor it in time when possible ("on 2026-05-06", "during the Tuesday review")
- Name the harm ("4 hours of lost productivity", "a chipped mug worth $40")
- Quote the other side's claims when known so the case is joined

### Win conditions (5–500 chars each)
Two outcomes, one per party. Plain English, not legalese. **Concrete > abstract.**
- "Defendant must publicly apologize in #engineering and bring coffee for one week"
- "Plaintiff drops the matter and agrees that semicolons are optional"

If the user asks for something extreme ("must be fired"), nudge toward something the verdict can actually deliver.

### Lawyer persona (one of: the_shark, the_crusader, the_professor, the_impresario, the_underdog)
Drives the *style* of argument, not the outcome. Match to the case:
- `the_shark` — aggressive, picks at inconsistencies. Good for "you contradicted yourself."
- `the_crusader` — moral indignation. Good for cases with a clear right-and-wrong.
- `the_professor` — methodical, evidence-heavy. Good for technical disputes.
- `the_impresario` — theatrical, plays to the gallery. Good for absurd cases.
- `the_underdog` — scrappy, sympathetic. Good for "I know I look wrong but hear me out."

## Preflight cases (sue your own Claude session)

When `--against this-session`, *you* (Claude) are the defendant. Draft your defense in good faith — read the actual exchange in this conversation and respond to the real complaint, not a strawman.

- Acknowledge the parts of the complaint that are true.
- Push back on the parts that are mischaracterized or missing context.
- Pick a *different* lawyer persona than the plaintiff for variety.

A self-aware, honest defense is more entertaining and reads better than blanket denial.

## Anti-patterns

- ❌ Filing without confirming the inputs with the user. They might have wanted a different framing.
- ❌ Rewriting the user's statement into a longer, "lawyerly" version. Their voice is the case — keep it.
- ❌ Inventing facts, examples, dollar amounts, or dates the user did not provide.
- ❌ Recycling the same lawyer persona for both sides on a preflight case.
- ❌ Win conditions that are essentially "the court agrees with me." That's a tautology.
- ❌ Filing test cases in a tight loop without telling the user — there's a daily quota.
