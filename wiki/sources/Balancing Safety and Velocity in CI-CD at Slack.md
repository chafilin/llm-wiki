---
title: Balancing Safety and Velocity in CI/CD at Slack
type: source
raw: raw/articles/Balancing Safety and Velocity in CI-CD at Slack.md
date_ingested: 2026-05-04
tags: [flaky-tests, ci, testing-architecture]
---

## Summary
Slack's Webapp monorepo went from p95 test turnaround >30 minutes and ~50% of PRs hitting a flaky test, to <18 minutes and <5% flakiness. The key was a three-tier pipeline (pre-merge/post-merge/regression) that placed only critical tests in the blocking path.

## Key takeaways
- Scale: 1 million test suites daily, up to 40,000 tests per suite, growing 10% monthly since 2017
- Even <1% flake rate × 60 suites = ~55% of PRs see failures — multiplication effect
- Three-tier solution: pre-merge (<1% of E2E, must pass), post-merge (<10%, can block deploys), regression (rest, batch bi-hourly)
- Results: turnaround decreased >40% (consistently <18 min), flakiness decreased >90% (<5%)
- No measurable increase in customer-reported defects
- Finite state machine triage: 2 consecutive failures → alert → 4 liaisons → infra/flakiness distinguished before involving dev
- Human workflows had to change alongside technical changes

## Connections
[[Flaky Tests]] [[Testing Philosophy]] [[Software Development]]

## Quotes
> "Even <1% flake rate per suite × 60 suites = ~55% of PRs see failures"
