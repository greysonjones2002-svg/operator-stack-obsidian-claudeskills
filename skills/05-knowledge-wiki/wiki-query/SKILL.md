---
name: wiki-query
description: >
  Answers a question from the owner's accumulated knowledge wiki instead of a fresh web search or
  general knowledge. Use when the owner asks something that should already be answered by material
  they've previously ingested — "what do I know about X," "check my wiki," "what have I found on
  this," "how does X compare to Y" (where both are things already in the wiki), or any question in a
  domain the wiki actively tracks. Not for questions about live/current events the wiki hasn't
  ingested yet, and not for business-ops questions (tasks, invoices, client status) — those belong to
  the core-ops and revenue skills, not the wiki.
---

# Wiki Query

## Why this exists

Answering a synthesis question by re-reading raw sources from scratch every time is slow and wastes
the work already done. If the owner asked a related question last month and the wiki captured that
synthesis, this question should start from there — not from zero. The wiki exists so answers compound
instead of evaporating into old chat history the moment the conversation ends.

This skill has one more job past just answering: real synthesis work — a comparison, an analysis, a
connection between two things that wasn't written down anywhere before — is valuable enough that it
should get filed back into the wiki, not left to die in the chat transcript. A good answer here should
usually become tomorrow's evidence.

## Step by step

### 1. Read the index first

Always start with `index.md`. It's the content-oriented catalog of every wiki page — link, one-line
summary, category, sometimes date or source count. Reading it first means the search stays fast and
grounded even without embedding-based retrieval — at the scale this wiki is built for (on the order of
a hundred sources, a few hundred pages) grep-style search over `index.md` and page titles is enough;
don't over-engineer this into a vector search.

### 2. Identify candidate pages

From the index, pick the pages that plausibly answer the question. Cast slightly wide rather than
narrow on the first pass — a comparison question usually needs the pages for both things being
compared, plus any existing comparison page if one's already there.

### 3. Drill into the pages

Read the candidate pages in full. Follow `[[wikilinks]]` one level out if a page references something
directly relevant that wasn't obvious from the index. Note which raw sources each claim traces back to
— the summary and entity pages should link back to `raw/`, so pull that thread if the question needs
source-level precision (an exact number, an exact quote, an exact date).

### 4. Synthesize with citations

Answer the question directly, then ground it: cite the specific wiki page(s) the answer draws from,
and the underlying source(s) where it matters (a number, a quote, a claim someone might want to
verify). Citations point to wiki pages by name — `[[competitor-x]]`, `[[acme-q2-earnings-summary]]` —
not to a vague "the wiki says."

If the question surfaces a genuine contradiction between pages (something `source-ingest` may have
already flagged, or something new), say so plainly rather than picking a side quietly.

### 5. Be honest about gaps

If the wiki doesn't have enough to answer well, say that — don't fill the gap with general knowledge
and present it as if it came from the wiki. The distinction matters: "the wiki doesn't have anything
on this yet" is a useful, actionable answer. A confident-sounding answer that's actually the model's
background knowledge dressed up as wiki-sourced is worse than no answer, because it looks verified
when it isn't. If it's a small gap, it's fine to add "here's what I know generally, separate from what
your wiki has" as a clearly labeled addendum — just don't blur the two together. A wiki with a
consistent gap in one area is also a good candidate to flag for `wiki-lint`.

### 6. Offer to file the answer back

If the answer involved real synthesis — connecting facts across pages that weren't already connected,
producing a comparison, drawing a conclusion the wiki didn't already state outright — offer to save it
as a new wiki page: *"Want me to file this comparison as a page in the wiki? It'll save the next
question like this from starting over."* If the owner says yes, write it the same way `source-ingest`
writes a wiki page: proper frontmatter (per `frontmatter-standard`), `[[wikilinks]]` to the pages it
drew from, and an index entry. Don't auto-file without asking — some answers are one-off and don't
need to become permanent pages, and that's the owner's call, not a default.

If the answer was a straightforward pull from one or two pages with nothing new synthesized, there's
nothing to file — just answer.

### 7. Log the query

Append a short entry to `log.md`:

```
## [2026-07-15] query | How does Competitor X's Q3 pricing compare to ours?
- Pages used: wiki/competitor-x.md, wiki/pricing-strategy-notes.md
- Filed back: wiki/competitor-x-vs-us-pricing-comparison.md (new)
```

If nothing got filed back, note that too (`- Filed back: no, straightforward lookup`) — the log should
reflect what actually happened, not just the wins.

## Worked example

Owner asks: "Does what I read about Competitor X's new pricing change anything about how we should
position against them?"

1. Read `index.md` — find `wiki/competitor-x.md`, `wiki/competitor-x-q3-pricing-summary.md`, and
   `wiki/positioning-notes.md`.
2. Read all three in full.
3. Synthesize: Competitor X dropped their entry tier price 20%, which narrows the gap that
   `positioning-notes.md` had been leaning on — cite both pages, note the specific numbers from the
   summary page.
4. This is new synthesis (the wiki had the pricing fact and the positioning fact separately, but never
   connected them) — offer to file it as `wiki/positioning-vs-competitor-x-2026-07.md`.
5. Owner says yes — write the page with frontmatter, wikilinks back to both source pages, add it to
   `index.md`.
6. Log the query and the filed-back page in `log.md`.

## What NOT to do

- Don't skip `index.md` and go straight to guessing which pages might be relevant — that's how
  relevant pages get missed.
- Don't answer from general knowledge and imply it came from the wiki. If it didn't come from the
  wiki, say so.
- Don't auto-file every answer as a new page — only offer when there's real synthesis worth keeping.
- Don't bury a contradiction in a hedge ("it's a bit unclear...") when the honest answer is "these two
  pages disagree, here's the discrepancy."
