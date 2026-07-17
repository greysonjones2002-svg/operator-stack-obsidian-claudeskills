---
name: cash-flow-pulse
description: >
  On-demand cash flow forecasting from whatever numbers the owner has on hand. Use when the owner
  asks "how's my cash," "can I afford [X]," "what's my runway," "am I going to be okay this month,"
  or expresses any cash flow worry — a big purchase, a slow month, a client who hasn't paid, payroll
  coming up. Also fires when the owner pastes a bank/processor export or a rough list of income and
  expenses and asks what it means. Produces a 30/60/90-day forecast with explicit risk points, not a
  single confident number. Does not move money, does not make purchase decisions — it shows the owner
  what the numbers say and lets them decide.
---

# Cash Flow Pulse

## Why this exists

Most solopreneurs know their bank balance today. Almost none of them know their bank balance three
weeks from now. That gap is where bounced payments, missed payroll, and panic decisions happen. This
skill closes the gap: take whatever numbers exist, project them forward, and say plainly where the
tight spots are — before they're a surprise.

The forecast is a planning tool, not a prophecy. Small business cash flow is lumpy and the inputs are
usually incomplete. The output should read like a sharp operator's gut check with the math shown, not
like a bank's official balance projection.

## When to fire

- "How's my cash looking" / "how are we doing on cash"
- "Can I afford [a hire, a tool, a trip, new equipment]"
- "What's my runway"
- Any expression of cash worry — slow month, a client ghosting on payment, a big bill coming up
- Owner pastes a bank statement, processor export (Stripe/PayPal/Square), or a CSV of transactions
  and asks for a read on it
- Before a big spending decision, even if not explicitly framed as a cash question

## Inputs — connector-optional by default

This skill has no guaranteed data connection. Work from whatever the owner provides:

1. **If a connector is available** (bank, Stripe, QuickBooks, etc.) — use it directly to pull actual
   balances and transaction history. Confirm the pull date range with the owner before treating it as
   authoritative.
2. **If no connector is available** — ask for, in order of usefulness:
   - Current account balance(s) and the date
   - Recurring income (client retainers, subscriptions, expected invoice payments) with expected
     dates
   - Recurring fixed costs (rent, software, insurance, loan payments, payroll) with due dates
   - Known one-off items coming up (a big bill, a tax payment, a planned purchase)
   - A rough guess is fine — say so. "Ballpark is okay, I'll flag anywhere the forecast is sensitive
     to that number."
3. **If the owner pastes a CSV or raw statement text** — parse it directly rather than asking them to
   re-summarize it. Categorize into recurring income, recurring costs, and one-offs as you go.

Never block on missing data. Build the forecast with what exists and mark the gaps.

## How to do it

### Step 1 — pull context

Check `memory/context/you.md` and any relevant file under `memory/clients/` for known recurring
revenue (retainers, subscription clients) and known fixed costs already on record, per the
`operator-prime` pattern. Don't make the owner repeat information already captured in the vault —
use it as a starting point, then confirm it's still current.

### Step 2 — build the ledger

Lay out three columns: money in, money out, running balance. Anchor to today's actual balance if
known. Walk forward day by day or week by week (week-by-week is usually enough resolution) through
30/60/90 days, adding known inflows and outflows on their expected dates.

### Step 3 — mark confidence, not just numbers

Every line has a different certainty level. Tag them:

- **Locked** — contractual, recurring, high confidence (rent, payroll, an active retainer)
- **Likely** — expected but not guaranteed (a client invoice due on terms, not yet paid)
- **Uncertain** — rough estimate or a number the owner wasn't sure of

Never present the ending balance as a single precise figure without this context. "You'll have
$4,200 on the 30th" is false precision if half the inputs are guesses. Say instead: "Projected around
$4,000–4,500 on the 30th, assuming the Ferro invoice lands on time — that's the biggest swing
factor."

### Step 4 — find the tight points

Scan the running balance for the lowest points in the window, not just the endpoint. A month can end
fine and still have a day in the middle where the balance goes negative or dangerously low if a bill
and a gap in income line up. Call these out specifically with the date and the cause.

### Step 5 — answer the actual question

If the owner asked "can I afford X," don't just hand back a forecast — run the forecast with and
without the expense and say directly whether it's tight, comfortable, or a problem, and why.

### Step 6 — write back

Log the forecast summary and any risk points to the day's journal entry per `capture-everything`. If
this surfaces a new recurring cost or income source not already on record, update
`memory/context/you.md` or the relevant client file. If a risk point needs follow-up (chase an
invoice, delay a purchase, cut a cost), add it to `TASKS.md`.

## What NOT to do

- Don't present a forecast as certain when the underlying numbers are guesses — always show the
  confidence tier
- Don't recommend or execute a purchase, a cut, or a transfer — surface the numbers and the tight
  points, let the owner decide
- Don't silently assume a late-paying client will pay on time in the "likely" column — flag them as
  the risk they are
- Don't build a forecast so granular it becomes noise — weekly resolution beats daily for a 90-day
  window unless the owner is in a genuinely tight stretch

## Worked example

**Owner:** "Can I afford to hire a part-time VA at $1,800/month? How's my cash looking the next 60
days?"

**Sample output:**

```
CASH FLOW PULSE — as of 7/15, starting balance $6,400

Week of 7/15: +$0 in / -$1,200 out (software + insurance, LOCKED)  → ~$5,200
Week of 7/22: +$3,500 in (Ferro Consulting retainer, LOCKED) / -$400 out → ~$8,300
Week of 7/29: +$0 in / -$2,100 out (rent + loan payment, LOCKED) → ~$6,200
Week of 8/5:  +$2,800 in (Whitmore invoice, LIKELY — 15 days past terms already) / -$300 out → ~$8,700
Week of 8/12: +$0 in / -$1,200 out (software + insurance) → ~$7,500
Week of 8/19: +$3,500 in (Ferro retainer, LOCKED) / -$400 out → ~$10,600
Week of 8/26: +$0 in / -$2,100 out (rent + loan) → ~$8,500

TIGHT POINT: none below $5,000 in this window, but the whole picture leans on the Whitmore invoice
landing — that one's LIKELY, not LOCKED, and it's already late once.

VA AT $1,800/MO: adding a recurring $1,800/month cost drops every ending balance by roughly that
amount cumulative. Re-run with it in: lowest point becomes ~$3,400 in the week of 7/29, before the
Whitmore invoice would land. That's the risk window — if Whitmore slips further, that week gets
tight with the VA cost added.

READ: affordable if Whitmore pays on schedule. Worth confirming that invoice before committing to the
hire, or starting the VA at a lower hours commitment for the first month.
```

## Handoff

Reads context via the `operator-prime` pattern (recurring revenue/cost facts already on file).
Writes the forecast, risk points, and any resulting action items back via the `capture-everything`
pattern (journal, `TASKS.md`, client files).
