---
name: lead-triage
description: >
  Ranks a pipeline of leads by fit, engagement, and urgency into a short, callable list with a
  specific talking point per lead. Use when the owner asks "who should I call today," "prioritize my
  pipeline," "which leads are hot," or pastes a CRM export / spreadsheet / list of new leads and asks
  what to do with them. Works from whatever the owner provides — a CSV export, a copied CRM view, or
  a plain description of each lead — no CRM connector required. If a CRM connector (HubSpot,
  Pipedrive, etc.) is available, pull the live list directly; otherwise ask the owner to paste or
  describe it. Never contacts a lead directly — output is a ranked list for the owner to work from.
---

# Lead Triage

## Why this exists

Most solopreneurs don't lack leads, they lack a next action. A spreadsheet of 40 names with no
ranking is not a to-do list, it's a wall of guilt. This skill turns a raw pipeline into a short list
of who to call today, in what order, and what to say when they pick up. The output is useless if it's
just a ranking with no reasoning attached — a name and a score tells the owner nothing they can act
on. Every lead on the list gets a reason and a talking point.

## When to fire

- "Who should I call today"
- "Prioritize my pipeline" / "what leads are hot"
- Owner pastes a CRM export, spreadsheet, or list of new leads
- Owner describes a batch of leads verbally ("I've got Jenna from the trade show, two people who
  filled out the contact form, and a referral from Mike")
- Start-of-day or start-of-week planning where pipeline exists

## Inputs it needs

At minimum, one line per lead with whatever the owner has:
- Name, company (if B2B)
- How they came in (referral, inbound form, trade show, cold list, past client)
- Last contact date and what was said, if any
- Any stated budget, timeline, or urgency signal
- Deal size or estimated value, if known

If a CRM connector is available, pull this directly instead of asking the owner to retype it. If not,
ask for a CSV/export paste, or let the owner describe leads in plain language — don't block on
structured data. Missing fields are fine; score with what exists and flag what's missing.

## How to score

Score each lead on three axes, 1–3 each (9 possible, not a fake precision score out of 100):

1. **Fit** — does this lead actually match who the owner sells to (right size, right problem, right
   budget range)? A referral from a bad-fit prior client still scores low here.
2. **Engagement** — have they taken a real action (replied, booked a call, opened three emails,
   asked a follow-up question) vs. gone cold (form fill with no follow-up, one unanswered email)?
3. **Urgency** — is there a stated or implied deadline (contract renewal, event date, budget cycle,
   explicit "need this by")? No signal = 1, not 0.

Total score sorts the list. Ties break toward whichever lead has a clearer, more specific talking
point available — a lead you can say something concrete to beats a lead you'd have to open with
"just checking in."

## Output format

A ranked call list, capped at what's actually callable in a day (default 5–8, ask if the owner wants
more). Each entry:

```
1. Jenna Ruiz — Ruiz & Co (score 8/9: fit 3, engagement 3, urgency 2)
   Why now: Replied to the pricing email Tuesday asking about a start date. Trade show lead, referred by
   name recognition of [[Case Study Client]].
   Talking point: Reference the trade show conversation about their Q3 hiring push — ask if the
   timeline she mentioned (before Labor Day) is still live. That's the urgency lever, not price.

2. Mike Torres — cold list, no prior contact (score 4/9: fit 2, engagement 1, urgency 1)
   Why lower: No engagement yet, fit is a guess based on industry alone. Still worth a call, just not
   today's first one.
   Talking point: Open with the specific problem the owner's ICP has, not a generic intro — this is a
   cold call, treat it like one.

...

Not on today's list (n leads): dead/unresponsive after 3+ touches, or fit score of 1 with no
countervailing urgency. Listed separately below so nothing silently disappears from the pipeline.
```

Always include the "not on today's list" section — a triage tool that quietly drops leads erodes
trust fast. Show what got deprioritized and why.

## Handoff

Pull lead/client context from `memory/clients/` and prior mentions in `journal/` before scoring —
don't triage blind if the owner already has history with someone on the list (via the `operator-prime`
pattern). After producing the list, write it back: today's ranked list and any new facts about
leads (a stated budget, a new deadline, a status change) go to `journal/YYYY-MM-DD.md` and, for
leads that become named contacts worth tracking, `memory/clients/` — via the `capture-everything`
pattern. Add "call [lead]" items to `TASKS.md` if the owner wants them tracked as discrete tasks
rather than just a list in the journal.

## What this skill does not do

- Does not call, email, or text anyone — it produces a list for the owner to work from
- Does not invent engagement signals that weren't provided or pulled from a connector
- Does not assign a false-precision score (87/100) when the owner gave three data points
