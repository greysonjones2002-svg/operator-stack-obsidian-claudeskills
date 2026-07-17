# Knowledge Wiki Log

Append-only chronological record of ingest/query/lint activity. Each entry starts with a consistent
prefix so it stays parseable with plain-text tools (e.g. `grep "^## \[" log.md | tail -5` for the
last 5 entries).

Format:

```
## [YYYY-MM-DD] ingest | Source Title
Brief note on what was added/updated and which wiki pages touched.

## [YYYY-MM-DD] query | Question asked
Brief note on what was answered and whether it got filed back as a new page.

## [YYYY-MM-DD] lint | Pass summary
Brief note on what the health check found and fixed vs. flagged.
```

---
