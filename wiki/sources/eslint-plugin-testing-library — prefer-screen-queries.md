---
title: eslint-plugin-testing-library — prefer-screen-queries
type: source
raw: raw/articles/eslint-plugin-testing-library — prefer-screen-queries.md
date_ingested: 2026-05-04
tags: [eslint, testing-library, test-linting]
---

## Summary
Enforces using `screen` for DOM queries instead of destructuring from `render()`. `screen.getByText()` vs `const { getByText } = render(...)`.

## Key takeaways
- `screen.getByText('foo')` preferred over `const { getByText } = render(...); getByText('foo')`
- Reason: better autocomplete, simpler per-test maintenance, consistent interface
- Valid exceptions: queries chained to `within()`, custom queries not on screen, `container`/`baseElement` options

## Connections
[[Test Linting]]
