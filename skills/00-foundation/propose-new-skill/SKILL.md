---
name: propose-new-skill
description: >
  Self-expansion mechanism — drafts a new SKILL.md when Claude notices it has done the same
  multi-step manual task three or more times with no matching skill in the pack. Use when a recurring
  workflow pattern emerges that isn't covered by any existing skill, or when the owner says "you keep
  doing this the same way, can we make it a skill," "turn this into something repeatable," or "can
  you remember how I like this done." This is how the pack grows to fit the specific business it's
  installed in, instead of staying frozen at the 25 skills it shipped with.
---

# Propose New Skill

## Why this exists

A generic skill pack can cover the common cases, but every business has its own recurring weird
task — a specific report a landscaping client always wants formatted a certain way, a specific
intake process for a photography studio, a specific way a bookkeeper wants transactions categorized.
This skill is how the vault grows a skill for that, instead of Claude re-improvising it from scratch
every time and the owner re-explaining the same preferences every session.

## When to fire

- Claude notices it has done a structurally similar multi-step task 3+ times (same inputs → same
  kind of output, same steps in between), with no existing skill covering it
- The owner explicitly asks for something to become repeatable
- A `pattern-radar` pass surfaces a workflow pattern that keeps recurring

Don't fire for one-off tasks, even complex ones. Three occurrences is the threshold — below that,
it's not yet a pattern, it's a coincidence.

## How to draft a proposal

1. **Name it** — short, verb-first or noun-first, matching the style of existing skills in this pack
   (`invoice-chase`, `contract-guard`, not `HandleInvoiceFollowUps`).
2. **Write the trigger description** — be specific about what phrases or situations should fire it.
   Vague triggers cause skills to fire when they shouldn't or stay silent when they should.
3. **Document the actual steps** — pull from what Claude has actually done the last 3 times, not an
   idealized version. If the real process has a judgment call in it, write down what judgment was
   actually exercised.
4. **Flag what's still uncertain** — if the pattern held 3 times but might not generalize, say so in
   the draft rather than presenting it as settled.
5. **Present it to the owner as a draft, not a fait accompli:**

> "I've now handled onboarding intake for 3 new clients the same way — pulling scope from the
> discovery call notes, drafting a welcome email, and creating the client folder with a standard
> starter structure. Want me to save this as a skill (`client-onboarding`) so it's consistent and
> automatic going forward? Draft attached — take a look before I save it."

6. **Only save on confirmation.** This skill drafts and proposes; it never silently adds itself to
   the pack's active skill set. New skills change how Claude behaves — that's worth a yes.

## Where to save it

New skills go in a `custom/` folder alongside the existing category folders (`00-foundation`,
`01-core-ops`, etc.) so it's clear at a glance which skills shipped with the pack and which were
grown by this specific business's usage. Same `SKILL.md` format as every other skill in the pack.

## The bigger point

This is the mechanism that makes the "self-maintaining" claim actually true rather than marketing
language. A static pack goes stale the moment it ships. A pack that notices its own gaps and asks
before filling them stays useful as the business changes.
