---
name: task-command
description: >
  Turns TASKS.md into a real daily/weekly prioritization system instead of a flat list. Use when the
  owner asks "what's on my plate," "what should I do today," "what should I focus on this week,"
  or wants help planning a realistic day. Surfaces what's overdue, what's due soon, and flags tasks
  that have sat untouched for 2+ weeks (stale, distinct from just old) so nothing quietly rots at the
  bottom of the list. Helps the owner commit to a realistic day or week rather than seeing everything
  at once and freezing.
---

# Task Command

## Why this exists

A task list that just grows is not a prioritization system — it's a guilt archive. Most solopreneurs
default to `TASKS.md` as a place things go to be written down and then never looked at again in any
structured way. This skill turns the file into an actual planning tool: what's urgent, what's rotting,
and what a realistic day or week looks like given everything else going on.

## When to fire

- "What's on my plate" / "what should I do today" / "what should I focus on this week"
- Morning or start-of-week planning, whether prompted by the owner or as part of a broader daily/
  weekly routine
- Owner feels overwhelmed by the list and needs it triaged down to something workable
- Periodic maintenance pass to catch tasks that have gone stale

## Inputs

This skill runs primarily off `TASKS.md` itself — no external connector is required.

1. **Primary source**: `TASKS.md` in the vault.
2. **If a task-tracking connector is available** (Todoist, Linear, etc.) — use it directly to pull
   live task state instead of, or alongside, `TASKS.md`, and reconcile the two if they diverge.
3. **Calendar context, if available** — check for known meetings/commitments that eat into available
   time for the day/week being planned. If no calendar connector exists, ask the owner directly:
   "anything on your calendar today I should plan around?"

## How to do it

### Step 1 — pull full context

Read `TASKS.md` in full, plus `memory/context/you.md` for known priorities and active work streams,
per the `operator-prime` pattern. A task's priority isn't just its own due date — it's whether it
serves something the owner has flagged as currently important.

### Step 2 — classify every open task

For each task, determine:

- **Overdue** — past its stated due date
- **Due soon** — due within the planning window (today, or this week)
- **Stale** — no due date, or a due date that's not close, but the task has sat with no update,
  progress note, or mention for 14+ days. This is a distinct flag from "old" — a task can be old and
  still active if it's been touched recently; stale means it's been abandoned, not just long-lived.
- **Active/on-track** — has a reasonable due date not yet arrived, or is clearly being worked

To determine "untouched," use whatever timestamp signal exists — last-edited date on the task line if
tracked, or the date it was last mentioned in a journal entry or session. If no timestamp exists at
all for a task, say so rather than guessing — flag it as "unknown age, worth checking."

### Step 3 — surface stale tasks explicitly

Don't bury stale tasks in the general list. Call them out as their own section: "these haven't moved
in 2+ weeks — still relevant, or safe to cut?" Let the owner decide to act, defer, or kill each one.
Don't auto-delete anything.

### Step 4 — build the realistic plan

For a day: pick a short list (3–5 items is usually the ceiling for a real day, fewer if there are
meetings eating the calendar) prioritizing overdue and due-soon items, informed by what the owner has
flagged as currently important. For a week: group by day, front-loading anything with a hard external
deadline.

Be honest about capacity. If there are 14 "due this week" items and no way to realistically do all of
them, say so directly and propose what to cut or push rather than handing back a list that sets the
owner up to fail.

### Step 5 — write back

Update `TASKS.md` directly if priorities shift, due dates get confirmed, or stale items get
resolved/killed per the owner's direction, per `capture-everything`. If planning surfaces a new task
mentioned in passing, add it. Log the day's/week's plan to the journal if it reflects a real decision
about where time is going.

## What NOT to do

- Don't just re-list every open task in due-date order and call that prioritization — actual triage
  requires judgment about what matters, not just what's soonest
- Don't silently delete or mark stale tasks complete — flag and ask
- Don't hand back a day plan with 12 items and call it realistic — cap it and say why
- Don't treat "old" and "stale" as the same thing — an old task that's actively being chipped away at
  isn't a problem; an old task nobody has touched in a month is

## Worked example

**Owner:** "What should I focus on today?"

**Sample output:**

```
TASK COMMAND — Wednesday 7/15

OVERDUE (2)
- Send Bramwell contract redline — due 7/12, 3 days late
- Submit Q2 estimated taxes — due 7/14, 1 day late — do this first, penalty risk

DUE TODAY/TOMORROW (3)
- Prep for 2pm call with Okafor Retail
- Approve final invoice batch (per invoice-chase review yesterday)
- Reply to Delacroix re: escalation flag from Monday's review

STALE — no movement in 2+ weeks, worth a decision (3)
- "Look into new accounting software" — added 6/20, no update since. Still want this, or cut it?
- "Follow up with Marcus re: referral" — added 6/28. Cold enough that a fresh outreach might read
  better than a "follow up."
- "Update website portfolio" — added 6/22. Low urgency but sitting quietly — worth a due date or
  archive.

TODAY'S REALISTIC PLAN (given the 2pm call eats your afternoon):
1. File the estimated tax payment (overdue, real penalty risk) — 30 min
2. Send the Bramwell redline (overdue, unblocks their side) — 45 min
3. Prep for and take the 2pm Okafor call
4. Reply to Delacroix on the escalation — 15 min

Everything else pushes to tomorrow. The three stale items aren't urgent — flagging them so they don't
just keep aging, no action needed today unless you want to kill or reschedule one now.
```

## Handoff

Reads `TASKS.md` and context via the `operator-prime` pattern (`memory/context/you.md` for current
priorities). Writes plan decisions, due-date changes, and stale-task resolutions back via the
`capture-everything` pattern (`TASKS.md`, journal).
