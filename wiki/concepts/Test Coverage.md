---
title: Test Coverage
type: concept
updated: 2026-05-04
---

## Definition
A measure of which lines/branches/functions in a codebase are executed during tests. Often misapplied as a target rather than a diagnostic tool.

## Patch Coverage vs. Project Coverage

**Project coverage** — percentage of all lines covered across the entire codebase. Chasing 100% is unrealistic and burdensome; much legacy code isn't worth testing.

**Patch coverage** — coverage of lines changed in a specific PR. The right enforcement point: "a developer should test their own code versus test all of the code." Every new line introduced should be tested. [[Codecov — Why Patch Coverage Matters More]]

## Coverage as Culture, Not Metric

Apollo grew frontend coverage from 24% to ~50% over 6 months with near-zero mandates. The lever: visibility. Nightly Grafana dashboards per team, weekly comparisons, missing coverage reports listing zero-coverage files by team. [[Beyond Numbers — Test Coverage Culture at Apollo]]

Key principle: **track direction, not position**. A team at 35% trending up outperforms one at 55% trending down. Celebrate delta, enforce minimally.

Enforcement: any coverage >0% triggers a pass (not 80%). Escape hatches (`// code-coverage-ignore`, PR label) reduce friction and drive adoption. Progressive rollout: informational → opt-in → universal.

## Quality Gates

Automated enforcement that blocks PRs when coverage drops below thresholds. [[SonarQube — Introduction to Quality Gates]]

SonarQube "Sonar way" gate on new code: ≥80% coverage, ≤3% duplication, no new bugs/vulnerabilities. Fudge factor: conditions ignored until ≥20 new lines (prevents disproportionate impact on tiny changes).

Codecov provides three status check types: project (overall), patch (PR-level), and changes (unexpected fluctuations). [[Codecov — Commit Status Checks]]

## Monorepo: Carryforward Flags

Generating full coverage for every commit is too expensive at monorepo scale. Carryforward flags: upload coverage for only the changed application/package; others persist from previous uploads. [[Compass — Code Coverage and Carryforward Flags]]

## Tooling

- **Vitest**: v8 (default) or Istanbul provider; threshold enforcement per-file or globally; `coverage.changed` for PR-scope-only measurement [[Vitest — Coverage Config]]
- **Codecov**: patch + project + changes status checks; carryforward flags for monorepos
- **SonarQube**: quality gates with new-code focus
- **Istanbul/nyc**: traditional Node.js coverage

## Open questions
- When does coverage become a metric that gets gamed (people writing tests to hit numbers, not catch bugs)?
- How to measure coverage meaningfully for E2E tests vs. unit tests?

## Connections
[[Testing Philosophy]] [[Software Development]] [[Mutation Testing]] [[Beyond Numbers — Test Coverage Culture at Apollo]] [[Codecov — Why Patch Coverage Matters More]] [[Codecov — Commit Status Checks]] [[Compass — Code Coverage and Carryforward Flags]] [[SonarQube — Introduction to Quality Gates]] [[Vitest — Coverage Config]]
