---
title: Keeping Developers Happy with a Fast CI
type: source
raw: raw/articles/Keeping Developers Happy with a Fast CI.md
date_ingested: 2026-05-04
tags: [ci, performance, shopify, test-selection, instrumentation]
---

## Summary
Shopify's test infrastructure team reduced p95 CI time from 45 minutes to 18 minutes on a 170k-test monolith. The method: measure everything first (scatter plot of frequency × duration), then eliminate work rather than optimize it. The biggest wins came from fixing Docker I/O, hash-based skipping of unchanged steps, and test selection.

## Key takeaways
- Measure before touching anything. A frequency × duration scatter plot immediately surfaces true bottlenecks — assumptions were wrong (it was disk I/O, not CPU).
- "The fastest code is the code that doesn't run": skip database migrations and asset compilation via MD5 hashing when inputs haven't changed — cuts that phase from 5min to 3min.
- Test selection (run only tests mapped to changed files) raised builds avoiding full test runs from 45% to 60%+; test stability went from 88% to 97%.
- Docker I/O was the hidden culprit: 10GB+ cached dirs caused memory pressure; read-only shared caches cut p95 startup from 90s to 25s.
- 80/20 on slow tests: a small number of outlier tests (one that hung regularly) disproportionately blow p95 times. Fix or disable them.
- Sustained CI speed requires ongoing monitoring — it degrades without investment.

## Connections
[[Merge Queue]] [[Flaky Tests]] [[Testing Philosophy]] [[Software Development]]
