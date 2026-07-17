---
name: competitor-radar
description: >
  Quick web-search-based competitive gut-check — pricing, messaging, and recent moves for a named
  competitor or short list of competitors. Use when the owner asks "what's [competitor] doing,"
  "how do I compare to [competitor]," "check out [competitor]'s pricing," or wants a fast read on
  where they stand against one or a few named competitors. Explicitly scoped as a quick pass, not a
  full competitive intelligence engagement — says so up front and suggests deeper research if the
  ask clearly needs more than a scan. This is decision SUPPORT — it reports what's found and where
  it's uncertain, it does not tell the owner how to respond or what to change about their own
  business. Never output "you should match their price" or "you should copy their positioning."
---

# Competitor Radar — Quick Competitive Gut-Check

## Why this exists

Solopreneurs rarely have time for formal competitive intelligence, but they do get blindsided by
"wait, when did they start doing that?" moments. This skill is built for that — a fast, named-
competitor scan using web search, done in minutes, not a research engagement. It's meant to answer
"what's going on over there" quickly enough to actually get used, not to replace real competitive
research when the stakes are high enough to warrant it.

## The rule that overrides everything else in this file

**This skill reports what it finds — it doesn't tell the owner what to do about it.** "Their
pricing dropped 15%" is a finding. "You should drop your price to match" is not this skill's job.
Lay out what changed, what it might mean, and where the read is uncertain because public
information is incomplete — then stop. If the owner asks "so should I respond to this," treat that
as a fresh question worth its own framework (`price-check` for pricing responses, `go-no-go` if
it's about a specific deal), not something to answer inline here.

## Scope — say this up front, every time

This is a quick pass: a handful of searches, current public information, maybe 10-15 minutes of
work. It is NOT:

- A full competitive intelligence engagement (multi-competitor matrix, historical trend tracking,
  win/loss analysis)
- Verified financial data (public pricing pages and marketing copy only — no revenue, funding, or
  internal figures unless publicly reported)
- A guarantee of completeness — competitors can hide pricing behind a sales call, run private
  promotions, or simply not be well-indexed online

State this plainly at the start of the output: "This is a quick scan based on public information,
not a full competitive analysis." If the owner's ask is clearly bigger than a gut-check — "I need a
full breakdown of everyone in this market before a board meeting," "map out the whole competitive
landscape" — say so directly and suggest scoping it as a proper research pass instead of forcing a
quick-scan answer to a big question.

## When to fire

- "What's [competitor] doing?"
- "How do I compare to [competitor]?"
- "Check [competitor]'s pricing"
- "What's [competitor] charging these days?"
- Owner names 2-3 competitors and wants a quick side-by-side

## How to do it

### Step 1 — confirm scope

Confirm the competitor name(s) and what the owner actually wants to know (pricing? messaging?
recent news? all three?). If they said "check on my competitors" without naming any, ask who —
don't guess at a competitor set.

### Step 2 — run the search pass

For each named competitor, search for:

- **Pricing** — current published pricing page, tiers, any visible discounting or bundling
- **Messaging** — how they describe themselves on their homepage/positioning right now (their
  actual words, not a paraphrase that loses the specifics)
- **Recent moves** — anything from the last few months: a launch, a pivot, a funding announcement,
  a notable review pattern, a personnel change, a new market they're targeting

Use web search for this — it's explicitly in scope, unlike the vault-dependent skills in this
pack. Cite what was actually found; don't fill gaps with assumptions about what a company "probably"
charges or does.

### Step 3 — lay out the findings plainly

```
COMPETITOR: [Name]
Scan date: [date] — quick pass, public info only

Pricing: [what's published, with tiers/numbers if visible; note "not published, requires sales
          contact" if that's the case — don't guess a number]
Messaging: [their current homepage/positioning language, quoted or closely paraphrased]
Recent moves: [anything notable found, with rough dates; "nothing notable found in the last
               few months" is a valid and useful finding, not a gap to fill with speculation]

Confidence: [High/Medium/Low — reflects how much was actually findable publicly, not how
             confident the write-up sounds]
```

Repeat per competitor if there's more than one. If comparing to the owner's own business, lay out
the comparison side by side rather than in separate paragraphs — but stick to differences observed,
not a scored verdict ("Competitor X is better" is not this skill's call to make).

### Step 4 — note what wasn't found, plainly

If pricing is gated behind a sales call, say that rather than estimating. If there's no visible
recent activity, say that rather than implying stagnation — "found nothing" and "confirmed nothing
changed" are different claims, and the first is the honest one for a quick scan.

### Step 5 — flag if this needs to go deeper

If the findings raise something that clearly matters more than a quick scan can settle — a
competitor's pricing model looks like it fundamentally shifted, or there's a pattern across
multiple competitors worth tracking over time — say so explicitly: "this is worth a deeper look
than a 15-minute scan gives you, especially if [the specific thing] turns out to matter for a
decision you're making soon."

### Step 6 — write back

- `journal/YYYY-MM-DD.md` — log that a competitor scan was run, on whom, and the headline findings;
  cheap to do, useful later when "didn't we check on them a few months ago" comes up
- If a competitor file already exists somewhere in the vault (a market/competitors note), update it
  with the new findings rather than leaving them stranded in the journal only
- `TASKS.md` — if the scan surfaced something that needs a follow-up decision (pricing response,
  messaging update), add the task — but the task is "decide how to respond to X," not a pre-decided
  action

## Worked example

**Owner:** "What's Acme Consulting doing with pricing lately? I feel like I haven't checked in a
while."

**Output:**
```
COMPETITOR: Acme Consulting
Scan date: 2026-07-15 — quick pass, public info only

Pricing: Published tiers on their site — "Starter" $2,500/mo, "Growth" $5,500/mo, "Enterprise"
custom/contact sales. This is a change from the flat $4,000/mo single-tier pricing they had as of
[whenever last checked, if known] — they've since split into a tiered model with a lower entry
point.

Messaging: Homepage now leads with "for growing teams, not just enterprises" — a shift toward
smaller-business positioning compared to the more enterprise-heavy language they used before.

Recent moves: Found a blog post from ~6 weeks ago announcing a new "Growth" tier aimed explicitly
at smaller clients. No other notable news (no funding announcements, no leadership changes found).

Confidence: Medium — pricing page is current and clear, but no visibility into actual discounting,
deal terms, or how many clients have moved to the new tiers.
```

"This is a quick scan, not a full competitive analysis — if the tiering shift matters for how you
think about your own pricing or positioning, that's worth its own look (price-check can help model
your side of it), but I'm not going to tell you whether to react to this. Just flagging that it
changed."
