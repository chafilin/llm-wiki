---
title: TestDino — Flaky Test Benchmark Report 2026
type: source
raw: raw/articles/TestDino — Flaky Test Benchmark Report 2026.md
date_ingested: 2026-05-04
tags: [flaky-tests, benchmarks, data]
---

## Summary
Industry benchmark report synthesizing flakiness rates, root causes, financial impact, and detection methods across major tech companies. Key finding: 84% of Google's pass-to-fail transitions are caused by flaky tests — most flagged failures are false alarms.

## Key takeaways
- Teams experiencing flakiness: 10% (2022) → 26% (2025), a 160% increase
- Google: 16% of tests are flaky; 84% of pass-to-fail transitions are flakes (most failures are false alarms)
- Root causes: async wait 45%, concurrency 20%, test order dependency 12%, resource leak 8%, network 5%
- Financial impact: Microsoft $1.14M/year, Google 2% coding time lost (~$120K/year for 50-dev team)
- Pipeline cascade: 0.01% flaky rate × 4,000 tests = 33% pipeline failure rate; 0.03% = 70%
- Detection methods: manual → retries → historical analysis → AI classification (FlakyGuard: 47.6% repair rate)
- Teams using monitoring tools: 25% fewer flaky reruns
- Microsoft 2-week resolution policy → 18% reduction in 6 months

## Connections
[[Flaky Tests]] [[Testing Philosophy]]
