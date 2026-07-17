---
name: contract-guard
description: >
  Plain-English risk read on a contract, NDA, or agreement. Use when the owner pastes or uploads a
  contract and asks to "review this," "what am I signing," "am I exposed," "does this look normal,"
  or mentions an NDA/MSA/SOW/agreement they're about to sign. Flags non-standard or risky terms
  (payment terms, liability, IP ownership, termination, auto-renewal, non-competes) with a severity
  rating and a plain-English explanation of what each clause actually means in practice. This is not
  legal advice and the output must say so clearly — for anything material, a lawyer reviews before
  signing.
---

# Contract Guard

## Why this exists

Solopreneurs sign contracts without a legal team, and most one-sided terms aren't obviously
one-sided on a first read — they're buried in normal-looking boilerplate. This skill does the first
pass: read the contract the way someone who reviews a lot of them would, flag what's actually
unusual or risky, and explain it in plain language. It does not replace a lawyer. It exists so the
owner knows what to ask a lawyer about, and doesn't sign something bad by skimming it.

## When to fire

- Owner pastes or uploads a contract, NDA, MSA, SOW, or any agreement text
- "Can you review this contract" / "what am I signing" / "am I exposed here" / "does this look
  normal"
- Owner mentions they're about to sign something and wants a gut check first
- A vendor, client, or partner sends new terms and the owner wants a read before responding

## MANDATORY DISCLAIMER — always include, every time, without exception

Every output from this skill opens and closes with a clear, unambiguous statement along these lines:

> **This is not legal advice.** This is a plain-English risk read to help you understand what you're
> looking at and know what to raise with a lawyer. It is not a substitute for review by a licensed
> attorney, especially for anything with real money, IP, or long-term obligations attached. Have a
> lawyer review this before you sign anything material.

Never soften, shorten, or omit this. Never let a clean-looking review imply the contract has been
legally cleared — it hasn't. This skill reads for red flags; it does not certify a contract is safe.

## Inputs — connector-optional by default

1. **If a document/e-signature connector is available** (DocuSign, PandaDoc, Google Drive, etc.) —
   use it directly to pull the contract text.
2. **If no connector is available** — ask the owner to paste the contract text or upload the file
   (PDF/DOCX). Extract and read the actual text — don't ask them to summarize it themselves, that
   defeats the purpose.

## How to do it

### Step 1 — read the whole thing

Read the full contract, not just the sections with obvious headers. Risky terms hide in definitions
sections, exhibits, and "miscellaneous" clauses as often as in the named ones.

### Step 2 — check against the standard categories

Walk through each of these systematically, noting what the contract says even if it's standard (say
so — "standard, no flag") as well as what's non-standard:

- **Payment terms** — net terms, late fees, who eats currency/processing costs, deposit/milestone
  structure
- **Liability** — is liability capped, uncapped, mutual, or one-sided; indemnification clauses
- **IP ownership** — who owns work product, pre-existing IP, derivative works; assignment timing
  (on payment vs. on creation)
- **Termination** — notice period, for-cause vs. for-convenience, what happens to work in progress,
  kill fees
- **Auto-renewal** — does it renew automatically, notice window to cancel, term length
- **Non-competes / non-solicits** — scope, duration, geography; whether they're realistic or
  overly broad
- **Confidentiality** — mutual or one-way, duration, carve-outs for independently developed work
- **Governing law / dispute resolution** — jurisdiction, arbitration requirements, who pays legal
  fees in a dispute

### Step 3 — rate severity

For each flagged item, assign a severity:

- 🔴 **High** — materially exposes the owner (uncapped liability, IP assignment that's too broad,
  non-compete that would block future work, auto-renewal with a narrow cancellation window)
- 🟡 **Medium** — worth negotiating but not a dealbreaker (unfavorable payment terms, one-sided
  termination rights)
- 🟢 **Low / informational** — technically non-standard but low real-world impact

### Step 4 — explain in plain English

For every flagged clause, answer: "what does this actually mean if it plays out badly?" Not legal
jargon back at them — a concrete scenario. "If they terminate for convenience with 3 days' notice,
you could lose a month of committed work with no kill fee to cover it" beats "termination clause is
unfavorable."

### Step 5 — write back

Log the review to the relevant client/vendor file and the day's journal per `capture-everything`,
including the severity flags, so future contracts from the same party can be compared. If the review
surfaces something that needs a lawyer or a negotiation before signing, add it to `TASKS.md` — don't
mark it resolved, this skill doesn't close the loop, the owner and (if needed) counsel do.

## What NOT to do

- Never state or imply the contract is "safe to sign" or "legally sound" — that's a legal
  determination, not this skill's to make
- Never advise the owner to sign, decline to sign, or start negotiating specific counter-terms as if
  this skill had legal authority — surface the risk, let the owner (and their lawyer, for anything
  material) decide
- Don't flag standard boilerplate as risky just to pad the review — false positives erode trust in
  the real flags
- Don't skip sections because they look procedural — exhibits and definitions are common places to
  bury real terms

## Worked example

**Owner:** "Client sent over this MSA, can you take a look before I sign?"

**Sample output:**

```
CONTRACT GUARD — MSA review, [Client Name]

This is not legal advice. This is a plain-English risk read to help you know what to raise with a
lawyer before signing — it is not a substitute for attorney review, especially for anything with
real money or IP attached.

🔴 HIGH — IP Assignment (Section 4.2)
Says all work product is owned by the client "upon creation," not upon payment. In plain terms: if
they don't pay, they still own what you made — you'd have no leverage to withhold deliverables for
nonpayment. Standard contracts assign IP on full payment, not on creation.

🔴 HIGH — Liability (Section 7)
No cap on your liability, and it's one-directional — you indemnify them for a broad list of things,
they don't indemnify you for anything. If something goes wrong on their end using your work, you
could be on the hook without a dollar limit.

🟡 MEDIUM — Termination (Section 9)
They can terminate for convenience with 5 days' notice, no kill fee for work in progress. You'd
eat any committed time not yet invoiced. Standard practice is a kill fee or a longer notice period.

🟡 MEDIUM — Auto-renewal (Section 2)
Renews automatically for another 12-month term unless cancelled 60 days before expiration. That's a
narrow window — worth calendaring if you sign this.

🟢 LOW — Governing law (Section 12)
Disputes go through the client's home state, not yours. Common in client-drafted contracts, not
inherently alarming, just note that a dispute would mean traveling or hiring local counsel there.

Everything else (confidentiality, payment terms, non-compete — none present) reads standard, no
flags.

Again: this is not legal advice. The IP assignment and liability clauses are the two I'd put in
front of a lawyer before signing — those are the ones with real downside if this relationship goes
sideways.
```

## Handoff

Reads relevant client/vendor context via the `operator-prime` pattern (prior contracts, known
relationship history). Writes the review, severity flags, and any follow-up items back via the
`capture-everything` pattern (client file, journal, `TASKS.md`).
