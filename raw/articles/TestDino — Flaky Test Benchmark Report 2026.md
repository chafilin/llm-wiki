# Flaky Test Benchmark Report 2026: Rates, Root Causes, and Cost Implications

**Source:** https://testdino.com/blog/flaky-test-benchmark/
**Author:** Jashn Jain
**Published:** March 9, 2026

## Flakiness Rates Are Rising

Teams experiencing test flakiness grew from 10% (2022) to 26% (2025) — 160% increase. Pipeline complexity increased 23% in same period. (Bitrise Mobile Insights 2025, 10M+ builds across 3.5 years.)

## Benchmark Rates by Company

| Company | Metric | Value |
|---------|--------|-------|
| Google | Flaky tests in inventory | 16% |
| Google | Flaky test executions | 1.5% |
| Google | Pass-to-fail transitions from flakes | **84%** |
| Atlassian | Jira Frontend master failures | 21% |
| Atlassian | Jira Backend failures | 15% |
| Microsoft | Overall test failures that are flaky | 13% |
| GitHub | Commits with flaky-caused red builds | 9% |

**Key stat:** Google data shows 84% of pass-to-fail transitions are caused by flakes — most flagged failures are false alarms.

## Root Cause Breakdown (Luo et al., FSE 2014)

| Root Cause | % |
|-----------|---|
| Async wait | 45% |
| Concurrency | 20% |
| Test order dependency | 12% |
| Resource leak | 8% |
| Network | 5% |
| Time | 4% |
| Other | 6% |

Nearly half stem from async wait issues — fixed sleeps instead of waiting for conditions.

## Financial Impact

| Metric | Amount |
|--------|--------|
| Microsoft annual cost | $1.14 million |
| Google coding time lost | 2% |
| 50-dev team at 2% loss | $120,000/year |
| Atlassian wasted dev hours/year | 150,000+ |

## Pipeline Cascade Effect

A 0.01% per-test flaky rate across 4,000 tests = 33% pipeline failure probability. At 0.03% across 4,000 tests = 70%.

## Detection Methods (by sophistication)

1. Manual observation
2. Automatic reruns (CI retries 1–3 times)
3. Historical analysis (100+ run patterns)
4. AI-powered classification (FlakyGuard repairs 47.6% of reproducible flaky tests)
5. Platform-level detection (Flakinator: 81% detection rate)

Teams using monitoring tools: 25% fewer flaky reruns.

## Framework Comparison

| | Playwright | Cypress | Selenium |
|--|-----------|---------|----------|
| Built-in auto-wait | Yes (default) | Yes (with retries) | No |
| Flakiness reduction | 50% fewer (from Selenium) | Improved | Historically most brittle |
| Parallel execution | 15–30 via contexts | Paid Cloud | Grid required |

Playwright's auto-wait targets root cause #1 (async wait, 45% of cases).

## Best Practices

1. Measure first — track scores weekly
2. Quarantine, don't delete — define return criteria
3. Fix or remove within timeframe (Microsoft's 2-week policy → 18% reduction in 6 months)
4. Invest in framework prevention (Playwright auto-wait)
5. Use AI-assisted repair
6. Connect to PR workflows
