---
name: capture-everything
description: >
  Proactive context preservation — prevents knowledge loss from conversation compression. Use
  AUTOMATICALLY when conversations get long, multiple topics get covered, decisions get made, or a
  session is ending. Also triggers on "write this down," "don't forget this," "save that," "done for
  now," "wrapping up." Fires at the END of any substantive session without being asked. This is the
  anti-compression layer — it writes context to the vault instead of letting it fade as the
  conversation grows. Use proactively, every time real work happens.
---

# Capture Everything — Anti-Compression Protocol

## Why this exists

Claude conversations compress as they get long. Client names, exact numbers, decisions, and action
items get fuzzy or vanish. The vault exists specifically so that doesn't have to happen. This skill
is the bridge: instead of letting context degrade, write it to the vault, where it survives and can
be re-read next session.

Mental model: the vault is external memory. When the conversation is getting full, flush to disk.

## When to fire

Proactive, not reactive — don't wait to be asked.

1. **Conversation getting long** — multiple topics, clients, or decisions covered in one session
2. **A decision got made** — any time the owner commits to a direction, it needs to survive past
   this conversation
3. **New facts surfaced** — a client's terms, a contact's role, a status change, a number
4. **End of session** — do a final sweep before wrapping up
5. **Before a topic switch** — if the conversation is about to pivot from one client to another,
   capture the first one before it gets squeezed out
6. **Claude notices its own uncertainty** — hedging about something discussed earlier in this same
   conversation is a sign context is already degrading. Stop, capture, re-read.

## How to capture

### Step 1 — scan and categorize

Since the last capture (or session start), sort what happened into:

- Decisions
- Client/person updates (new facts, status changes)
- Action items
- New terms (glossary candidates)
- Tooling or process changes

### Step 2 — write, don't ask permission

| Category | Target | Action |
|---|---|---|
| Decisions | `journal/YYYY-MM-DD.md` → "Decisions made" | Append; create today's entry if missing |
| Client/project updates | `memory/clients/[Name]/` | Update or create |
| Person updates | `memory/people/[Name].md` | Update or create |
| Action items | `TASKS.md` | Add to the right section |
| New terms | `memory/glossary.md` | Add a row |
| Business-level facts | `memory/context/you.md` | Update relevant section |
| Session summary | `journal/YYYY-MM-DD.md` → "What happened today" | Append |

Routine writes don't need permission — that's the whole point, this should be frictionless.

### Step 3 — confirm briefly

One line, not a routing report:

> "Saved: updated the Riverside Landscaping file, added 2 tasks, journal entry for today done."

Mid-conversation auto-captures can be even shorter: "Context saved — 3 files updated."

### Step 4 — re-read after capturing

If the conversation continues, re-read the vault files just written instead of relying on memory of
what was discussed. The vault is now the source of truth, not the conversation history.

### Step 5 — bracket entities

Wrap people, clients, and projects in `[[double brackets]]` on first mention per section of any
vault write. Only bracket things with a real file in `memory/people/` or `memory/clients/` — if no
file exists yet, don't auto-create one, surface it to the owner so they decide if it's worth a file.
First-name shorthand uses the alias form: `[[Riverside Landscaping|Riverside]]`. Never bracket
inside code spans, file paths, or URLs. This keeps Obsidian's graph and backlinks actually useful
instead of decorative.

## What NOT to capture

- Small talk
- Claude's own reasoning, unless the owner wants a specific analysis saved
- Duplicate info already in the vault at the same level of detail
- Draft work-in-progress that isn't a final output

## Relationship to other foundation skills

`operator-prime` reads from the vault at session start. `capture-everything` writes to it during and
after. `memory-consolidation` and `pattern-radar` keep what's written accurate and useful over time.
Together they're one loop — see `operator-prime`'s "feedback loop" section for the full picture.

## The golden rule

When in doubt, write it down. A redundant entry costs nothing. A lost decision or forgotten client
detail costs real time and, eventually, real money.
