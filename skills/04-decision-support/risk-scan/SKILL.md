---
name: risk-scan
description: >
  Builds a risk register covering vendor dependency, contract/liability exposure, cash
  concentration (one client too large a share of revenue), and key-person risk (what breaks if the
  owner is out for a month) — rated by likelihood and impact, with the highest-priority risks
  flagged plainly rather than buried in a long list. Use when the owner asks "what could go wrong,"
  "am I exposed," "what's my risk here," or wants a periodic risk review. This is decision SUPPORT —
  it surfaces and rates exposure, it does not tell the owner which risks to accept or how to
  mitigate them beyond naming the tradeoff. Never output "you should drop this client" or "you need
  to hire a backup" as a directive — name the exposure and let the owner decide what to do about it.
---

# Risk Scan — Risk Register & Exposure Rating

## Why this exists

Solo operators carry risk that a bigger business would spread across departments and people — one
person is sales, delivery, and finance, which means one bad month, one lost client, or one bad
vendor dependency can hit harder than it would somewhere with more redundancy. Most of that risk is
invisible day to day because it doesn't show up until it's already a crisis. This skill exists to
make it visible on purpose, before it's a crisis, by naming specific exposures instead of leaving
"what could go wrong" as a vague background worry.

## The rule that overrides everything else in this file

**This skill names the exposure and rates it — it does not decide what to do about it.** "Client X
is 55% of revenue, that's a concentration risk" is the skill's job. "You should diversify away from
Client X" or "you should fire Client X" is not — that's a business decision that trades off real
relationship value, effort, and alternatives the owner is positioned to weigh and this skill isn't.
If the owner asks "so what do I do about this," it's fine to name the general category of response
("diversification," "a written contract," "a backup vendor") without prescribing the specific move,
and to say plainly that deciding the actual response is a `go-no-go`-style call for them to make.

## When to fire

- "What could go wrong?"
- "Am I exposed?"
- "What's my risk here?"
- Periodic review requests, especially paired with `quarterly-review` — risk-scan is a natural
  companion to a QBR, not a replacement for one

## The four risk categories, always covered

Don't skip a category because nothing obvious comes to mind — a category with "no material risk
found" is a real, useful finding. Silently dropping a category because it seemed empty is how a
real risk goes unscanned.

### 1. Vendor dependency

What does the business rely on that it doesn't control? Software subscriptions critical to
delivery, a single supplier with no backup, a platform (marketplace, ad platform, hosting) the
business depends on for revenue or delivery that could change terms or access without notice.

Ask: if this vendor disappeared or changed terms tomorrow, what breaks, and how fast?

### 2. Contract/liability exposure

Pull from client contracts (check `memory/clients/` and any contracts/deliverables folders) for:
missing or weak liability caps, no clear scope boundaries (which invites scope-creep disputes),
IP ownership ambiguity, auto-renewal terms the owner might not be tracking, personal guarantee
clauses, anything that exposes the owner beyond the value of the specific engagement.

Ask: if this relationship went badly and ended in a dispute, what's the realistic downside based
on what's actually written in the contract — not what's assumed?

### 3. Cash concentration

Using whatever revenue figures the owner has recorded (don't estimate what isn't on file), work
out what share of total revenue comes from each client. Flag any client above a meaningful
threshold — 30% is a common flag point for a solo operator, but state the actual percentage rather
than just applying a label, so the owner sees the real number, not just a category.

Ask: if the largest client left tomorrow, what percentage of revenue goes with them, and how long
would it realistically take to replace?

### 4. Key-person risk

What breaks if the owner is out — sick, injured, on a trip with no signal — for a full month?
Cover: which client relationships have no other point of contact, which recurring deliverables have
no documented process a stand-in could follow, which decisions only the owner knows how to make,
whether there's any income that continues to arrive without the owner actively working (retainers
already invoiced vs. project work that stops the moment they stop).

Ask: today, with zero notice, what would a month of the owner being unreachable actually cost —
in dollars, in relationships, in things left undone?

## How to do it

### Step 1 — gather the inputs

- `memory/clients/` — for contract terms, revenue figures if tracked there, relationship notes
- `journal/` — for anything already flagged informally as a concern (a vendor complaint, a client
  getting shaky, a "need to document this process" note that never got acted on) — this overlaps
  with what `pattern-radar` would catch, and quarterly-review may have already surfaced some of it;
  check for an existing quarterly-review entry before re-deriving everything from scratch
- Direct owner input for anything not written down — key-person risk especially usually isn't
  documented anywhere and needs to be asked about directly

### Step 2 — build the register

For each identified risk:

```
RISK: [specific, named — "Client X is 55% of revenue" not "revenue concentration"]
Category: [Vendor / Contract / Cash concentration / Key-person]
Likelihood: [Low / Medium / High] — based on any real signal (has this nearly happened before?
  is there a specific reason to think it's more likely soon?), not a default guess
Impact: [Low / Medium / High] — in concrete terms where possible (dollars, days of disruption)
Evidence: [what in the vault or owner's answer supports this rating]
```

Rate likelihood and impact independently — a low-likelihood, high-impact risk (e.g., a rare but
catastrophic contract exposure) needs different attention than a high-likelihood, low-impact one
(e.g., a minor vendor price increase), and collapsing them into one score hides that difference.

### Step 3 — flag the highest-priority risks plainly, don't bury them

After the full register is built, pull the High/High and High-impact items into a short "flagged"
section at the top, not just at the end of a long list the owner has to read through to find. The
whole point of this skill is that the important risk doesn't get lost in the register — don't
undercut that by making the owner dig for it.

```
FLAGGED — HIGHEST PRIORITY
1. [Risk] — [one line on why this ranks above the rest]
2. [Risk] — [one line]

FULL REGISTER
[everything, organized by category, including Low/Low items — they belong on record even if
they're not urgent]
```

### Step 4 — name the risk, not the fix

For flagged items, it's fine to note the general shape of a response without prescribing it: "this
is the kind of exposure that's usually addressed with [a written scope-change clause / a documented
backup contact / spreading revenue across more clients] — which of those, if any, makes sense for
you is a separate call." Do not say "you should do X" as the ending. If the owner wants to work
through what to actually do about a specific flagged risk, that's a `go-no-go`-shaped follow-up
conversation, not something to resolve inline in the scan itself.

### Step 5 — write back

- `journal/YYYY-MM-DD.md` — log that a risk scan was run and the flagged items, so risk exposure
  has a paper trail over time (did the Client X concentration get worse or better since last scan)
- `TASKS.md` — if the owner wants to act on a flagged risk, add the task once they've said what
  they want to do — don't pre-populate tasks based on the skill's own suggestion before the owner
  has actually decided
- Update `memory/clients/[Name]/` if a contract-related exposure was found that should be visible
  next time that client file is opened

## Worked example

**Owner:** "Been meaning to do a risk check, been heads-down on delivery for months."

**After gathering client files and journal:**

```
FLAGGED — HIGHEST PRIORITY
1. Cash concentration — [[Client B]] is 58% of tracked Q2 revenue ($9,800 of $16,800). Likelihood:
   High (client relationships end for reasons outside your control eventually). Impact: High
   (losing this client would cut revenue by more than half with no immediate replacement in the
   pipeline based on current TASKS.md).
2. Key-person risk — no other point of contact exists for [[Client A]] or [[Client B]]; both
   relationships run entirely through you with no documented handoff process. Likelihood: Medium
   (illness/emergency is not rare over a year). Impact: High (a month unreachable would likely
   mean missed deliverables on both, given no backup process exists).

FULL REGISTER
VENDOR: [project management tool] — single point of failure for scheduling, no backup process
documented. Likelihood: Low. Impact: Medium.
CONTRACT: [[Client B]] contract has no liability cap found in the file — worth confirming this is
intentional. Likelihood: Low. Impact: Medium-High if a dispute ever occurred.
CASH: see flagged item above.
KEY-PERSON: see flagged item above. Also — retainer clients ([[Client A]]) continue billing during
a short absence; project-based work ([[Client C]]) does not, meaning a month out costs more than
the retainer-only clients would suggest.

These are named and rated, not prescribed — whether Client B's concentration is worth addressing
by diversifying, formalizing more protection in the contract, or just consciously accepting given
the relationship, is your call. Happy to work through options if you want to think through a
specific one of these.
```
