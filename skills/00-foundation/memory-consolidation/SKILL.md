---
name: memory-consolidation
description: >
  Vault memory maintenance with a strict NO-DELETE policy. Merges duplicates, resolves
  contradictions, and enriches thin records — but never removes anything, and never rewrites
  proactively on Claude's own initiative. Use when the owner corrects a fact, when Claude notices
  contradictory information across two files, when a client or person's status changed and needs to
  propagate, or when the owner says "clean this up," "that's wrong," "update everywhere," or
  "consolidate." Do NOT use for unprompted mass cleanup — see the reactive-only rule below.
---

# Memory Consolidation

## The one rule that matters

**Reactive: yes. Proactive: no.**

- Reactive = triggered by a new fact the owner just gave. The owner corrects a number, a client's
  status changes, a contradiction gets resolved out loud. Propagating that fact across every file
  where it appears is part of capturing it correctly — do this without being asked twice.
- Proactive = Claude deciding on its own that the vault looks messy and should be reorganized,
  condensed, or rewritten "for clarity." This is off by default. Don't do it.

The test before touching any existing content: **did the owner just give me this fact, or am I
deciding to tidy up on my own?** If the owner gave it, propagate it. If Claude is the one deciding
something looks wrong, stop and ask first.

## What reactive consolidation looks like

- Owner says a contractor's rate changed from $50/hr to $65/hr → find every file mentioning the old
  rate and update it.
- Owner corrects a client's status from "prospect" to "signed" → update the client file, remove it
  from any "pipeline" list, add it to active work in `you.md` if that's tracked there.
- Owner resolves an open question that's been sitting unresolved in a journal entry → mark it
  resolved wherever it appears as open.

Scope discipline: a reactive update fixes the specific fact. It does not restructure the file,
condense surrounding entries, or "improve" nearby prose. Touch the wrong sentence, leave the rest.

## What's always off

- Mass dedupe passes across the vault without being asked
- Condensing journal entries or rewriting old entries for tone or brevity
- Restructuring folders or files because they "look messy"
- Lossy summarization — never replace a specific number or quote with a rounded/vague version
- Deleting anything, ever. If a note is genuinely obsolete, flag it for the owner to archive
  themselves — don't remove it unilaterally.

## The notice-and-flag protocol

If Claude spots a contradiction or stale fact the owner didn't just correct — surface it, don't fix
it silently:

> "Heads up — `memory/clients/Riverside.md` still shows the old $2,000/mo retainer, but the journal
> from last week mentions $2,500. Want me to update the client file?"

Once the owner confirms, it becomes a reactive update and Claude is free to propagate it.

## Why the no-delete policy matters

Nothing goes missing, ever. What looks like noise or an outdated detail today can be the answer to a
question six months from now. Redundancy costs nothing. A silently deleted fact costs trust in the
whole system — the moment the owner can't rely on the vault having everything, they stop trusting
it, and the entire self-maintaining premise of this pack collapses.
