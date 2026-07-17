---
name: day-one-setup
description: >
  First-run onboarding interview — fires automatically the very first time Claude is used in a
  freshly installed Operator Stack vault (signal: memory/context/you.md still has empty template
  fields, or the owner says "I just installed this," "help me set up," "get started," "onboard me,"
  or anything indicating a first session). Interviews the owner about their business, fills in
  memory/context/you.md, preferences.md, and glossary.md directly instead of leaving them as blank
  templates, and recommends which of the pack's skill categories matter most for their situation.
  This is the skill that turns a generic install into something that actually knows the owner from
  message one — run it before any other skill on a first session.
---

# Day-One Setup — First-Run Onboarding

## Why this exists

A skill pack that ships with empty template files is only as good as how long it takes the owner to
fill them in by hand — and most people never do, so the vault stays generic forever. This skill
closes that gap in one conversation: it interviews the owner like a sharp new hire would on day one,
then writes the answers directly into the vault so every other skill in this pack is working with
real context from the very next message, not placeholder text.

## When to fire

- The vault is freshly installed and `memory/context/you.md` still has the unfilled template
  headers with no content under them
- The owner says anything like "I just installed this," "set this up for me," "help me get
  started," "onboard me," or opens with a business question before any setup has happened
- Don't re-fire once `you.md` is filled in — check first, this is a one-time interview, not a
  recurring skill. If the owner wants to update something later, that's a normal `capture-everything`
  update, not a re-onboarding.

## How to run the interview

Keep it conversational, not a form dump. Ask in a few small batches rather than one wall of 15
questions — that's how real onboarding conversations go, and it lets the owner's answers to early
questions shape which later questions actually matter.

### Batch 1 — the basics

- What's the business, in your own words? (What do you actually do, who do you do it for?)
- Are you running this solo, or is it you plus contractors/a small team?
- How long has this been running — brand new, a couple years in, established?

### Batch 2 — how they work

- What does a typical week look like? Where does the most time actually go?
- What tools are you already using — invoicing, calendar, email, anything for tracking clients?
- Do you want Claude to draft things for your review, or are you comfortable with more being handled
  directly? (This sets the baseline for how the business-ops skills should behave — most of them
  default to draft-only regardless, but this shapes tone.)

### Batch 3 — what matters right now

- What's the actual goal right now — more revenue, more time back, getting organized, something
  else specific?
- Anything you'd explicitly never want handled without you being asked first? (Dollar thresholds,
  categories of decisions, whatever comes to mind.)
- Any words or phrases that make things sound fake/AI-generated to you, that Claude should avoid?

### Batch 4 — which parts of the pack to point them at

Based on everything above, tell them plainly which categories of this pack matter most for their
situation, rather than dumping the full 25-skill list:

- Running mostly on gut feel with no real financial visibility → lead with `01-core-ops`
  (cash-flow-pulse, invoice-chase, month-end-close)
- Actively selling/prospecting → lead with `02-revenue`
- Builds their own tools/sites/automations → point at `03-build-ship`
- Making a lot of high-stakes calls solo with no sounding board → lead with `04-decision-support`
- Doing research, competitive tracking, or wants a real second brain beyond day-to-day ops → point
  at `05-knowledge-wiki`

Everyone gets `00-foundation` — it's not optional, it's what makes the rest of the pack work.

## Where the answers go

Write directly, don't just summarize back in chat:

| What was learned | Goes to |
|---|---|
| Business description, solo/team, tenure, tools, current goal | `memory/context/you.md` |
| Draft-vs-act preference, decision thresholds, tone/formatting preference | `memory/context/preferences.md` |
| Banned words/phrases | `memory/context/preferences.md` → "Banned phrases" |
| Any shorthand, product names, or terms that came up | `memory/glossary.md` |
| Recommended skill categories for this owner | A short note at the top of `TASKS.md` or a first journal entry — whichever exists in the vault template |

Apply `frontmatter-standard` to any file touched, same as every other write in this pack.

## Closing the interview

End with a short, concrete summary, not a recap of the whole conversation:

> "Set up. I've saved your business context, your preferences, and flagged `02-revenue` and
> `04-decision-support` as the categories most worth using first given what you told me. From here
> just talk to me like you would a new operator on day two — I'll pull from what we just covered
> automatically."

## What this is not

This is not a sales pitch for the rest of the pack, and it's not a rigid intake form. If the owner
wants to skip ahead and just ask a question, answer the question and weave the setup questions in
naturally later rather than blocking them. The goal is a vault that knows the owner by the end of
the first real conversation — how that conversation gets there matters less than that it does.
