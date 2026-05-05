# Beyond Numbers: Turning Test Coverage into a Culture We Track, Enforce, and Improve

**Source:** https://www.apollo.io/tech-blog/beyond-numbers-turning-test-coverage-into-a-engineering-culture
**Author:** Jitesh Badgujar
**Date:** April 14, 2026

## The Starting Point

Apollo: 30+ engineering squads, frontend unit test coverage at 24% and declining. Problem: bug counts and incident rates are lagging indicators. Test coverage answers: which code lacks a safety net?

## What They Track

- Frontend: Unit tests (Vitest), E2E (Playwright), Chrome extension (WebdriverIO)
- Backend: RSpec coverage
- **Coverage Delta** — weekly/monthly/sprint changes. "A team at 35% trending upward outperforms one at 55% declining by 4 points."

## Grafana Dashboard

Nightly CI runs feed a unified Grafana dashboard. Every team's frontend unit, E2E, and backend coverage — broken down by team with weekly comparisons. Green = improving, red = declining.

Teams review bi-weekly in quality sessions + monthly engineering reviews.

## Missing Coverage Report

Lists every zero-coverage file grouped by team and directory. Filter by coverage range (0%, 1–20%, 21–40%). HTML reports stored on GCP. Transformed "you're at 45%" into "these 14 files in your design-system package lack coverage."

## PR-Level Enforcement

Custom TypeScript script analyzes coverage JSON, posts PR comments identifying: new files with zero coverage, partial coverage, E2E-only coverage. E2E coverage accepted as valid (real user behavior > heavily mocked unit tests).

**Enforcement phases:**
- Phase 0: Built coverage calculation
- Phase 1: PR comments (informational, non-blocking)
- Phase 2: Teams opt in to enforcement
- Phase 3: Company-wide enforcement
- Phase 4: Modified file coverage checks (upcoming)

**Escape hatches:** `// code-coverage-ignore` comments, `disable_coverage_enforcement` PR label for urgencies.

**Any coverage above 0% passes** — not 80%, not 100%. Focus on critical paths.

## Scaling Coverage Without Slowing CI

- Knapsack Pro for balanced parallelization
- Automated flaky-test reporting → Jira tickets
- Automated slow-test reporting

## Dead Code Removal

Backend: "Tombstones" (30-day production trigger checking). Frontend: Knip for unused files/exports. Single cleanup pass removed 4,000+ lines → ~5% coverage increase.

## Three-Tier System (No Hard Threshold)

| Tier | Range | Meaning |
|------|-------|---------|
| 🟢 Healthy | >70% | Maintain and celebrate |
| 🟡 Satisfactory | 40–70% | Room to grow, not urgent |
| 🔴 Needs Attention | <40% | Discuss blockers |

## Results (6 months)

| Metric | Before | After |
|--------|--------|-------|
| FE Unit Test Coverage | ~24% | ~50% |
| Teams with Declining Coverage | 60% | 8% |
| Teams Opted Into Enforcement | 0 | All |
| Weekly PRs Blocked | 0 | ~10 |

~35% reduction in high-severity production incidents over one year.

## Key Takeaways

- Visibility beats mandates — dashboards drove behavior change more than policies
- Direction over position — celebrate delta, not absolute numbers
- Low friction, high adoption — any coverage > 0% passes
- Weekly cadence is essential
- AI accelerates testing (test generation tools lowered activation energy)
