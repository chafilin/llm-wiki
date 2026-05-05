---
title: Datadog — Working with Flaky Tests
type: source
raw: raw/articles/Datadog — Working with Flaky Tests.md
date_ingested: 2026-05-04
tags: [flaky-tests, tooling, datadog]
---

## Summary
Datadog Test Optimization documentation for flaky test tracking. Provides per-test metrics (duration, flaked dates, commits affected, failure rate, trend) and three tag categories (flaky, new flaky, known flaky).

## Key takeaways
- Three tags: `is_flaky` (active), `is_new_flaky` (recently introduced), `is_known_flaky` (previously identified — may indicate test instability vs. code issue)
- Key metrics: average duration, first/last flaked dates, commits affected, failure rate, trend
- Tests inactive 30 days auto-removed from tracking; reappear if flakiness recurs
- Manual removal via trash icon per commit to ignore mistakenly-flagged tests

## Connections
[[Flaky Tests]]
