---
title: Making the Most of Snapshot Testing
type: source
raw: raw/articles/Making the Most of Snapshot Testing.md
date_ingested: 2026-05-04
tags: [snapshots, testing, jest]
---

## Summary
Practical guide to snapshot testing discipline by Sam Hogarth. Core theme: snapshot tests are a liability if too large or indeterminate — value only when they're small, deterministic, and capture something meaningful.

## Key takeaways
- Don't snapshot everything — large snapshots "become undiffable when there's a change"
- Prefer `.toMatchInlineSnapshot()` for small snapshots (stays in test file, visible in review)
- Pass hint strings: `.toMatchSnapshot('button in loading state')` for readable names
- Mock `Date.now()`, `Math.random()` — or use Property Matcher for type validation without exact value
- Custom serializers: `test` + `print` functions for clean, purposeful diffs
- `snapshot-diff`: shows only what changed between two states, not full before/after
- Extends to API contract testing and any serializable data

## Connections
[[Snapshot Testing]]
