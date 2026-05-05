---
title: eslint-plugin-testing-library — no-debugging-utils
type: source
raw: raw/articles/eslint-plugin-testing-library — no-debugging-utils.md
date_ingested: 2026-05-04
tags: [eslint, testing-library, test-linting]
---

## Summary
Bans Testing Library debugging utilities from committed code. Same principle as removing `console.log` — debug helpers left in tests pollute output and indicate unfinished work.

## Key takeaways
- Banned: `debug`, `logTestingPlaygroundURL`, `prettyDOM`, `logRoles`, `logDOM`, `prettyFormat`
- Default severity: `warn` (Angular, Marko, React, Svelte, Vue)
- `utilsToCheckFor` option: selectively enable/disable specific utilities
- "debug statements also pollutes the tests if one of your teammates forgot to remove it"

## Connections
[[Test Linting]]
