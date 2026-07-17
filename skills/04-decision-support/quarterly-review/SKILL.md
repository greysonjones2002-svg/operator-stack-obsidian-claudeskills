---
name: quarterly-review
description: >
  Pulls together revenue/margin trend, customer health signals, and wins/risks from the vault's
  journal and client files across the quarter into a prioritized "what to focus on next quarter"
  review — not just a numbers recap. Explicitly invokes pattern-radar to surface recurring themes
  before writing the final prioritized list. Use when the owner asks "how's the quarter going,"
  wants a QBR, asks "where do I stand," or it's the end of a calendar quarter and a review hasn't
  been done yet. This is decision SUPPORT — it synthesizes what happened and surfaces patterns, it
  does not hand the owner a strategy or tell them what to prioritize without their input. Ends with
  a prioritized list framed as "here's what the data points to," open for the owner to reorder or
  reject, not a locked directive.
---

# Quarterly Review — Trend Synthesis & Next-Quarter Focus

## Why this exists

Solopreneurs run day to day and rarely step back far enough to see the shape of a whole quarter —
which clients are actually healthy, which numbers are trending the wrong way, which problem keeps
showing up in the journal without ever getting fixed. This skill exists to do that stepping-back:
pull three months of scattered notes, numbers, and client status into one place and surface what
the pattern actually is, not just what happened most recently (recency bias is the main failure
mode a solo operator has when self-assessing).

## The rule that overrides everything else in this file

**This skill ends with a prioritized list the owner can reorder or reject — not a locked
directive.** "Based on the trend, X shows up as the highest-leverage focus" is fine. "Your top
priority next quarter is X, full stop" is not this skill's call — the owner may have context
(personal capacity, a deal in motion, a reason to deprioritize something that looks urgent on
paper) that the vault doesn't capture. Frame the output as "here's what the data points to,"
explicitly invite pushback, and don't treat silence as agreement — ask.

## When to fire

- "How's the quarter going?"
- "Can we do a QBR?"
- "Where do I stand?"
- End of a calendar quarter (late Mar/Jun/Sep/Dec) if no review has been logged yet for that period
  — check `journal/` for a prior quarterly-review entry before assuming one is overdue

## How to do it

### Step 1 — gather the quarter's material

This is a multi-file pull, not a couple of reads. Scan:

- `journal/` — every entry across the quarter's date range, not just the most recent few. Look for
  decisions made, client status changes, recurring frustrations, wins mentioned in passing
- `memory/clients/` — every client file touched or updated during the quarter; check status,
  contract terms, any noted friction
- `memory/context/you.md` (or the owner's equivalent business-context file) — for stated goals this
  quarter was supposed to move toward, so the review measures against something real, not a
  generic template
- `TASKS.md` — what got done vs. what's been sitting since early in the quarter (a task open the
  whole quarter is itself a signal)

If the quarter spans a lot of journal entries, this is squarely a sub-agent job — don't do a
shallow skim and call it a quarter review. Dispatch comprehensive reads across the full date range
rather than sampling the entries that happen to be memorable.

### Step 2 — build the trend picture

From what's gathered, assemble (using only figures the owner has actually recorded — don't
estimate a number that isn't in the vault):

- **Revenue/margin trend** — month over month if the data supports it, otherwise quarter-over-
  quarter vs. the prior quarter if that's on file. State clearly if only partial data exists —
  "two of three months have revenue figures logged, third is missing" is more useful than
  papering over the gap.
- **Customer health signals** — which clients look stable, which show friction (late payments,
  scope disputes, communication gaps, explicit dissatisfaction noted in the journal), which grew
  or shrank in scope
- **Wins** — completed deals, resolved problems, positive client feedback, anything worth
  recording as a win even if it wasn't framed as one at the time
- **Risks** — anything flagged during the quarter that's still open: a client concentration issue,
  a recurring complaint, a task that kept getting pushed

### Step 3 — invoke pattern-radar explicitly

Before finalizing anything, run (or explicitly reference) the vault's `pattern-radar` skill against
this quarter's material specifically. The point of pattern-radar here is to catch what a single
read-through misses: the same vendor complaint showing up in four different journal entries three
weeks apart, a client's payment timing quietly drifting later each month, a type of project that
keeps taking longer than quoted. These recurring-theme patterns are usually more decision-relevant
than any single quarter's headline number, because they're the things likely to keep costing time
or money into next quarter if unaddressed.

If `pattern-radar` isn't available as an invokable skill in this installation, do its job manually:
explicitly re-scan the gathered material a second time looking only for repetition — the same
issue, vendor, or client name appearing more than once across separate entries — rather than
treating each entry as a standalone data point.

### Step 4 — write the review

Structure:

```
QUARTERLY REVIEW — [Quarter, Year]

REVENUE & MARGIN TREND
[what the numbers show, with the actual figures, and an honest note on data completeness]

CUSTOMER HEALTH
Stable: [clients, brief why]
Friction: [clients, specific issue, not vague "some tension"]
Grown/shrunk: [any scope changes]

WINS
[specific, dated where possible]

RISKS (open, unresolved as of quarter end)
[specific, ideally with severity/likelihood — risk-scan can go deeper on this if needed]

RECURRING PATTERNS (via pattern-radar)
[the repeated theme(s) found — this is often the most useful section, don't bury it]

SUGGESTED FOCUS FOR NEXT QUARTER
[prioritized list, each tied explicitly to evidence above — "this ranks first because X pattern
cost roughly Y hours/dollars across the quarter," not an unsupported ranking]
```

### Step 5 — the prioritized list is a proposal, not an assignment

When presenting the "suggested focus" section, say explicitly: "This ranking comes from what
showed up most in the data — it's not weighing things you might know that aren't written down,
like an upcoming personal constraint or a deal already in motion that changes the calculus. Does
this match how you'd rank it, or is something missing?" Then actually wait for the answer before
treating the list as final — don't proceed to write it into `TASKS.md` as settled priorities
without that check.

### Step 6 — write back

- `journal/YYYY-MM-DD.md` — log that the quarterly review was run and link/summarize the findings,
  so "did we already do Q2's review" has an answer next time
- `TASKS.md` — once the owner confirms or adjusts the priority list, add the confirmed items as
  actual tasks, not before
- If client health issues surfaced, update the relevant `memory/clients/[Name]/` file with the
  specific concern — this is a reactive update per `capture-everything` since the review is
  surfacing a new read on existing facts
- If a genuinely new pattern was found (not previously documented), that's worth its own note in
  wherever the vault tracks recurring operational patterns, so next quarter's pattern-radar pass
  starts from a documented baseline instead of rediscovering it from scratch

## Worked example

**Owner:** "Can you give me a QBR for Q2?"

**After gathering journal entries April-June, client files, and TASKS.md:**

```
QUARTERLY REVIEW — Q2 2026

REVENUE & MARGIN TREND
April: $14,200 logged. May: $16,800 logged. June: not explicitly logged in journal — estimate
skipped per no-invention rule; flagging as a gap to close for Q3 tracking.

CUSTOMER HEALTH
Stable: [[Client A]] — on-time payment each month, no friction noted.
Friction: [[Client B]] — journal notes late payment in April AND May (this is the second
consecutive month, not a one-off).
Grown: [[Client C]] — scope expanded mid-May per journal entry, no updated contract terms found
on file — worth confirming that's intentional and documented.

WINS
- Closed [[Client D]] in April, first month at full retainer by May.
- Resolved a recurring email/plugin conflict noted three times in April journal entries — appears
fixed as of May 2nd entry, no further mentions since.

RISKS (open)
- [[Client B]] payment timing — two consecutive late months is a pattern, not a fluke.
- June revenue not tracked — can't assess Q2 close accurately without it.

RECURRING PATTERNS (via pattern-radar)
- [[Client B]] mentioned in 5 separate journal entries across the quarter, 4 of them about
payment timing specifically — this is the single most-repeated theme in the quarter's notes.

SUGGESTED FOCUS FOR NEXT QUARTER
1. Resolve [[Client B]] payment timing directly — two consecutive late months plus the journal
pattern suggests this won't self-correct.
2. Close the June revenue tracking gap before Q3 ends, so Q3's review isn't missing a month too.
3. Confirm [[Client C]]'s scope expansion is reflected in updated contract terms.

This ranking is based on what showed up most in the data — you'd know better than the journal
whether Client B's payment issue is actually urgent or just an annoyance you're already handling.
Does this match your read, or should something move?
```
