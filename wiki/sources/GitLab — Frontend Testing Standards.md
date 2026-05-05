---
title: GitLab — Frontend Testing Standards
type: source
raw: raw/articles/GitLab — Frontend Testing Standards.md
date_ingested: 2026-05-04
tags: [testing, frontend, gitlab, jest, vue]
---

## Summary
GitLab's opinionated frontend testing guide. Core principle: test user-facing behavior, not implementation details. Covers DOM querying, assertion style, MSW integration tests, snapshot use, and Capybara E2E guidelines.

## Key takeaways
- Don't test library internals (Vue computed props, library behavior)
- DOM queries: prefer `byRole` (accessibility), `findByText`, `data-testid` (kebab-case); avoid `.js-*` classes
- Prefer `toBe` over `toEqual` for primitives; avoid `toBeTruthy`/`toBeFalsy` (too permissive)
- Use `async/await`, not `done` callbacks
- Unexpected console messages fail tests by default
- Faking time: `useFakeDate()`/`useRealDate()` (enabled by default)
- MSW integration tests: mount full Vue app, intercept API with fixture data, interact via native DOM, assert on DOM not Vue state
- Snapshots: sparingly — only for critical HTML structures and complex utility outputs
- Capybara E2E: when multi-component, cross-page, or excessive mocking would be needed in unit tests

## Connections
[[Testing Philosophy]] [[Snapshot Testing]] [[Test Linting]]
