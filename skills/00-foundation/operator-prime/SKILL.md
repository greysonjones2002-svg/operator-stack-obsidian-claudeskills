---
name: operator-prime
description: >
  Proactive self-training system that makes Claude smarter about this business every session by
  reading the vault first. Use AUTOMATICALLY at the start of every substantive session — don't wait
  to be told to "load context." If Claude is about to do real work (not just answer a quick factual
  question), it should prime itself first. Also trigger mid-conversation when Claude hits a name,
  client, or term it doesn't recognize — that's a signal to stop and read the vault instead of
  guessing. Trigger phrases: "you should know this," "we talked about this," "remember?," "check
  your notes," "catch me up," "what's the status on," or any sign Claude is operating without
  context it should already have.
---

# Operator Prime — Self-Training Protocol

## Why this exists

Every new Claude session starts from zero. The owner shouldn't have to re-explain who their best
client is, what's overdue, or how they like things phrased. That knowledge lives in the vault. This
skill makes Claude read it — proactively, every session, and any time it hits a gap mid-conversation.

The goal: Claude should feel like an operator who was in the room yesterday, not a stranger who
needs onboarding every morning.

## The prime sequence

### Level 1 — every session

1. `TASKS.md` — what's on the plate right now
2. `memory/context/you.md` — who runs this business, what it does, active work
3. `memory/glossary.md` — shorthand and terms specific to this business
4. Latest file in `journal/` — what happened most recently

This is the minimum. If Claude reads nothing else, read these four.

### Level 2 — when the request touches a specific client or person

- `memory/clients/[ClientName]/` — the **entire folder**, not just files already known from earlier
  in this conversation. Confirmed failure mode elsewhere: answering a "what's the status" question
  from partial memory instead of the full folder produces confidently wrong answers. Full-folder
  sweep, every time, even when Claude is sure it already knows what's in there.
- `memory/people/[Name].md` — role, history, preferences, last contact.

### Level 3 — recovery, when Claude is lost

If a name, acronym, or reference comes up that isn't recognized: don't guess. Check
`memory/glossary.md`, grep the vault for the term, read what turns up, then continue. This is
always better than asking the owner "who's that?" when the answer is sitting in a file, and always
better than inventing a plausible-sounding answer.

## When not to prime

- Quick factual questions with no business context needed ("what's 15% of 340?")
- Context already loaded earlier in this same session — don't re-read files just read
- The owner explicitly says "skip context, just do X"

## Self-training behaviors

Beyond the read sequence, Claude should get smarter about this business over time:

**Pattern recognition** — notice preferences that aren't documented yet (formatting habits,
decision-making patterns, tools reached for or avoided) and write them to `memory/context/you.md`
under "Learned preferences."

**Knowledge gap detection** — any time Claude has to ask something that should already be in the
vault, write the answer down immediately after getting it. Common gaps: a client mentioned with no
file yet, a term used with no glossary entry, a workflow step implied but never documented.

**Vault health** — periodically (weekly, or when doing a deep prime) check for stale client files,
orphaned references, and contradictions. Flag them to the owner or fix obvious ones directly — see
`memory-consolidation` for the rules on what counts as "obvious."

## The feedback loop

```
operator-prime (read) → work happens → capture-everything (write) → vault updates
        ^                                                                  |
        └──────────────────────────────────────────────────────────────────┘
                         next session reads the updated vault
```

Every capture makes the next prime better. Every prime that hits a gap should trigger a write. This
loop — not any single skill — is what makes the vault self-maintaining. It only works if both halves
fire consistently.

## Litmus test

After priming, Claude should be able to answer without asking:

- What's the business, and what stage is it at?
- What are the active clients/projects and their status?
- What happened in the last session?
- What's overdue or urgent right now?
- What does [any glossary term] mean?

If Claude can't answer these after priming, the vault has a gap — flag it, don't fake confidence.
