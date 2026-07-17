---
name: frontmatter-standard
description: >
  Stamps standardized YAML frontmatter on every note written to the vault. Fires automatically after
  capture-everything, or any other skill, creates or modifies a vault file. Also triggers on "fix
  frontmatter," "standardize metadata," "tag these," or any request to clean up note headers. The
  vault's searchability depends on consistent metadata — a note without it is a note pattern-radar
  and operator-prime can't find efficiently.
---

# Frontmatter Standard

## The standard

Every note in `memory/`, `journal/`, and any client/project folder gets YAML frontmatter at the top:

```yaml
---
type: [client | person | project | context | journal | glossary]
updated: YYYY-MM-DD
tags: [optional, relevant, tags]
---
```

Client and project files add:

```yaml
status: [active | inactive | prospect | complete]
```

Person files add:

```yaml
role: [client | contractor | vendor | partner | other]
```

## When to apply it

- Any time a new file gets written by any skill in this pack — stamp frontmatter as part of
  creating it, don't leave it for a later cleanup pass.
- Any time an existing file is substantively edited — update the `updated:` date.
- During a `vault-hygiene` pass, for any file found missing it.

## Why this matters more than it looks like

Frontmatter is what makes `type:`, `status:`, and `tags:` queryable — in Obsidian directly (via
search or the Bases/Dataview-style plugins if installed) and by Claude when scanning the vault for
relevant context. A vault full of notes with inconsistent or missing metadata degrades every other
skill in this pack: `operator-prime` has to guess what's current, `pattern-radar` can't reliably
group entries, `vault-hygiene` can't tell what's stale. This is a small, boring skill that everything
else quietly depends on.
