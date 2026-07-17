---
name: go-no-go
description: >
  Structured for/against framework for a specific deal, client, or project decision — pulls
  together deal size, time cost, strategic fit, red flags, and opportunity cost into a clear
  comparison, and pushes back with sharpening questions if the owner's framing sounds one-sided.
  Use when the owner asks "should I take this deal," "should I work with this client," "is this
  project worth it," "should I say yes to this," or describes an opportunity and seems to be
  weighing whether to commit. Also triggers on "walk me through whether I should do this" framing.
  This is decision SUPPORT — it organizes the for/against case and asks the questions the owner is
  skipping, it does not tell the owner to take or pass on the deal. Never output "you should take
  this" or "you should pass" as a bottom line.
---

# Go/No-Go — Structured Deal Decision Framework

## Why this exists

Solopreneurs say yes to bad deals under time pressure, flattery, or fear of an empty pipeline —
and say no to good ones out of scope-creep anxiety or a bad gut reaction to one detail. The failure
mode isn't usually missing information, it's unstructured weighing: the owner lists the reasons to
say yes because those are top of mind (they're excited, or they need the revenue), and the reasons
to say no stay unexamined. This skill exists to force the full comparison onto the table before the
gut makes the call.

## The rule that overrides everything else in this file

**This skill never outputs "take it" or "pass."** It builds the for/against comparison, surfaces
what's missing, and asks the questions the framing is dodging. If the owner asks directly "just
tell me yes or no," say so plainly: the framework can tell you what the tradeoffs actually are, but
whether $8K and a strategic-fit gamble is worth six weeks of your time is a call about your risk
tolerance and your runway, not something this can compute for you. Hand back the comparison and ask
what's tipping it for them.

## When to fire

- "Should I take this deal/client/project?"
- "Is this worth it?"
- "Should I say yes to [opportunity]?"
- Owner describes a specific opportunity (deal size, timeline, client) and is visibly weighing it
- Owner asks for help drafting a response to a prospect and the underlying question is really
  "should I even do this"

## How to do it

### Step 1 — pull together what's known

Ask for (or extract from what the owner already gave):

- **Deal size** — dollar value, and over what timeframe (one-time vs. recurring changes the math)
- **Time cost** — realistic hours/weeks, not the client's estimate; ask the owner for their own
  gut-check number if they haven't given one
- **Strategic fit** — does this move toward where the owner says they want the business to go
  (check `memory/context/you.md` and any goals/strategy notes in the vault for what "where they
  want to go" actually is, rather than assuming)
- **Red flags** — anything already raised: slow-to-respond client, unclear scope, budget hedging,
  reputation concerns, past pattern of similar deals going sideways (check `memory/clients/` or
  `journal/` for prior history with this person/company if it exists)
- **Opportunity cost of saying yes** — what does the owner NOT do if they take this on? Is there
  already a pipeline of other work this would crowd out, or is the calendar actually open?

If the owner hasn't supplied one of these, ask directly rather than leaving it blank — an
incomplete go/no-go with unstated gaps is more dangerous than a shorter one that's honest about
what it doesn't know yet.

### Step 2 — check the framing before building the comparison

Read back what the owner has said so far. If it's lopsided — every point raised is a reason to say
yes, or every point is a reason to say no — stop and ask sharpening questions before writing
anything up. Don't silently fill the other column yourself; the point is to get the owner's own
read on the missing side, not to invent a counter-argument for them. Examples of sharpening
questions:

- "You've mentioned the revenue and the relationship — what's the part of this that gives you
  pause? There's usually something, even if it's small."
- "What would have to be true for this to go badly? Walk me through the worst realistic version."
- "If you turn this down, what do you do with that time instead — is there something specific, or
  is the calendar actually open?"
- "Is there anything about this client/project that's a repeat of a pattern that's burned you
  before?" (worth cross-checking `journal/` and `memory/clients/` for actual history, not just
  asking blind)

Only move to Step 3 once there's real material on both sides — even a thin "no" column that's
honestly thin, is better than one that was never asked about.

### Step 3 — build the for/against comparison

```
DEAL: [name/description]

FOR                                    AGAINST
- Deal size: $X over [timeframe]       - Time cost: ~Y hours/weeks at [owner's rate,
- Strategic fit: [specific reason]       if known] = opportunity cost of $Z
- [relationship/pipeline reason]       - Red flag: [specific concern, not vague "risk"]
- [other stated positive]              - Opportunity cost: [what this displaces, if anything]
                                        - [other stated negative]

OPEN QUESTIONS (unresolved, worth getting answers before deciding):
- [anything Step 1/2 surfaced that's still unknown]
```

Keep entries specific — "red flag: client pushed back on the deposit twice already" is useful,
"risk: might be difficult" is not. If a line item doesn't have a specific reason behind it, ask for
one or drop it.

### Step 4 — state the tradeoff, not the verdict

Close with something like:

```
Reading this back: the case for is mostly [revenue / strategic fit / relationship]. The case
against is mostly [time cost / red flag / opportunity cost]. The open question that seems to
matter most is [X] — that's probably worth resolving before deciding either way, if there's
time to ask.

This isn't a close call / this is genuinely close [pick whichever is true based on the actual
comparison] — but which way it tips depends on how much weight you put on [the specific
tradeoff], and that's your call, not something the framework decides for you.
```

Never end with "so you should take it" or "so you should pass." If the comparison is genuinely
lopsided (nine reasons for, no real reasons against, and the owner is just nervous), it's fine to
say the comparison itself looks one-sided — but frame it as "the case against is thin, is that
because there really isn't one, or because we haven't found it yet" rather than declaring a
verdict.

### Step 5 — write back

- If the owner decides on the spot, that's a reactive fact — log it per `capture-everything`:
  `journal/YYYY-MM-DD.md` decision log, and if it's a new or existing client, update
  `memory/clients/[Name]/` with the deal terms and decision
- If undecided, add a `TASKS.md` follow-up with whatever the open question was and a date to
  revisit, so it doesn't just evaporate
- If a red flag came up that's worth remembering for next time (a client pattern, a type of deal
  that keeps causing trouble), that's the kind of fact `pattern-radar` should eventually catch —
  note it in the journal now so it's there to find later

## Worked example

**Owner:** "New client wants a 3-month retainer, $6K/month, but they want daily availability and
their brief is really vague. Feels like a lot of money though."

**Sharpening check:** owner has only stated the "for" (money) and one soft "against" (vague brief).
Ask: "What's daily availability actually cost you — does that block other clients, or is it more
of an annoyance? And has 'vague brief' been a problem with past clients like this, or is this a
guess?" Owner responds: daily availability would mean turning down a standing weekly client worth
$1,800/month, and yes — a similar vague-brief client eight months ago turned into 3x the promised
scope for the same price (check `memory/clients/` confirms this if a file exists).

**Comparison:**
```
FOR                                     AGAINST
- $6K/month, 3-month commitment        - Daily availability displaces existing $1,800/month
  ($18K total)                           client — real opportunity cost, not hypothetical
- New logo, could lead to referrals    - Vague brief: matches a past pattern (see [[Client X]],
                                          8 months ago) that turned into 3x scope creep
                                        - No scope document yet — open question

OPEN QUESTIONS:
- Can a scope doc get nailed down before signing, given the past scope-creep pattern?
- Net gain if displaced client is included: $18K - ($1,800 × 3) = $12,600 net over 3 months,
  not $18K
```

**Summary:** "The headline number is $18K, but the real net gain after the displaced client is
closer to $12,600 — that's worth knowing before this feels like a clear yes. The vague-brief
pattern matching a client that cost you scope creep before is the thing I'd want resolved, not
brushed past — worth trying to pin down a scope document before signing rather than after. Whether
$12,600 net plus the new-logo upside is worth that risk is your call."
