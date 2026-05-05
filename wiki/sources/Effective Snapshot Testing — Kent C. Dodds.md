---
title: Effective Snapshot Testing — Kent C. Dodds
type: source
raw: raw/articles/Effective Snapshot Testing — Kent C. Dodds.md
date_ingested: 2026-05-04
tags: [snapshots, testing, jest]
---

## Summary
Kent C. Dodds' measured take on snapshot testing (2017). Acknowledges their real problems while identifying specific contexts where they provide genuine value: error messages, Babel AST, CSS-in-JS. The key rule: keep them small and purposeful.

## Key takeaways
- Valid uses: error messages/logs (no fragile regex), Babel plugin AST, CSS-in-JS styling
- Problems: intent unclear → failures hard to diagnose; generated files encourage insufficient review; high false-negatives erode trust; teams regenerate instead of investigating
- Large snapshots (>640 lines) amplify all problems
- Recommendations: keep small (dozens of lines), use custom serializers, use snapshot-diff for state changes

## Connections
[[Snapshot Testing]]
