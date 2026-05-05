---
title: TestDino — Playwright Flaky Tests
type: source
raw: raw/articles/TestDino — Playwright Flaky Tests.md
date_ingested: 2026-05-04
tags: [flaky-tests, playwright, debugging]
---

## Summary
Practical guide to Playwright-specific flakiness: six root causes, concrete fixes, quarantine patterns. Key insight: 46.5% of flaky tests fail due to CI infrastructure constraints (RAFTs), not code problems.

## Key takeaways
- Six causes: timing/async (45%), shared state/race conditions, environment differences, external dependencies, resource leaks, non-determinism
- RAFTs (Resource-Affected Flaky Tests): 46.5% fail from CI infrastructure constraints, pass locally
- Fix #1 (45% of cases): replace `waitForTimeout` with web-first assertions (`await expect(locator).toBeVisible()`)
- Fix: promise-first pattern for network (`waitForResponse` before action, not after)
- Fix: `page.clock.install()` for deterministic time
- Fix: stable locators (`getByRole('button', {name})` vs `.btn-primary`)
- `--fail-on-flaky-tests` (v1.45+): treats retry-dependent passes as build failures
- Target: <2% flaky rate, <5% failure rate
- Quarantine with tags: `--grep @flaky` (non-blocking separate run) / `--grep-invert @flaky` (main pipeline)

## Connections
[[Flaky Tests]] [[Playwright — Test Sharding]]
