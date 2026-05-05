---
title: Taming Test Flakiness — Atlassian
type: source
raw: raw/articles/Taming Test Flakiness — Atlassian.md
date_ingested: 2026-05-04
tags: [flaky-tests, tooling, ml]
---

## Summary
Atlassian built Flakinator — an internal platformized tool for detecting, quarantining, and tracking flaky tests across 12+ products. It handles 350M+ test executions daily and combines retry-based detection, Bayesian inference scoring, automated Jira/Slack integration, and ownership-based assignment.

## Key takeaways
- Flaky tests caused 21% of Jira Frontend master failures, 15% of backend — wasting 150,000+ dev hours/year
- Flakinator replaced a manual file-based system: detects, quarantines, tracks, auto-assigns owners
- Two detection algorithms: RETRY (fail-then-pass = flaky, 81% detection rate) + Bayesian inference (moving window, multi-signal score 0–1)
- Lifecycle: detect → find owner via code ownership → create Jira with deadline → Slack notification → quarantine → measure health → re-enable when healthy
- Recovered 22,000+ builds, identified 7,000 unique flaky tests
- Lessons: data quality matters; combine algorithms (no single method is universal); developer experience drives adoption

## Connections
[[Flaky Tests]] [[Testing Philosophy]]
