---
name: source-ingest
description: >
  Adds a new source to the owner's knowledge wiki instead of just filing it away. Use when the owner
  pastes text, uploads a document, gives a URL, or describes something they just read, watched, or
  heard and wants it captured — including "add this to my wiki," "ingest this," "file this away,"
  "I just read something on X, here's the link," or any similar handoff of new material. For URL
  sources that are live web pages, run the `defuddle` skill first to pull clean markdown before
  ingesting — don't hand raw HTML to the wiki. Not for business-ops material (invoices, tasks,
  client updates) — that belongs to `capture-everything` and the core-ops skills, not the wiki.
---

# Source Ingest

## Why this exists

The default way people use an LLM with documents is retrieval: dump files in, ask a question, the
model pulls relevant chunks and answers. That's fine for a single lookup. It falls apart the moment
a question needs synthesis across five, ten, or fifty sources — every time you ask, the model
re-derives the connections from scratch, because nothing from the last answer stuck around.

This skill does the opposite. Every time a new source comes in, it doesn't just get filed — it gets
read, and what's learned from it gets folded into a standing wiki: summary pages, entity pages,
concept pages, an index. The wiki is a compounding asset. Ingest source #40 and it should benefit
from everything the wiki already knows from sources #1 through #39 — cross-references already exist,
contradictions already got flagged, the synthesis already reflects what came before. You're not
re-reading the whole library every time you ask a question; you're reading a wiki that's already
been built from it.

Three folders do the work:

- `raw/` — the source material itself, untouched. This skill writes into it once (saving a new
  source) and never edits an existing raw file. If assets (images, screenshots) come with a clipped
  page, they land in `raw/assets/`.
- `wiki/` — the pages this skill creates and maintains. Summaries, entity pages, concept pages,
  comparisons. This is the layer that gets smarter over time.
- `index.md` and `log.md` — navigation. `index.md` is the catalog (updated every ingest); `log.md` is
  the append-only history (one entry per ingest).

## Step by step

### 1. Get the source into raw text

- **Pasted text or an uploaded document** — use it as-is.
- **A live URL** — run `defuddle` first to extract clean markdown. Don't ingest raw HTML; it wastes
  tokens and buries the actual content in navigation and boilerplate. If the page is already markdown
  (a `.md` URL, a GitHub README, etc.), skip straight to fetching it.
- **Described from memory** ("I just watched a talk about X, here's the gist...") — there's no raw
  document to save. Note this in the raw file itself (e.g., `raw/2026-07-15-owner-notes-on-x-talk.md`
  with a header noting it's a paraphrase, not a transcript) so future ingests know this source is
  secondhand and weight it accordingly.

Save the raw material to `raw/` with a clear filename (date-prefixed if useful for ordering, e.g.
`raw/2026-07-15-acme-q2-earnings-call.md`). This file is never edited again after this step — if the
source needs correcting later, that's a new source, not an edit to an old one.

### 2. Gauge how much framing you need

For a straightforward source — a short article, a source in a domain the wiki already covers well, a
source that obviously slots into an existing page — just ingest it. Don't interrupt the owner to ask
what a two-paragraph note is about.

For an unfamiliar or ambiguous source — a long document, a new domain the wiki hasn't touched, a
source that could reasonably update several different pages — ask one focused question before diving
in: *"This looks like it touches both the competitor landscape and the pricing model pages — what do
you want me to prioritize pulling out?"* One question, not a checklist. The point is to avoid burning
effort extracting the wrong things from a dense source, not to gate every ingest behind a Q&A.

### 3. Read and extract

Read the full source. Pull out: the core claims, any numbers or dates worth preserving exactly (not
rounded, not paraphrased into vagueness), named entities (people, companies, products, tools), and
anything that confirms, extends, or contradicts something already in the wiki.

### 4. Write or update the summary page

Every ingested source gets a summary page in `wiki/` — one page per source, even short ones. This is
the anchor other pages link back to. Include: what the source is, when it was ingested, the key
takeaways in the owner's terms (not a copy-paste of the source), and a link back to the raw file.

### 5. Update entity and concept pages

This is the step that makes the wiki compound instead of just accumulate. A single source might touch
10-15 existing pages — don't stop at the summary. For every named entity or concept the source
touches:

- If a page already exists, update it: add the new data point, revise a claim if the new source is
  more current or more authoritative, or add a note if the new source contradicts what's there (flag
  the contradiction explicitly rather than silently overwriting — see below).
- If no page exists yet and the entity or concept is substantial enough to warrant one (not a passing
  mention), create it.
- Every page — new or updated — gets proper `[[wikilinks]]` to related pages and frontmatter per this
  pack's `frontmatter-standard` skill. Don't re-derive the frontmatter convention here; apply it the
  way that skill defines it.

If the new source contradicts an existing claim, don't just pick a winner silently. Add a visible note
on the affected page — something like `>[!warning] Conflicts with [[source-2026-04-earnings]] — that
source said X, this one says Y as of [date]` — and let the owner or a later `wiki-lint` pass resolve
it if it's not obvious which is correct.

### 6. Update the index

Add or update the entry in `index.md`: link, one-line description, category, and any useful metadata
(date, source count for pages that aggregate multiple sources). This is what makes `wiki-query` fast
later — it reads the index before it reads anything else, so an entry that's missing or vague here
costs every future query.

### 7. Log it

Append an entry to `log.md` using a consistent, grep-able prefix:

```
## [2026-07-15] ingest | Acme Q2 Earnings Call
- Raw: raw/2026-07-15-acme-q2-earnings-call.md
- Pages touched: wiki/acme-corp.md (updated), wiki/saas-pricing-trends.md (updated), wiki/competitor-landscape.md (updated)
- Pages created: wiki/acme-q2-earnings-summary.md
- Flagged: revenue figure conflicts with wiki/acme-corp.md's prior estimate (see note on that page)
```

## Worked example

Owner pastes a link to a blog post about a competitor's new pricing tiers.

1. Run `defuddle` on the URL, get clean markdown.
2. Save it to `raw/2026-07-15-competitor-x-pricing-post.md`.
3. Source is straightforward and the wiki already has a `competitor-x.md` page — no need to ask what
   to prioritize, just proceed.
4. Read it: three new tiers, specific prices, one quote about their positioning against mid-market
   buyers.
5. Write `wiki/competitor-x-q3-pricing-summary.md` — what changed, the actual numbers, the quote.
6. Update `wiki/competitor-x.md` (add the new pricing structure, link to the summary), update
   `wiki/pricing-strategy-notes.md` if the wiki tracks the owner's own pricing thinking (note the gap
   or overlap with the competitor's move), add `[[wikilinks]]` between all of them.
7. Update `index.md` with the new summary page entry.
8. Append the `log.md` entry.

## What NOT to do

- Don't skip the raw save and go straight to wiki pages — the raw file is what every wiki claim
  traces back to, and it needs to exist even if the wiki text later gets revised.
- Don't touch a source's raw file after the fact. New information about the same topic is a new
  source, not a correction to an old one.
- Don't silently overwrite a contradicted claim — flag it and let it get resolved deliberately.
- Don't skip index or log updates because the source felt minor. A missing index entry is a page
  `wiki-query` will never find.
- Don't over-ask. One clarifying question for a genuinely ambiguous source is enough; a straightforward
  source needs zero.
