---
name: vault-hygiene
description: >
  Structural maintenance pass — finds orphan notes, broken links, missing frontmatter, and stale
  files that haven't been touched despite still being active. Use on a weekly cadence, or whenever
  the owner says "clean up the vault," "audit my notes," "what's stale," "check the vault," or
  "maintenance pass." This is structural (does the vault hold together, is metadata consistent) —
  not factual accuracy, which is memory-consolidation's job.
---

# Vault Hygiene

## What this checks

1. **Orphan notes** — files with no incoming links and no reference anywhere else in the vault.
   Not automatically wrong, but worth flagging: was this meant to connect to something?
2. **Broken links** — `[[wiki-links]]` pointing at a note that doesn't exist. Either the linked note
   should be created, or the link is a typo that should point at the right file.
3. **Missing or inconsistent frontmatter** — see `frontmatter-standard` for the actual standard;
   this skill's job is finding violations, not defining the rules.
4. **Stale-but-active files** — a client marked active in `you.md` whose file in `memory/clients/`
   hasn't been touched in 2+ weeks. Could mean the relationship went quiet (worth knowing) or could
   mean updates aren't being captured (a `capture-everything` gap).
5. **Gaps in the journal** — missing days that suggest a session happened without a capture pass.

## How to run it

1. Scan `memory/`, `journal/`, and `TASKS.md` for the five checks above.
2. Group findings by severity: broken links and missing frontmatter are cheap, fix directly. Stale
   files and possible orphans need the owner's judgment — flag, don't guess.
3. Report as a short punch list, not a wall of text:

> **Vault hygiene pass:**
> - Fixed: 3 files missing frontmatter (added via `frontmatter-standard`)
> - Fixed: 1 broken link in `journal/2026-07-01.md` (pointed at a typo'd client name, corrected)
> - Flagged: `memory/clients/Harbor Fitness.md` marked active, no updates in 3 weeks — still live?
> - Flagged: `memory/people/Jordan.md` has no incoming links — orphaned or just new?

## What NOT to do

This skill finds and fixes *structural* problems (links, metadata, staleness signals). It does not
rewrite content, merge files, resolve factual contradictions, or delete anything — those are
`memory-consolidation`'s job, under its stricter reactive-only rule. When a hygiene pass surfaces a
factual contradiction along the way, hand it off: flag it the same way `memory-consolidation`
would, don't fix it here.

## Cadence

Default to running this proactively about once a week, or any time a deep `operator-prime` read
turns up enough friction (broken links interrupting normal reading) that it's clearly overdue.
Don't run it so often that it becomes noise — this is upkeep, not a every-session ritual.
