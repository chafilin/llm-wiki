---
title: eslint-plugin-jest — no-large-snapshots Rule
type: source
raw: raw/articles/eslint-plugin-jest — no-large-snapshots Rule.md
date_ingested: 2026-05-04
tags: [eslint, jest, snapshots, test-linting]
---

## Summary
ESLint rule that limits snapshot size (default: 50 lines) to keep them reviewable. Large snapshots become rubber-stamped during code review.

## Key takeaways
- Default: 50 lines max for external snapshots; `inlineMaxSize` defaults to `maxSize`
- `allowedSnapshots`: per-file allowlist by snapshot name or regex pattern
- Requires `ecmaVersion: 2015` (snapshots use template literals)
- "A stored snapshot is only as good as its review"

## Connections
[[Test Linting]] [[Snapshot Testing]]
