---
name: wiki-lint
description: >
  Health check for the knowledge wiki's content — not its file structure. Use on a weekly-ish cadence
  or whenever the owner asks "check my knowledge base," "what's stale in my wiki," "any
  contradictions," "audit the wiki," or "what's missing." Finds contradictions between pages, claims
  that newer sources have superseded, orphan pages, concepts mentioned often but never given their own
  page, missing cross-references, and gaps a web search could close. This is the content-accuracy
  counterpart to `vault-hygiene`, which handles structural upkeep (broken links, missing frontmatter,
  stale client files) on the business-ops side — this skill does the same job for what the wiki
  actually says, not how the files are organized.
---

# Wiki Lint

## What this checks

1. **Contradictions between pages** — two pages making incompatible claims about the same thing,
   including ones `source-ingest` already flagged and never got resolved, plus new ones that only show
   up when pages are read side by side.
2. **Stale claims** — a page states something as current fact, but a more recent source in `raw/` or a
   more recently updated page supersedes it. This is different from `source-ingest`'s contradiction
   flag: a stale claim might not directly contradict anything, it's just aged past its shelf life
   (a "current price" from six months ago, a "latest version" that's no longer latest).
3. **Orphan pages** — pages in `wiki/` with no inbound `[[wikilinks]]` from anywhere else in the wiki.
   Not automatically wrong (a page can be genuinely standalone), but worth surfacing: was this meant to
   connect to something and never got linked?
4. **Missing pages for repeated concepts** — a name, entity, or concept that shows up across multiple
   summary or entity pages but never got its own page. If something is referenced five times, it
   probably deserves to be a first-class page instead of a scattered mention.
5. **Missing cross-references** — two pages that clearly relate (same entity, same source, adjacent
   topic) but don't link to each other. Cheap to fix, easy to miss during a normal ingest.
6. **Gaps a web search could fill** — a page with an open question, an unresolved contradiction with
   no clear resolution, or a concept that's thin because only one source has ever touched it. Flag
   these as candidates for a fresh source, not something to fill in from general knowledge on the
   spot — that's `wiki-query`'s "be honest about gaps" rule applied here too.

## How to run it

1. Read `index.md` for the full page inventory, then scan `wiki/` for the checks above. Use `log.md`
   to spot patterns over time — repeated ingest entries touching the same page with no resolution
   noted is itself a signal something's gone stale or contradictory.
2. Group findings by what's cheap to fix directly versus what needs the owner's judgment:
   - Cheap, fix directly: missing cross-references, obvious orphan pages that clearly belong linked
     somewhere, frontmatter gaps (apply `frontmatter-standard`).
   - Needs the owner: contradictions where it's not obvious which source is right, stale claims where
     "stale" is a judgment call, whether a repeated concept is worth a dedicated page, whether a gap is
     worth chasing down with a new source.
3. Report as a short punch list, not a wall of text:

> **Wiki lint pass — 2026-07-15:**
> - Fixed: added 3 missing cross-references between `wiki/competitor-x.md` and
>   `wiki/pricing-strategy-notes.md`
> - Fixed: linked orphan page `wiki/q2-market-notes.md` from `wiki/market-overview.md`
> - Flagged: `wiki/acme-corp.md` and `wiki/acme-q2-earnings-summary.md` disagree on Q2 revenue —
>   which source is more current?
> - Flagged: `wiki/competitor-x.md` pricing claim is from March, competitor since posted a Q3 update —
>   worth a fresh ingest?
> - Flagged: "Jordan Reyes" mentioned in 4 different pages, no dedicated page — worth creating one?
> - Flagged: `wiki/positioning-notes.md` has an open question about market size with no source behind
>   it — candidate for a web search ingest

4. Don't act on the flagged items without the owner's go-ahead — fix the cheap structural stuff
   directly, surface everything else and wait.

## What NOT to do

- Don't silently resolve a contradiction by picking whichever page looks newer — flag it, let the
  owner (or a fresh source) settle it.
- Don't rewrite pages for tone, brevity, or "cleanliness" during a lint pass. This is an accuracy and
  structure check, not an editing pass — touch only what a specific finding requires.
- Don't create a new page for every repeated mention automatically. Flag the candidates; let the owner
  decide which ones are worth the dedicated page.
- Don't fill a flagged gap from general knowledge just because a web search wasn't run yet. If the gap
  needs a source, say that's what it needs — don't quietly patch it with an unsourced claim.
- Don't confuse this with `vault-hygiene`. If a finding is about the wiki's file structure in general
  (not specific to knowledge content — e.g., something outside `05-knowledge-wiki` entirely), that's
  `vault-hygiene`'s job, not this skill's.
