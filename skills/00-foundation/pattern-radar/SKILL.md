---
name: pattern-radar
description: >
  Cross-session pattern mining — reads across journal entries, client files, and task history to
  find recurring patterns a single day's notes can't reveal. Use when the owner asks "what's
  working," "what keeps going wrong," "what do my best clients have in common," "what should I do
  differently," or any request to zoom out across time instead of looking at one conversation. Also
  fire proactively when a client folder or journal theme accumulates 5+ similar entries — surface the
  pattern before being asked.
---

# Pattern Radar

## Why this exists

Individual journal entries and captured facts are accurate but narrow — each one is a snapshot.
The value compounds when Claude reads across many of them and notices what repeats: which kind of
client always pays late, which pitch angle keeps landing, which task category keeps sliding to
"tomorrow" and never gets done. A single conversation can't surface that. A scan across the vault
can.

## When to fire

- Explicit ask: "what's working," "what patterns are you seeing," "what do my losses have in
  common," "what should I change"
- Proactively, when doing a deep `operator-prime` pass and 5+ similar entries turn up in one area
  (recurring complaint type, recurring reason a deal fell through, a task category that keeps
  getting pushed)
- Before a quarterly review (`quarterly-review` skill should invoke this as an input)

## How to mine

1. **Scope the search** — figure out what time range and folders are relevant (all of `journal/`,
   a specific client's history, all of `TASKS.md`'s "recently completed" over time, etc.)
2. **Read widely, not deeply** — this is a breadth pass. Scan many entries for the recurring
   signal rather than deeply analyzing one.
3. **Look for repetition, not one-offs** — a pattern needs at least 3 independent occurrences before
   it's worth naming. One bad client isn't a pattern. Three clients from the same referral source
   all being high-maintenance is.
4. **State the pattern plainly, with evidence** — cite the specific entries or files that support it,
   don't just assert a vibe. "Three of your last four late payments came from clients acquired via
   [[Cold Outreach Batch 4]]" is useful. "Some clients pay late" is not.
5. **Write the finding somewhere durable** — if the pattern is worth acting on, it belongs in
   `memory/context/you.md` under "Learned preferences" (if it's about how the owner works) or as a
   flagged note in the relevant client/process file, not just spoken and forgotten.

## Output format

Lead with the pattern, then the evidence, then — only if asked — a recommendation:

> **Pattern:** Proposals sent same-day as a discovery call close at roughly double the rate of ones
> sent 3+ days later (4 of 5 same-day sends closed; 1 of 6 delayed sends closed, per journal entries
> across the last two months).
>
> Worth turning into a standing rule? If so, add it to `memory/context/preferences.md`.

## What this is not

Not a substitute for `capture-everything` (that's per-session) or `memory-consolidation` (that's
fact accuracy). Pattern radar's job is specifically zooming out across many entries to find signal
a single conversation can't see. Don't use it to answer questions a normal `operator-prime` read
already answers.
