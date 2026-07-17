---
product: Operator Stack
version: v1.1 (build)
updated: 2026-07-15
---

# Operator Stack — Skill Manifest

34 skills across 7 categories. Install `00-foundation` first and always — every other skill depends on the vault structure and memory habits it establishes. `01`–`04` (business ops), `05` (knowledge wiki), and `06` (Obsidian formats) can be installed selectively — a buyer who doesn't build software can skip most of `03-build-ship`, one who has no interest in a research/second-brain layer can skip `05` — but the pack is sold and positioned as one coherent stack, not à la carte.

## 00-foundation — the self-learning / self-maintaining engine

Ported from Krastor's own operating system, plus a first-run onboarding skill. This is the actual differentiator versus every other skill pack on the market — it's not a static list, it's a memory loop that starts working from message one instead of a blank template.

| Skill | Fires when | Does |
|---|---|---|
| `day-one-setup` | First session in a freshly installed vault (empty `you.md`) | Interviews the owner, fills in `you.md`/`preferences.md`/`glossary.md` directly, recommends which skill categories matter most for them |
| `operator-prime` | Start of every substantive session; unrecognized name/project mid-session | Reads the vault (CLAUDE.md, you.md, glossary, TASKS.md, latest journal) before doing any real work |
| `capture-everything` | Long conversations, decisions made, session ending, topic switch | Writes decisions, facts, and action items to the vault before they compress out of context |
| `memory-consolidation` | Owner corrects a fact, or Claude notices a contradiction | Reactively fixes the vault to match reality — never proactively rewrites for "tidiness" |
| `pattern-radar` | Owner asks "what's working," or after 5+ similar entries pile up | Mines journal/task history for recurring patterns worth turning into a standing rule |
| `vault-hygiene` | Weekly, or on request | Finds orphan notes, broken links, missing frontmatter, stale files — fixes or flags |
| `frontmatter-standard` | Any time a new note is written | Stamps consistent metadata so the vault stays searchable as it grows |
| `propose-new-skill` | Claude does the same multi-step manual task 3+ times with no matching skill | Drafts a new SKILL.md for the owner's review — this is how the pack grows itself over time |

**Feedback loop:** `operator-prime` (read) → work happens → `capture-everything` (write) → `pattern-radar` and `memory-consolidation` keep it accurate → next session's `operator-prime` starts smarter. This loop is the whole product. Every other skill is a spoke off this hub.

## 01-core-ops — the boring stuff that eats a solopreneur's week

| Skill | Trigger | Does |
|---|---|---|
| `cash-flow-pulse` | "how's my cash," "can I afford," "runway" | 30/60/90-day cash forecast from manual figures or CSV, no connector required |
| `invoice-chase` | "who owes me," overdue invoice mentioned | Drafts payment reminders matched to each client's tone and history |
| `contract-guard` | Contract pasted or uploaded, "review this," "am I exposed" | Plain-English risk flags on any contract — NDA, MSA, vendor agreement |
| `task-command` | "what's on my plate," daily/weekly planning | Runs TASKS.md as a real task system — priorities, staleness, planning |
| `month-end-close` | "close the month," "what's my P&L," month-end | Reconciles records, flags gaps, writes a plain-English monthly narrative |

## 02-revenue — getting and keeping customers

| Skill | Trigger | Does |
|---|---|---|
| `lead-triage` | "who should I call," new leads to sort | Scores and ranks leads, gives a call-list with talking points |
| `outreach-drafts` | "draft an email to," "follow up with" | Personalized cold and follow-up messages in the owner's voice |
| `proposal-builder` | "write a proposal for," "put together a quote" | Turns scope notes into a client-ready proposal/SOW |
| `client-pulse` | "how are my clients feeling," reviews/complaints pasted | Synthesizes sentiment from notes, emails, reviews into a fixable list |
| `content-engine` | "what should I post," "content plan" | Turns what's actually selling into a content/outreach calendar |

## 03-build-ship — for owners who build their own tools

| Skill | Trigger | Does |
|---|---|---|
| `quick-site` | "I need a landing page," "build a site for" | Scaffolds and ships a simple site or page, no dev team required |
| `automation-architect` | "this process is manual and slow," "automate" | Maps a manual process to the right automation pattern and scopes the build |
| `tool-builder` | "I need a calculator/tracker/form for" | Builds small single-purpose internal tools the owner actually needs |

*v1.2 candidates, not built yet: API/integration wiring skill, no-code vs. custom build-or-buy advisor. Flagged here so `propose-new-skill` doesn't rediscover them from scratch.*

## 05-knowledge-wiki — the second brain layer

A separate memory system from the business-ops layer above — built for compounding research and knowledge over time rather than day-to-day operations. Architecture: `raw/` (immutable sources) → `wiki/` (Claude-maintained pages) → `index.md` (content catalog, read first) + `log.md` (chronological record). Usable for market research, competitive tracking, due diligence, course/book notes, or a personal knowledge base — by a solopreneur, an agency owner researching a market, or anyone building a second brain for its own sake.

| Skill | Trigger | Does |
|---|---|---|
| `source-ingest` | New source provided (paste, upload, URL, described) | Reads it, integrates it into the wiki — updates entity/concept/summary pages, the index, and the log |
| `wiki-query` | A question that should draw on accumulated knowledge, not a fresh search | Reads the index first, drills into relevant pages, synthesizes a cited answer; offers to file real synthesis back into the wiki |
| `wiki-lint` | Weekly, or "check my knowledge base," "what's stale" | Health check for contradictions, stale claims, orphan pages, missing pages for repeated concepts, gaps |

## 06-obsidian-companion — native Obsidian format skills

Bundled from [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills), MIT licensed — not written by Krastor, ship the license notice. Teaches Claude the file formats Obsidian actually uses natively, so the vault behaves like a real Obsidian vault instead of a folder of plain markdown that happens to open in it.

| Skill | Does |
|---|---|
| `obsidian-markdown` | Wikilinks, embeds, callouts, YAML properties/frontmatter |
| `obsidian-bases` | `.base` database-style table/card views with filters and formulas |
| `json-canvas` | `.canvas` visual boards — nodes, edges, groups |
| `obsidian-cli` | Command-line vault interaction, plugin/theme development |
| `defuddle` | Clean markdown extraction from web pages (used by `source-ingest` for URL sources) |

## 04-decision-support — a sparring partner, not just a task-doer

| Skill | Trigger | Does |
|---|---|---|
| `price-check` | "should I raise prices," margin questions | Margin-by-product breakdown and pricing-scenario data — data only, never picks the price for the owner |
| `go-no-go` | "should I take this deal/client/project" | Structured decision framework, surfaces the case against as well as for |
| `competitor-radar` | "what's [competitor] doing" | Lightweight competitive positioning check, web-search based |
| `quarterly-review` | "how's the quarter going," "QBR" | Revenue/margin/customer-health trend review with prioritized next-quarter actions |
| `risk-scan` | "what could go wrong," periodic review | Risk register — vendor, contract, cash, key-person, concentration risk |

## Packaging status

Currently: raw `SKILL.md` files in category folders, matching the Agent Skills spec (YAML frontmatter `name` + `description`, markdown body). Not yet packaged as an installable Claude Code plugin or `.skill` bundle for one-click install — that packaging step is required before the $99 sale, not before the friend beta (the friend can install skills manually, same as Krastor does today via `scripts/sync-vault-skills-to-cowork.ps1`-style setup).

**Before public sale, still needed:**
- [ ] Package as installable plugin/bundle (see `cowork-plugin-management:create-cowork-plugin` skill for the mechanics)
- [ ] Strip every Krastor-specific reference from generic skills — verify none leaked in from the adaptation pass (done once already for the original 25; re-verify after the expansion pass)
- [ ] Friend beta on a genuinely fresh vault — fix whatever breaks in first-run onboarding, specifically test that `day-one-setup` actually fires correctly and doesn't feel like a form
- [ ] Resolve the TeamBrain Personal Tier positioning question (see README "Open item")
- [ ] Decide final product name (working title: Operator Stack)
- [ ] Write buyer-facing landing page / sales copy (separate from this internal manifest)
- [ ] Push to a GitHub repo (git repo initialized locally 2026-07-15 — remote/push still needs Greyson's own GitHub auth, Claude can't authenticate that from this session)
- [ ] Spot-check the 8 new/expanded skills (day-one-setup, the 3 knowledge-wiki skills) for voice consistency, same as the original 20
