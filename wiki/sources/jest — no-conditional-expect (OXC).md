---
title: jest/no-conditional-expect — OXC
type: source
raw: raw/articles/jest — no-conditional-expect (OXC).md
date_ingested: 2026-05-04
tags: [eslint, jest, test-linting, assertion-quality]
---

## Summary
OXC linter documentation for `jest/no-conditional-expect`. Prevents `expect` calls inside conditionals (if, &&/||, catch, promise.catch) — assertions in these paths can be silently skipped.

## Key takeaways
- Flags `expect` in: `if` statements, logical operators, `catch` blocks, promise `.catch()`
- Root problem: "Jest only considers a test to have failed if it throws an error" — conditional assertions may never execute
- Valid: conditionals within assertions (`expect(!value).toBe(false)`), assertions in `finally`

## Connections
[[Test Linting]] [[eslint-plugin-playwright — no-conditional-expect]]
