---
title: eslint-plugin-playwright — no-conditional-expect
type: source
raw: raw/articles/eslint-plugin-playwright — no-conditional-expect.md
date_ingested: 2026-05-04
tags: [eslint, playwright, test-linting, assertion-quality]
---

## Summary
Playwright ESLint plugin rule preventing `expect` inside conditional code. Same concept as Jest variant: conditional assertions can be silently skipped, letting tests pass without verifying anything.

## Key takeaways
- Same violations as Jest variant: if statements, logical operators, catch blocks, promise.catch
- Valid: conditionals within assertions, `finally` blocks, Playwright's `expect(foo).rejects.toThrow(Error)`
- Recommended alternative for error testing: wrapper function that guarantees error capture

## Connections
[[Test Linting]] [[jest — no-conditional-expect (OXC)]]
