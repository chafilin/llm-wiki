---
title: eslint-plugin-jest — expect-expect Rule
type: source
raw: raw/articles/eslint-plugin-jest — expect-expect Rule.md
date_ingested: 2026-05-04
tags: [eslint, jest, test-linting, assertion-quality]
---

## Summary
Documentation for the `jest/expect-expect` rule. Triggers when a test contains no assertion call, preventing tests that silently pass while validating nothing.

## Key takeaways
- Rule: `jest/expect-expect` — triggers when test has no `expect` call
- `assertFunctionNames`: add custom assertion functions (supports wildcards like `request.**.expect`)
- `additionalTestBlockFunctions`: for non-standard test block wrappers (e.g., `theoretically`)
- Default matches `expect` only — configure to include SuperTest, custom assertion libraries, etc.

## Connections
[[Test Linting]]
