---
title: Snapshot Testing
type: concept
updated: 2026-05-04
---

## Definition
A testing technique where a value is serialized to a file on first run and compared against that file on subsequent runs. Catches unintended changes in output, but easily misapplied.

## The Critique

The strong industry consensus: **don't snapshot entire component trees**. Problems: [[The Case Against React Snapshot Testing — ezCater]]
1. **Unclear assertion** — entire component renders; diffs show many changes; hard to know what actually broke
2. **Rubber-stamping** — large diffs become impossible to review; developers approve without thinking
3. **Maintenance burden** — fail for unrelated reasons (dependency updates, CSS changes); constant spurious churn
4. ezCater replaced nearly all snapshot tests with focused unit tests after 6 months

## Where Snapshots Legitimately Work

Snapshots are effective when the output is meaningful and small: [[Effective Snapshot Testing — Kent C. Dodds]]
- **Error messages and tool output** — no fragile regex patterns needed
- **Babel plugin AST transformations** — complex AST is hard to assert without snapshots
- **CSS-in-JS style output** — catch regressions in applied styles

## Best Practices

**Keep them small.** Dozens of lines, not hundreds. Large snapshots become undiffable. [[Making the Most of Snapshot Testing]]

**Use inline snapshots** (`.toMatchInlineSnapshot()`) for small cases — stays in the test file, visible in review.

**Name them.** `.toMatchSnapshot('button in loading state')` — tests are documentation.

**Make them deterministic.** Mock `Date.now()`, `Math.random()`. Use Property Matcher syntax for values you want to type-check without pinning exact values.

**Snapshot only the difference.** For before/after state testing, use `snapshot-diff` to show only what changed — not full before/after trees.

**Enforce size limits.** `jest/no-large-snapshots` (default: 50 lines) prevents snapshots from growing silently. [[eslint-plugin-jest — no-large-snapshots Rule]]

## Relation to Test Linting

`jest/no-large-snapshots` bridges snapshot testing and [[Test Linting]] — it's a linting rule specifically for snapshot quality.

## Open questions
- Is there a snapshot size threshold where they become net-harmful vs. net-beneficial?
- What's the right alternative to CSS-in-JS snapshot testing in 2026?

## Connections
[[Testing Philosophy]] [[Test Linting]] [[GitLab — Frontend Testing Standards]] [[Effective Snapshot Testing — Kent C. Dodds]] [[The Case Against React Snapshot Testing — ezCater]] [[Making the Most of Snapshot Testing]] [[eslint-plugin-jest — no-large-snapshots Rule]]
