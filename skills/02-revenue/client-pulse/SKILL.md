---
name: client-pulse
description: >
  Synthesizes sentiment and recurring themes from pasted emails, reviews, support tickets, or notes
  into a short list of concrete, fixable issues — each backed by a real quote, not a vague sentiment
  score. Use when the owner asks "how are my clients feeling," pastes reviews/complaints/feedback and
  asks for a read on it, or says "check in on relationships." Works from whatever's pasted or
  described — review site exports, email threads, support tickets, or a verbal summary of recent
  client interactions. If a review-platform or helpdesk connector is available, pull recent feedback
  directly; otherwise ask the owner to paste or describe it. Output is a same-week action list, not a
  dashboard — every finding maps to something the owner can actually do.
---

# Client Pulse

## Why this exists

"Sentiment is 7.2/10, trending down" tells the owner nothing they can act on. What they need is: this
specific client said this specific thing, three other clients are hinting at the same issue, and
here's what to do about it this week. This skill exists to turn a pile of unread feedback — reviews,
emails, tickets, offhand comments — into a short list of real, fixable problems, each one anchored to
an actual quote so the owner can verify it's not a hallucinated pattern.

## When to fire

- "How are my clients feeling"
- Owner pastes reviews, complaints, support tickets, or feedback and asks for a read
- "Check in on relationships" / "how's [client] doing"
- Before a renewal, QBR, or check-in call where the owner wants to walk in informed

## How to do it

### Step 1 — gather input

Take whatever the owner has:
- Pasted reviews (Google, Yelp, industry-specific platforms)
- Email threads, especially anything with a complaint, hesitation, or lukewarm response
- Support/ticket exports
- A verbal rundown ("Client X seemed off on the last call, Client Y mentioned pricing twice")

If a review-platform or helpdesk connector is available, pull recent items directly. Otherwise ask:
"Paste what you've got — reviews, emails, ticket exports, whatever — or just tell me what's stuck
in your head from recent conversations." Also check `memory/clients/` and `journal/` (via
`operator-prime`) for prior mentions of friction with the same clients — a one-off comment last
month plus a similar comment this week is a pattern, not two isolated data points.

### Step 2 — extract, don't summarize

For each piece of input, pull the actual language used, not a paraphrase. "Client seemed unhappy
about turnaround" loses the real signal. "Client wrote: 'this is the second time we've had to chase
you for an update'" is the real signal — keep the quote.

### Step 3 — cluster into themes

Group individual comments/quotes into 3–6 recurring themes (not more — if everything is a theme,
nothing is prioritized). A theme needs at least one direct quote to back it; a single vague
impression with no quote gets flagged as "worth watching" separately, not promoted to a numbered
finding.

### Step 4 — rank by fixability and stakes this week

Order findings by: how fixable is this in the next 7 days, and how much revenue/relationship risk
does it carry if ignored. A minor annoyance mentioned by one client ranks below a recurring
communication gap mentioned by three, even if the recurring one feels less dramatic.

### Step 5 — output format

```
CLIENT PULSE — [date]
Based on: [n] reviews, [n] email threads, [n] tickets/notes

1. Response time is the top complaint (3 mentions, all in the last 3 weeks)
   - [[Client A]]: "second time we've had to chase you for an update"
   - [[Client B]] (review, 3 stars): "great work once it happens, just slow to hear back"
   - Journal, 2026-06-28: noted [[Client C]] seemed frustrated on the call about timing
   Fix this week: [specific, doable action — e.g., "send a standing Friday status update to active
   clients, even a one-liner, before they have to ask"]

2. Pricing pushback is emerging but isolated (1 direct mention)
   - [[Client D]]: "wanted to check if there's flexibility on the renewal rate"
   Worth watching, not urgent: one data point isn't a pattern yet — track if it recurs before
   changing pricing strategy.

3. [Positive theme worth reinforcing, if one exists]
   - Two clients independently praised [specific thing] — worth doubling down on / mentioning in
     marketing, not just noting and moving on.

Not enough signal yet: [any vague impressions without a backing quote — named so they're not lost,
but not treated as confirmed findings]
```

Always separate confirmed findings (backed by a quote) from things worth watching (a hunch, one
ambiguous comment) — collapsing the two into one list is exactly the vague-sentiment-score problem
this skill exists to avoid.

## Handoff

Pull prior client history via `operator-prime` (memory/clients/, journal/) so today's pulse check
connects to past friction instead of treating every session as a blank slate. After producing the
findings, write back: update the relevant `memory/clients/[Name]/` file with any new friction point
or praise, log the pulse-check summary in `journal/YYYY-MM-DD.md`, and add the "fix this week" items
to `TASKS.md` as discrete action items — via the `capture-everything` pattern.

## What this skill does not do

- Never produces a single sentiment score or trend line with no supporting quotes
- Never contacts a client directly — findings and any follow-up messages are for the owner to act on
- Never inflates a single ambiguous comment into a "theme" — themes need multiple data points or get
  labeled as unconfirmed
