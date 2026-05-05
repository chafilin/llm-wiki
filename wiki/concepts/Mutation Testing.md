---
title: Mutation Testing
type: concept
updated: 2026-05-04
---

## Definition
A technique that evaluates test suite quality by deliberately introducing small bugs (mutants) into the code and checking whether tests catch them. "Tests the tests." Outputs a mutation score: percentage of mutants killed.

## Why It Matters

Code coverage tells you which lines were executed, not whether the tests would catch a bug on those lines. A test that calls a function but never asserts the result will show 100% coverage but 0% mutation score on that function.

Google research validated the approach by comparing 15 million mutants against real bug-fix pull requests — mutants closely approximate real bugs.

## How It Works

1. Apply a mutation (e.g., `>` → `>=`, `+` → `-`, remove a condition)
2. Run the test suite against the mutated code
3. If tests fail: mutant killed ✓. If tests pass: mutant survived ✗
4. Score = killed / total

## StrykerJS

The standard tool for JavaScript/TypeScript mutation testing. Supports Jest, Vitest, Mocha, and others. Key optimizations:

**Incremental mode** — tracks code/test changes and only re-runs mutations for what changed. Real example: 3,731 of 3,965 results reused (only 234 new runs needed). [[StrykerJS — Announcing Incremental Mode]] [[StrykerJS — Incremental Mode Docs]]

**TypeScript checker** — validates mutants against TypeScript types before running tests. Prunes mutants that TypeScript would reject, eliminating wasted test cycles. [[StrykerJS — TypeScript Checker]]

## Practical Limitations

- **E2E/integration tests not supported** — StrykerJS can't instrument Playwright or integration test runs. Mutation score reflects only unit test quality; overall test protection is likely higher than the score suggests. [[Mutation Testing Our JavaScript SDKs — Sentry]]
- **Runtime** — full runs take 35-45 minutes at moderate scale; incremental mode mitigates this
- **Score is not a goal** — 0.62 is not "bad" if the surviving mutants are in trivially-tested edge cases

## Practical Use

Run weekly, not per-PR (too slow). Track score trend over time. Use as a diagnostic to identify specific gaps, not as a pass/fail gate. [[Mutation Testing Our JavaScript SDKs — Sentry]]

## Open questions
- At what codebase size does full mutation testing become infeasible even with incremental mode?
- Can mutation score be used as a PR gate for high-risk modules only?

## Connections
[[Testing Philosophy]] [[Test Coverage]] [[Mutation Testing Our JavaScript SDKs — Sentry]] [[StrykerJS — Announcing Incremental Mode]] [[StrykerJS — Incremental Mode Docs]] [[StrykerJS — TypeScript Checker]] [[StrykerJS — Incremental Mode (GitHub)]]
