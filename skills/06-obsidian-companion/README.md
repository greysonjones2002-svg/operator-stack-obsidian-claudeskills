---
category: 06-obsidian-companion
source: kepano/obsidian-skills
license: MIT
---

# Obsidian Companion Skills

These five skills are bundled from [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills) (Steph Ango), MIT licensed. They teach Claude Obsidian's native file formats directly — Obsidian Flavored Markdown (wikilinks, embeds, callouts, properties), Bases (`.base` database views), JSON Canvas (`.canvas` mind maps/flowcharts), the Obsidian CLI, and Defuddle (clean markdown extraction from web pages).

**Attribution requirement:** the MIT license these ship under requires the copyright notice stay attached to the code — `LICENSE-obsidian-skills.md` in this folder is that notice and must ship with the pack. Don't strip it. Selling the bundled pack commercially is explicitly permitted under MIT; removing the license notice is not.

## Why these are in Operator Stack

Every other category in this pack teaches Claude how to run a *business*. This category teaches Claude how to correctly speak *Obsidian's own file formats* — which is what makes the difference between a vault that merely contains markdown files and a vault that actually uses Obsidian's native features (linked graph, Bases table/card views, Canvas boards, properties-driven queries). Without these, Claude tends to write plain markdown that technically works but ignores everything Obsidian does well. With them, the vault this pack ships behaves like a real Obsidian vault, not a folder of text files that happens to open in Obsidian.

## Files

| Skill | What it teaches Claude |
|---|---|
| `obsidian-markdown` | Wikilinks, embeds, callouts, YAML properties/frontmatter, and other Obsidian-specific markdown syntax |
| `obsidian-bases` | `.base` files — database-style table/card views over notes, with filters, formulas, and summaries |
| `json-canvas` | `.canvas` files — visual boards with nodes, edges, and groups (mind maps, flowcharts, project boards) |
| `obsidian-cli` | Command-line interaction with an Obsidian vault, plus plugin/theme development commands |
| `defuddle` | Extracting clean markdown from web pages (used by the knowledge-wiki category's `source-ingest` skill when a source is a URL) |

Unmodified from upstream except for this README. If upstream publishes updates, re-sync from the source repo rather than hand-editing these copies.
