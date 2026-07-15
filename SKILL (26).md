---
name: invoice-chase
description: >
  Drafts payment reminder messages for overdue or upcoming-due invoices, matched to how late the
  invoice is and the client's payment history. Use when the owner asks "who owes me money," "what's
  overdue," "follow up on payment," "chase invoice for [client]," or mentions a client hasn't paid.
  Also fires when reviewing accounts receivable generally. Always produces a DRAFT for the owner to
  review, edit, and send themselves — never sends, emails, or messages a client automatically. The
  owner approves every message before it goes out.
---

# Invoice Chase

## Why this exists

Chasing money is the task solopreneurs put off the longest, because every reminder feels a little
awkward and the tone is hard to calibrate — too soft and it gets ignored, too hard and it damages a
relationship worth keeping. This skill removes the friction of drafting the message, not the
judgment of sending it. It writes the right message for the situation; the owner decides if it's
right and hits send.

## When to fire

- "Who owes me money" / "what's outstanding" / "what's overdue"
- "Follow up on [client]'s invoice" / "chase payment from [client]"
- Owner mentions a client hasn't paid, or an invoice due date has passed
- Periodic accounts-receivable review (weekly/monthly check-in on outstanding invoices)

## Inputs — connector-optional by default

1. **If an invoicing or payments connector is available** (QuickBooks, Stripe, PayPal, FreshBooks,
   etc.) — use it directly to pull outstanding invoices, amounts, due dates, and payment history.
2. **If no connector is available** — ask the owner to paste or list: client name, invoice amount,
   due date, and how many times (if any) this client has been late before. A spreadsheet or CSV
   export works fine — parse it directly.
3. **Client payment history** — check `memory/clients/[ClientName]/` for prior notes on payment
   behavior (chronically late, always on time, disputes invoices, etc.) per the `operator-prime`
   pattern. This context matters more than the raw days-overdue number for setting tone.

## How to do it

### Step 1 — build the aging list

Sort every outstanding invoice by days overdue (or days until due, for upcoming ones). For each:
client name, amount, due date, days overdue, and prior late-payment count if known.

### Step 2 — assign a tier

Match tone to severity — not aggression, escalation:

| Tier | Situation | Tone |
|---|---|---|
| **Heads-up** | Due within 3 days, first time working with this client or no history of lateness | Friendly reminder, assume good faith |
| **First reminder** | 1–14 days overdue, no prior late-payment history | Warm, brief, assumes it slipped their mind |
| **Second reminder** | 15–30 days overdue, or client has been late once before | Direct, references the original due date, asks for a specific response (payment or a date) |
| **Firm** | 30+ days overdue, or client is a repeat-late-payer per their file | Clear, states the amount and days overdue plainly, asks for payment or a concrete plan, references any prior conversation about lateness if one exists |
| **Escalation flag** | 45+ days overdue, or a pattern of repeated lateness/broken promises | Don't draft an automatic message — flag to the owner that this may need a phone call, a late fee per contract terms, or a decision about continuing the relationship. This is a judgment call, not a template. |

### Step 3 — draft, don't send

Write the actual message text — email or text, matched to how the owner usually communicates with
that client if known. Include the specific amount, invoice number if available, and due date. Never
generate a subject line or message threatening legal action, collections, or service cutoff — those
are business decisions, not reminder-drafting decisions, and belong to the owner.

### Step 4 — present the batch

If chasing multiple invoices, present all drafts together, sorted by severity (most overdue first),
so the owner can review and approve/edit/skip each one in one pass rather than one at a time.

### Step 5 — write back

Log which invoices were chased and on what date to the client's file and/or the day's journal entry,
per `capture-everything`, so the next chase knows this one already went out and doesn't duplicate it.
If an invoice crosses into escalation territory, add a task to `TASKS.md` for the owner to decide on
next steps (call, late fee, hold future work).

## What NOT to do

- Never send, email, or auto-schedule a message — draft only, always
- Never draft a message that threatens legal action, reports to collections, or implies consequences
  the owner hasn't approved
- Don't default to "firm" tone just because the amount is large — tone follows days-overdue and
  history, not dollar amount
- Don't nag a client who's 2 days late with the same intensity as one who's 45 days late
- Don't invent payment history — if nothing is on file, treat the client as first-time-late and say so

## Worked example

**Owner:** "Who owes me money right now?"

**Sample output:**

```
OUTSTANDING INVOICES — as of 7/15

1. Bramwell Design — $2,400 — due 7/1 — 14 DAYS OVERDUE — no prior late history
   Tier: First reminder

   Draft:
   Subject: Quick check on invoice #114
   Hi Sam — hope things are good on your end. Just noticed invoice #114 ($2,400, due 7/1) is still
   showing open on my side. If it already went out, no worries, ignore this. Otherwise let me know
   if you need anything from me to get it processed. Thanks!

2. Okafor Retail — $1,150 — due 6/10 — 35 DAYS OVERDUE — late twice before (per client file)
   Tier: Firm

   Draft:
   Subject: Invoice #109 — $1,150, now 35 days past due
   Hi Priya — invoice #109 for $1,150 was due 6/10 and is now over a month outstanding. Can you
   confirm when I can expect payment, or let me know if there's an issue with the invoice itself?
   Happy to hop on a call if that's easier.

3. Delacroix Studio — $4,800 — due 5/28 — 48 DAYS OVERDUE — pattern of broken payment promises
   Tier: ESCALATION FLAG — not drafted. This is the third time this client has gone past 45 days.
   Recommend a phone call instead of another written reminder, and a decision on whether to continue
   taking new work from them. Your call.
```

## Handoff

Reads client payment history via the `operator-prime` pattern (`memory/clients/`). Writes chase
activity, dates, and any escalation flags back via the `capture-everything` pattern (client files,
journal, `TASKS.md`).
