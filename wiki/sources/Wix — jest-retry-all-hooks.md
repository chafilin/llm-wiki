---
title: Wix — jest-retry-all-hooks
type: source
raw: raw/articles/Wix — jest-retry-all-hooks.md
date_ingested: 2026-05-04
tags: [jest, flaky-tests, testing-tools]
---

## Summary
Open-source Jest patch by Wix that makes `beforeAll`/`afterAll` hooks work correctly with `jest.retryTimes`. By default these hooks don't re-run when tests retry; this package converts them to smart `beforeEach`/`afterEach` equivalents that re-run on failure.

## Key takeaways
- `beforeAll` → runs on first execution and again if previous test failed
- `afterAll` → runs after each test, especially on failure
- Requires `jest-environment-emit` as peer dependency
- Compatible with jest-metadata, jest-allure2-reporter, Detox

## Connections
[[Flaky Tests]]
