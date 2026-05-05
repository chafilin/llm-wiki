# Balancing Safety and Velocity in CI/CD at Slack

**Source:** https://slack.engineering/balancing-safety-and-velocity-in-ci-cd-at-slack/
**Authors:** Carlos Valdez, Frank Chen
**Date:** February 18, 2022 (Updated August 23, 2022)

## The Problem (2020)

Slack's Webapp monorepo:
- p95 test turnaround: consistently >30 minutes
- Flakiness per PR: ~50% of PRs hit at least one flaky test
- Scale: 1 million test suites daily, up to 40,000 tests per suite
- Test count growing 10% monthly since 2017

Root causes: infra strain from cascading failures, tests not updated until fully broken, no clear escalation paths. Even <1% flake rate per suite × 60 suites = ~55% of PRs see failures.

## Three-Tier Pipeline Solution

**Pre-merge:** <1% of E2E tests. Must pass. High-criticality features only.

**Post-merge:** <10% of E2E tests. Runs after mainline merge. Medium-criticality, can block deploys.

**Regression:** Remaining E2E tests. Batch execution, bi-hourly cadence, low-criticality.

## Results

- Test turnaround: decreased >40%, now consistently <18 minutes
- Flakiness: decreased >90%, now consistently <5%
- No measurable increase in customer-reported defects

## Triage and Alert Strategy

Finite state machine approach:
1. Detection: 2+ consecutive failures trigger alert
2. Escalation: 4 liaisons engaged — triage engineer, test suite owner, PR developer, deploy commander
3. Automation: Slack bots create failure-specific channels, auto-notify parties
4. Prioritization: infra/flakiness issues distinguished from real code problems before involving developers

## Key Lessons

- Infrastructure itself contributed to flakiness (timeouts, dependency failures)
- Success required coordination across 12 teams to define critical tests
- Observability: identifying specific commits causing failures enabled targeted fixes
- Technical changes required corresponding human workflow redesigns
