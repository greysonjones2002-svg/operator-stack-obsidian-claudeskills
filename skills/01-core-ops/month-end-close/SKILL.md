---
name: month-end-close
description: >
  Walks the owner through closing out the month — reconciling records against bank/processor data if
  available, flagging uncategorized or duplicate transactions, and writing a plain-English narrative
  of what actually happened financially, not just the numbers. Use when the owner says "close the
  month," "what's my P&L," "why did revenue/margin change," or when a new month has started and last
  month hasn't been closed yet. Produces a reconciliation checklist plus a short story of the month,
  not a wall of line items.
---

# Month-End Close

## Why this exists

Most solopreneurs know roughly how the month went but couldn't say precisely, and never turn "roughly"
into a real close — categorized, reconciled, and understood. That gap compounds: taxes get harder,
pricing decisions get made on vibes instead of margin data, and a bad month doesn't get caught until
it's a bad quarter. This skill exists to make closing the month a 20-minute routine instead of a
dreaded quarterly scramble, and to make the output a story the owner actually understands, not just a
spreadsheet.

## When to fire

- "Close the month" / "let's close out [month]"
- "What's my P&L" / "how did last month go financially"
- "Why did revenue/margin/profit change" — this often means a close hasn't happened and the answer is
  buried in uncategorized transactions
- A new month has started and the prior month's close is missing or incomplete
- Periodic monthly routine, if the owner has one set up

## Inputs — connector-optional by default

1. **If an accounting/banking/processor connector is available** (QuickBooks, bank feed, Stripe,
   PayPal, etc.) — use it directly to pull the month's transactions and existing categorization.
2. **If no connector is available** — ask the owner to paste or upload a bank statement export, a
   processor export (Stripe/PayPal/Square), or a spreadsheet of the month's transactions. Work from
   whatever format they have — don't require a specific tool or template.
3. **Prior month context** — check `memory/context/you.md` and relevant client files for known
   recurring revenue and costs already on record, per `operator-prime`, to compare this month against
   expectations and catch anomalies faster.

## How to do it

### Step 1 — reconcile

Compare the transaction data against what's already recorded/categorized (if anything is). For each
transaction, confirm it's accounted for once, correctly, and in the right category. Flag:

- **Uncategorized** — a transaction with no clear category assigned
- **Possible duplicates** — same amount, same or near-same date, similar description — flag for the
  owner to confirm rather than auto-merging, since legitimate repeat charges look identical to
  duplicates
- **Unusual** — a transaction that doesn't match any normal pattern for this business (unusually
  large, unfamiliar vendor, off-cycle timing)

### Step 2 — total it up

Once categorized, roll up: total revenue, total costs by category, gross margin, net for the month.
Compare against the prior month and, if available, against the same month last year.

### Step 3 — write the narrative, not just the numbers

This is the part a spreadsheet can't do. Explain what happened in plain English:

- What drove revenue up or down (a new client, a client who churned, a seasonal pattern, a one-off
  project)
- What drove costs up or down (a new tool, a one-time purchase, a price increase from a vendor)
- Whether margin moved and why (did costs grow faster than revenue, or the reverse)
- Anything that looks like it's starting a trend versus a one-off blip

Bad version: "Revenue was $18,200, down from $21,400." Good version: "Revenue dropped about $3,200
from last month — almost entirely because the Whitmore project wrapped and hasn't been replaced yet,
not because existing retainer clients pulled back. Worth watching whether that gap gets filled before
next month, since retainer revenue held steady."

### Step 4 — flag what needs a decision

Separate observations from open questions. If margin dropped because of a cost that might be
permanent (a vendor price increase) versus temporary (a one-time equipment purchase), say which is
which and flag anything that might warrant a pricing or cost decision — without making that decision.

### Step 5 — write back

Write the close summary and narrative to the day's journal entry, and update
`memory/context/you.md` or relevant tracking with the month's headline numbers, per
`capture-everything`, so next month's close has a real baseline to compare against. Add any flagged
decisions (a cost to investigate, a client gap to fill, a pricing question) to `TASKS.md`.

## What NOT to do

- Don't auto-merge or delete suspected duplicate transactions — flag and ask, some repeat charges are
  legitimate
- Don't present a categorization as final if it's a guess — say when something is your best read
  rather than a confirmed category
- Don't just hand back totals — the narrative (what happened and why) is the actual point of this
  skill, not a byproduct
- Don't make a pricing, cost-cutting, or spending decision based on the close — surface what the
  numbers suggest and let the owner decide

## Worked example

**Owner:** "Can you close out June for me? Margin feels off."

**Sample output:**

```
MONTH-END CLOSE — June

RECONCILIATION
- 3 transactions uncategorized: $340 (Adobe, 6/8), $1,200 (unfamiliar vendor "Hensley LLC", 6/19),
  $85 (recurring, likely a subscription — confirm which one)
- 1 possible duplicate: two $600 charges to "Riverside Print Co" on 6/11 and 6/12 — same amount,
  back-to-back days. Confirm if that's two separate orders or a duplicate charge.
- Everything else reconciles cleanly against the bank export.

TOTALS
- Revenue: $16,800 (May: $19,100, -12%)
- Costs: $9,400 (May: $7,600, +24%)
- Gross margin: 44% (May: 60%)

THE STORY
Margin dropped sharply this month, and it's costs, not revenue, driving most of it. Revenue slipped
modestly — about $2,300, mostly from the Kessler project finishing up with nothing yet booked to
replace it. But costs jumped $1,800, and $1,200 of that is the unfamiliar "Hensley LLC" charge that's
currently uncategorized — that single transaction accounts for more than half the cost increase.
Worth confirming what that charge actually was before drawing conclusions about margin trend; if it's
a one-time cost, June's margin drop is mostly noise. If it's the start of a recurring cost, that's a
different conversation.

FLAGGED FOR YOU
- Confirm the Hensley LLC charge — biggest lever on this month's margin read
- Confirm whether the Riverside Print duplicate is real
- Kessler project ended with nothing booked to replace it yet — worth a look at pipeline, not
  something this close can tell you, just flagging the gap
```

## Handoff

Reads prior-month baselines and business context via the `operator-prime` pattern
(`memory/context/you.md`, client files). Writes the close summary, narrative, and flagged decisions
back via the `capture-everything` pattern (journal, `memory/context/you.md`, `TASKS.md`).
