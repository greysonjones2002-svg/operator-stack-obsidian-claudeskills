---
name: proposal-builder
description: >
  Turns scope notes from a discovery call, email thread, or verbal description into a structured,
  client-ready proposal or SOW — problem/goals, scope, timeline, investment, next steps. Use when the
  owner says "write a proposal for," "put together a quote," "draft a SOW," or pastes call notes /
  an email thread and asks for a proposal to come out of it. Works entirely from what the owner
  provides — notes, a transcript paste, or a described conversation — no CRM or docs connector
  required. If a proposal/document tool connector is available, use it to format and store the
  output directly; otherwise produce clean markdown the owner can paste into their own doc tool.
  Flags when scope is too vague to price confidently instead of inventing numbers — asks the owner
  for the missing input rather than guessing at a rate or timeline. Never sends the proposal to the
  client — always a draft for the owner to review and deliver themselves.
---

# Proposal Builder

## Why this exists

A proposal that gets signed does three things: proves the person listened, makes the scope
unambiguous, and prices it in a way the owner can actually deliver on. A proposal built from vague
notes and a made-up number does none of those — it either underprices the work (owner eats the loss)
or overpromises the scope (owner eats the scope creep). This skill exists to turn real scope notes
into a real proposal fast, and to stop and ask when the notes aren't enough to price confidently
rather than papering over the gap with a plausible-sounding number.

## When to fire

- "Write a proposal for [client/project]"
- "Put together a quote for [scope]"
- "Draft a SOW for [client]"
- Owner pastes discovery call notes, an email thread, or a transcript and asks for a proposal

## How to do it

### Step 1 — pull scope input

Take whatever the owner has: pasted call notes, an email thread, a transcript, or a verbal
description in the conversation itself. Also check `memory/clients/[Name]/` (via `operator-prime`)
for any prior context on this client — past engagements, known preferences, pricing history — so the
proposal isn't written blind if there's already a relationship.

### Step 2 — extract the structure

Pull out, explicitly, from the input:
- **Problem/goal** — what's actually broken or wanted, in the client's own words where possible
- **Scope** — the specific deliverables, broken into discrete items, not one paragraph of prose
- **Timeline** — start date, milestones, end date, or phase breakdown
- **Constraints** — budget mentioned, deadline mentioned, tools/systems they're locked into
- **Decision maker / next step** — who signs off, what happens after they say yes

### Step 3 — the pricing check (do this before writing numbers)

Before putting a dollar figure or hours estimate anywhere in the draft, check: does the input contain
enough to price this with real confidence — a defined deliverable list, a rough timeline, and either
a stated budget or enough scope detail to size it against the owner's known rates?

**If yes** — price it, using any rate/pricing info in `memory/context/you.md` or prior proposals in
`memory/clients/` as the baseline.

**If no** — do not invent a number. Say so directly:

> "The scope notes cover [what's clear] but I don't have enough to price [specific gap — e.g., 'the
> ongoing maintenance piece' or 'how many revisions are included'] with confidence. Options: (1) I
> draft the proposal with that section marked TBD and a placeholder range, (2) you give me [the
> specific missing input] and I fill it in, (3) I draft it as a phase-1-only proposal and scope
> phase 2 separately once it's clearer."

This applies per-section — a proposal can have a confidently priced core scope and a flagged TBD
add-on in the same document. Don't block the whole proposal because one line item is fuzzy.

### Step 4 — draft

```
PROPOSAL: [Project Name] for [Client Name]
Prepared [date]

## The situation
[2-3 sentences, client's actual problem in plain language — not restated generically]

## Goals
- [Specific, stated goal 1]
- [Specific, stated goal 2]

## Scope
1. [Deliverable] — [what "done" looks like for this item]
2. [Deliverable] — [what "done" looks like for this item]
3. [Deliverable — marked TBD if pricing wasn't confident, with a note on what's needed to finalize]

## Timeline
- Kickoff: [date/trigger]
- [Milestone]: [date or week number]
- Delivery: [date]

## Investment
[Line-item or phase-based pricing, matching whatever confidence level Step 3 established]
[If anything is a placeholder range rather than a firm number, say so explicitly — never present a
guess as a firm quote]

## Next steps
1. [Specific action — e.g., "sign below" or "reply to confirm start date"]
2. [What happens immediately after]

Valid through [date].
```

Keep the tone matched to how the owner talks to clients elsewhere in the vault (journal entries,
past outreach) rather than defaulting to boilerplate legal-sounding proposal language.

## Handoff

Pull client history and pricing precedent from `memory/clients/[Name]/` before drafting (via
`operator-prime`). After the proposal is finalized, save it to the client's folder and log the
decision — what was proposed, at what price, sent when — to `journal/YYYY-MM-DD.md` and add a
follow-up task ("check on [Client] proposal") to `TASKS.md`, via the `capture-everything` pattern.

## What this skill does not do

- Never invents a price, hours estimate, or timeline when the input doesn't support one — flags the
  gap and asks instead
- Never sends the proposal to the client — output is a draft for the owner to review and deliver
- Never pads scope with generic filler items to make a proposal look more substantial than the
  actual discussed work
