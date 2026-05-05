---
title: The Unreasonable Effectiveness of Test Retries — Shopify
type: source
raw: raw/articles/The Unreasonable Effectiveness of Test Retries — Shopify.md
date_ingested: 2026-05-04
tags: [flaky-tests, mobile, retries, android]
---

## Summary
Shopify Android monorepo case study showing that strategic test retries, rather than root-cause-only fixes, dramatically improved pipeline reliability. With 99.95% individual test reliability across 100-test pipelines × 20 pipelines, overall pass rate was ~35%; one retry per test raised this to 99.95%.

## Key takeaways
- Math of flakiness: 0.9995^100 × 20 pipelines = ~35% overall pass rate; one retry = 99.95%
- Three failure categories: retriable (env setup, Docker, git), fatal (full reload needed), flaky tests (retry up to 3×)
- Screenshot tests identified as particularly unreliable
- Android: 31% → ~90%; iOS: 67% → 97% after retries
- Retries don't replace fixing root causes — notify developers when tests need retries
- Beyond retries: reduce unreliable component dependencies, enhance reliability, implement caching

## Connections
[[Flaky Tests]] [[Testing Philosophy]]

## Quotes
> "A slightly slower build is preferable over manual retries"
