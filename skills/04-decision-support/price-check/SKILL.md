---
name: price-check
description: >
  Margin and pricing analysis from figures the owner provides directly — builds a per-product or
  per-service margin breakdown and models 2-3 pricing scenarios (current, +10%, +20%, or whatever
  the owner wants tested) with the math shown plainly. Use when the owner asks "should I raise
  prices," "am I charging enough," "what's my margin on X," "can I afford to discount this," or
  brings in cost/revenue numbers and wants to know if pricing makes sense. Also triggers on "what
  happens if I raise prices 10%" or similar what-if framing. This is decision SUPPORT — it lays out
  the math and the tradeoff, it does not pick a number for the owner. Never output a recommended
  price. Requires the owner to supply real cost and revenue figures; does not estimate or invent
  numbers that weren't given.
---

# Price Check — Margin Breakdown & Pricing Scenarios

## Why this exists

Most solopreneurs set a price once, out of instinct or by copying a competitor, and never revisit
the math. Costs creep up. Time-per-job changes. A service that was profitable at launch quietly
stops being worth doing. This skill exists to put the actual numbers in front of the owner so the
pricing question gets answered with math instead of vibes — and then gets out of the way, because
the number the owner picks is a business decision only they can own.

## The rule that overrides everything else in this file

**This skill never says "raise your price to $X" or "you should charge more."** It builds the
breakdown, models the scenarios, states the tradeoff plainly, and stops. If the owner pushes for a
direct recommendation ("just tell me what to charge"), say so directly: this tool shows you the
math, the call is yours, because you know things about your market, your relationships, and your
risk tolerance that aren't in these numbers. Then hand back the breakdown and ask what's missing
from their side of the decision.

## When to fire

- "Should I raise my prices?"
- "Am I charging enough for [service]?"
- "What's my margin on [product]?"
- "Can I afford to discount this for a client?"
- "What happens if I raise prices 10%?"
- Owner pastes in cost/revenue numbers unprompted and seems to be fishing for a pricing read

## What this skill needs from the owner

Ask for these if not already provided — don't guess or backfill with assumptions:

- **Revenue per unit/job/service tier** — current price charged
- **Direct costs per unit** — materials, subcontractor pay, platform fees, whatever scales with
  volume
- **Volume** — units/jobs/clients per month or year, recent enough to be current
- **Fixed or semi-fixed costs** to allocate, if the owner wants fully-loaded margin instead of just
  contribution margin (ask which they want — contribution margin is simpler and usually enough for
  a first pass)
- **Time cost**, if the offer is service-based and margin needs to account for the owner's or a
  contractor's hours, not just cash costs

If any of these are missing, ask. Do not fill gaps with industry averages or assumptions — a
margin number built on a guess is worse than no margin number, because it looks precise and isn't.

## How to do it

### Step 1 — build the margin-by-product/service breakdown

For each product/service the owner names, lay out:

```
[Service/Product name]
  Price:              $X
  Direct cost:         $Y
  Contribution margin: $X - $Y = $Z  (Z/X = __%)
  Volume (last period): N units
  Total contribution:   $Z × N
```

Do this for every line the owner gives figures for. If the owner only gives one, do one — don't
pad it out with placeholder categories.

### Step 2 — model 2-3 pricing scenarios

Default to three: current price, +10%, +20%. Adjust to whatever the owner asks for instead (e.g.
"what if I dropped it 15% to win more volume" is a valid scenario too — this isn't only for
increases).

For each scenario, show:

```
Scenario: +10% ($X → $X × 1.10 = $X')
  New contribution margin per unit: $X' - $Y = $Z'
  Margin % change: __% → __%
  Revenue at CURRENT volume (no demand change): $X' × N
  Revenue if volume drops 5%:  $X' × (N × 0.95)
  Revenue if volume drops 10%: $X' × (N × 0.90)
  Revenue if volume drops 20%: $X' × (N × 0.80)
```

**On the volume-drop number specifically — this is the part most tools get wrong.** Price
increases do correlate with some volume drop historically, but the size of that drop depends
entirely on the specific market, how price-sensitive the customer base is, and how differentiated
the offer is. Do not invent a specific "expect a 12% drop" figure — there's no way to know that
without the owner's own price-elasticity data (a past price change and what happened to volume
afterward, or real market research). Instead:

- Show a **range of volume-drop scenarios** (0%, 5%, 10%, 20% is a reasonable default spread) so
  the owner can see how sensitive the outcome is to an assumption they get to make, not one you
  made for them.
- If the owner HAS real data — "last time I raised prices 8% I lost 3 clients out of 40" — use
  that data specifically and say so ("based on your 2024 increase, a similar elasticity would put
  the drop around X%"). Real data beats a generic range every time; use it when it exists.
- If no data exists, say plainly: "I don't have a real number for how much volume you'd lose — no
  one does without your own elasticity data or a market test. Here's the range so you can see how
  much the outcome depends on that unknown."

### Step 3 — lay out the tradeoff, not the answer

Close with a plain-language summary of what's actually being traded off — not a pick:

```
At +10%: margin per unit improves from __% to __%. Breakeven volume drop (the point where
higher price stops paying for lower volume) is approximately __%. If you believe you'd lose
fewer clients than that, the increase pays off on paper. If you think you'd lose more, it
doesn't. That belief is the actual decision — this doesn't know your customers' price
sensitivity, you do.
```

Calculate the breakeven volume-drop threshold explicitly (the % volume drop at which new-price
revenue equals old-price revenue) — that's the single most useful number in this analysis, because
it turns "should I raise prices" into "do I believe I'd lose more or less than X% of volume,"
which the owner can actually answer from what they know about their customers.

### Step 4 — write back

Per the foundation layer: if this was a real pricing review (not a quick hypothetical), log it.

- `journal/YYYY-MM-DD.md` — note that a price check was run, on what, and the scenarios modeled
  (not the numbers if they're sensitive, but the fact that the analysis happened and what was
  decided, if anything was decided)
- If the owner makes a decision on the spot ("okay, I'm raising the consult fee to $X"), that's a
  reactive fact — capture it per `capture-everything`: journal decision log, and update whatever
  file tracks pricing (a services/offers note, if one exists) with the new number and effective
  date
- `TASKS.md` — if the owner says "let me think about it," add a follow-up task with a date, not an
  open-ended one

## Worked example

**Owner input:** "I charge $150/hr for consulting. I do about 80 billable hours a month. My only
real direct cost is a $40/month software subscription plus about $8/hr in travel/materials I don't
bill separately. Should I go to $165?"

**Breakdown:**
```
Consulting (current)
  Price:               $150/hr
  Direct cost:          $8/hr (travel/materials) + $40/mo fixed (software, ~$0.50/hr at 80hrs)
  Contribution margin:  $150 - $8.50 = $141.50/hr (94.3%)
  Volume:               80 hrs/month
  Total contribution:   $11,320/month
```

**Scenario: $150 → $165 (+10%)**
```
New contribution margin: $165 - $8.50 = $156.50/hr (94.8%)
Revenue at current volume (80 hrs, no drop):        $13,200
Revenue if volume drops 5%  (76 hrs):                $12,540
Revenue if volume drops 10% (72 hrs):                $11,952
Revenue if volume drops 20% (64 hrs):                $10,624
Breakeven volume drop (revenue = current $12,000):   ~9.1% (73 hrs)
```

**Summary given to owner:**
"At $165/hr you break even on total revenue if you lose roughly 9% of your billable hours or
less — call it 7 hours a month out of 80. Anything less than that drop and you come out ahead in
raw revenue, on top of the margin already being slightly better per hour. I don't have data on
whether your clients would actually push back at $165 — you know that market better than any
model does. The one thing worth flagging: this is total revenue, not total profit; since your
direct costs barely move, the real profit picture actually looks slightly better than the revenue
numbers alone. The call is yours."

No price recommended. Data and threshold handed over, decision left with the owner.
