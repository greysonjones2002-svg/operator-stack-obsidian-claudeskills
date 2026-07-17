# CLAUDE.md

Instructions for Claude operating in this vault. Read this file completely before doing any real work.

---

## First session

If `memory/context/you.md` still has empty template fields, this is a fresh install — run the
`day-one-setup` skill before anything else. It interviews the owner and fills in `you.md`,
`preferences.md`, and `glossary.md` directly, so every skill after this one is working with real
context instead of a blank template.

## Boot sequence — do this before responding to any substantive request

1. Read `TASKS.md` — what's currently on the plate.
2. Read `memory/context/you.md` — who owns this business, what it does, active work.
3. Read `memory/glossary.md` — shorthand, acronyms, client codenames used in this vault.
4. Read the latest file in `journal/` (highest date) — what happened most recently.
5. If the request touches a specific client, read `memory/clients/[ClientName]/` in full — not just the files you already remember from earlier in this conversation. Full-folder sweep, every time.
6. If the request touches a specific person, read `memory/people/[Name].md`.

Skip this for quick factual questions that don't need business context ("what's 15% of 340?"). Do it for everything else, including things that feel like you already know the answer — you don't, this is a fresh session.

## Capture is lossless — write everything, filter nothing

When in doubt, write it down. Decisions, numbers, client names, dates, prices, terms, offhand comments that might matter later — capture the actual figure, not a rounded summary. "$4,200 deposit due the 15th" is correct. "About four grand due mid-month" has already lost information.

Don't wait to be asked. If a decision gets made in conversation, write it to today's journal entry before the conversation moves on.

## Consolidation rule

Reactive updates — allowed and expected: the owner corrects a fact, a status changes, a contradiction gets resolved. Fix it everywhere it appears.

Proactive rewrites — off by default: no unprompted mass cleanup, no "tidying" old journal entries, no condensing for brevity. If something looks stale or contradictory and the owner hasn't said anything, flag it and ask — don't silently fix it.

## End of session

Before wrapping up any session where real work happened: write a journal entry (or append to today's), update any client or people files that were touched, add new action items to `TASKS.md`. A session that ends without a vault write when real decisions were made is a bug.

## Skills

This vault ships with the Operator Stack skill pack, six categories:

- **00-foundation** — `day-one-setup`, `operator-prime`, `capture-everything`, `memory-consolidation`, `pattern-radar`, `vault-hygiene`, `frontmatter-standard`, `propose-new-skill`. Implements everything in this file automatically — invoke these rather than re-deriving the logic from scratch every time.
- **01-core-ops, 02-revenue, 03-build-ship, 04-decision-support** — business-function skills. Trigger on the situations described in each skill's own description; use the skill instead of improvising a generic answer.
- **05-knowledge-wiki** — `source-ingest`, `wiki-query`, `wiki-lint`. A second, separate memory system from the business-ops layer above: a compounding personal/research knowledge base at `knowledge-wiki/` (raw sources → Claude-maintained wiki pages → `index.md`/`log.md`). Use this for anything that's about accumulating and synthesizing knowledge over time — research, competitive tracking, reading notes, course notes — not for day-to-day business operations, which stay in the business-ops skills above.
- **06-obsidian-companion** — bundled from kepano/obsidian-skills (MIT licensed, see that folder's LICENSE file). Teaches Claude to write proper Obsidian-native formats: wikilinks/callouts/properties, `.base` database views, `.canvas` boards, and clean web-page extraction via Defuddle.

---

*This file is the owner's to edit. Add venture-specific rules, banned phrases, formatting preferences, anything that makes Claude sound like this business instead of a generic assistant.*
