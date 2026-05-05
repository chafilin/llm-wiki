# Mutation Testing Our JavaScript SDKs — Sentry

**Source:** https://sentry.engineering/blog/js-mutation-testing-our-sdks
**Author:** Lukas Stracke
**Date:** August 23, 2024

## What Mutation Testing Is

Deliberately introduces bugs into code and checks whether tests catch them:
1. Apply mutations (small code modifications)
2. Run tests against each mutant
3. Calculate mutation score (% of detected mutations)

Google research validated the approach by comparing 15 million mutants against real bug-fix PRs.

## Sentry's Test Architecture

- **Unit tests**: Vitest and Jest, per-package
- **Integration tests**: Browser and Node SDKs
- **E2E tests**: Playwright, validating actual SDK payloads

## Tool: StrykerJS

"By far most popular option" for JavaScript mutation testing. Supports per-test coverage analysis and incremental mode.

## Key Challenges

1. **Incomplete coverage picture** — StrykerJS lacks Playwright support; integration/E2E tests excluded
2. **Performance** — Full runs take 35-45 minutes (after Jest→Vitest migration reduced core SDK from 60→25 min)
3. **Framework compatibility** — Node 18+ required after Vitest migration

## Results

Core SDK mutation score: **0.62**

Surviving mutants breakdown:
- ~50% from untested edge cases (warnings, early returns)
- ~50% from uncovered code paths

Higher-level packages showed lower scores despite more E2E/integration tests — unit coverage was lighter.

## Strategy

Weekly scheduled runs (not per-PR) to track score trends via dashboards and alerts. The incomplete picture from missing E2E support is acknowledged.
