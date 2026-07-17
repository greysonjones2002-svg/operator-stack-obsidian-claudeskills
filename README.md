---
product: Operator Stack
owner: Krastor
status: v1 complete, pre-packaging
created: 2026-07-15
updated: 2026-07-15
---

# Operator Stack — by Krastor

**The self-maintaining Claude + Obsidian second brain for anyone running a business — solo operator, agency owner, small business owner, or a builder standing up their own AI-run operation.**

## What this actually is

Operator Stack is a pack of Claude Agent Skills plus a matching Obsidian vault structure. Install both, and Claude stops being a chat window you re-explain your business to every session, and starts being an operator that remembers your clients, tracks your money, drafts your outreach, builds your simple tools, pushes back on bad decisions, and compounds a real knowledge base the longer you use it.

It's the same architecture Krastor runs on internally (vault-prime, context-offload, memory-consolidation, pattern-extraction) generalized for anyone who wants it — a single-operator business, a small agency, or a friend who just wants their own second brain. The proof this works is that Krastor has been running on it since day one.

**What it is not:** it is not a hosted SaaS, not a chatbot, not a CRM. The owner owns their vault, owns their Claude subscription, owns their data. Krastor sells the architecture and the skill pack — the same "we own the design, you own the tools" model Krastor uses with consulting clients.

## Seven categories, 34 skills

1. **Foundation (8 skills)** — the self-learning, self-maintaining engine, and the actual differentiator versus every other skill pack on the market. `day-one-setup` interviews the owner on first run and fills in their context automatically — this pack doesn't ship with blank templates the owner has to hand-fill. The rest (`operator-prime`, `capture-everything`, `memory-consolidation`, `pattern-radar`, `vault-hygiene`, `frontmatter-standard`, `propose-new-skill`) form the read/write/maintain loop that makes the vault get smarter the longer it's used, without the owner doing anything except keep working.
2. **Core ops (5 skills)** — cash flow, invoicing, contracts, tasks, month-end close.
3. **Revenue (5 skills)** — lead triage, outreach, proposals, client sentiment, content planning.
4. **Build/ship (3 skills)** — landing pages, automation scoping, small internal tools.
5. **Decision support (5 skills)** — pricing, go/no-go, competitive checks, quarterly review, risk — all built to hand the actual call back to the owner, never to make it for them.
6. **Knowledge wiki (3 skills)** — a second, separate memory system for compounding research and knowledge over time: `source-ingest`, `wiki-query`, `wiki-lint`, built on a raw-sources → Claude-maintained-wiki → index/log architecture. This is the "second brain" half of the product — usable for market research, competitive intelligence, book/course notes, or a personal knowledge base, independent of the day-to-day business-ops layer.

Plus **06-obsidian-companion** — five bundled skills (MIT licensed, from kepano/obsidian-skills) that teach Claude to actually use Obsidian's native formats: wikilinks/callouts/properties, `.base` database views, `.canvas` boards, and clean web-page extraction. Without these, Claude tends to write plain markdown that technically works but ignores everything Obsidian does well.

## Why this and not the other solopreneur skill packs already on the market

Anthropic shipped Claude for Small Business in May 2026. There are already Solopreneur OS packs, 15-skill stacks, and marketplaces selling one-off skills for $4 a piece. None of what's out there does what Operator Stack does:

1. **It's self-maintaining, not a static list.** Most competing packs are a folder of skills that never change and never learn the owner's business. The foundation layer captures decisions, consolidates duplicates, flags stale or contradictory data, and proposes new skills when it notices a recurring gap.
2. **It onboards itself.** `day-one-setup` means the owner never stares at an empty template file — the vault knows their business by the end of the first real conversation.
3. **It's two products in one: business operator + second brain.** The knowledge-wiki layer is a compounding research/synthesis system, not just task management — most competing packs don't have anything like it.
4. **It's built by someone who runs an actual business on it.** Every business-ops skill in this pack mirrors a skill Krastor uses for real client work, generalized. That claim has to stay true — don't ship a skill in this pack that Krastor itself wouldn't trust with real client money or a real deadline.

## Structure

```
operator-stack/
├── README.md                    <- this file
├── MANIFEST.md                  <- full skill inventory, categories, install order
├── vault-template/              <- the starter Obsidian vault a buyer clones
│   ├── CLAUDE.md                <- boot sequence + first-session logic
│   ├── TASKS.md
│   ├── journal/README.md
│   ├── knowledge-wiki/          <- raw/, wiki/, index.md, log.md scaffolding
│   └── memory/
│       ├── context/you.md       <- filled in by day-one-setup, not hand-edited
│       ├── context/preferences.md
│       └── glossary.md
└── skills/
    ├── 00-foundation/           <- install first, always
    ├── 01-core-ops/
    ├── 02-revenue/
    ├── 03-build-ship/
    ├── 04-decision-support/
    ├── 05-knowledge-wiki/
    └── 06-obsidian-companion/   <- bundled MIT-licensed skills, LICENSE file included
```

## Monetization path (per Greyson's direction, 2026-07-15)

1. **Build v1** — done, all 34 skills shipped.
2. **Beta with a friend** — hand it to someone setting up a fresh Obsidian vault from scratch, watch where onboarding breaks, fix it.
3. **Sell online, one-time, $99** — after the beta proves install-and-go works for someone who isn't Greyson and isn't a Krastor client.
4. Longer term: maintained-subscription tier and engagement-bundling stay open as follow-on plays. The $99 one-time sale is the near-term target.

**Open item, not yet resolved:** this product sits close to the TeamBrain Personal Tier spec — both target solo operators. The working differentiation: Operator Stack = the buyer's own vault, own tools, no hosting, sold once. TeamBrain Personal = hosted SaaS with a personal MCP endpoint, subscription. Revisit explicitly before public sale — see TASKS.md.

## Install (for the buyer)

1. Clone `vault-template/` into a new Obsidian vault, or drop its contents into an existing one.
2. Copy `skills/` into the Claude Code / Cowork skills directory.
3. Open Claude in the vault root. On first message, `day-one-setup` fires automatically and interviews the owner — no manual template-filling required.
4. Everything else — memory, business ops, knowledge wiki — works from that point forward without further setup.

## Attribution / licensing notes

- `skills/06-obsidian-companion/` is bundled from kepano/obsidian-skills, MIT licensed. The license notice must ship with the pack — see that folder's `LICENSE-obsidian-skills.md`.
- `skills/05-knowledge-wiki/` implements a general knowledge-compounding pattern (raw sources → maintained wiki → index/log) as original content — no third-party code or text copied in.

## Build log

- **2026-07-15** — v1 architecture defined, foundation layer adapted from Krastor's own vault-prime/context-offload/memory-consolidation/pattern-extraction/vault-hygiene/frontmatter-enforcer. 25 skills shipped across core ops, revenue, build/ship, decision support.
- **2026-07-15 (same day, expansion pass)** — added `day-one-setup` onboarding skill, the `05-knowledge-wiki` category (3 skills), and bundled `06-obsidian-companion` (5 skills from kepano/obsidian-skills, MIT). Pack grew from 25 to 34 skills. Broadened positioning from "solopreneur" to "anyone running a business or standing up their own AI-run operation." See journal entry same 