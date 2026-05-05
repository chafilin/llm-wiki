---
title: eslint-plugin-testing-library — prefer-presence-queries
type: source
raw: raw/articles/eslint-plugin-testing-library — prefer-presence-queries.md
date_ingested: 2026-05-04
tags: [eslint, testing-library, test-linting]
---

## Summary
Enforces using `getBy*` for presence assertions and `queryBy*` for absence assertions. Using the wrong query type gives weaker error messages or silently passes when it should fail.

## Key takeaways
- Presence (`toBeInTheDocument()`, `.toBeTruthy()`) → use `getBy*` (throws if not found = better error message)
- Absence (`not.toBeInTheDocument()`, `.toBeNull()`) → use `queryBy*` (returns null = allows assertion to run)
- Invalid: `expect(screen.queryByText('button')).toBeInTheDocument()`
- Valid: `expect(screen.getByText('button')).toBeInTheDocument()`
- Auto-fixable via `eslint --fix`

## Connections
[[Test Linting]]
