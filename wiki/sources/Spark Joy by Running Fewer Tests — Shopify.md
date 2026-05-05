---
title: Spark Joy by Running Fewer Tests — Shopify
type: source
raw: raw/articles/Spark Joy by Running Fewer Tests — Shopify.md
date_ingested: 2026-05-04
tags: [ci, test-selection, shopify, dynamic-analysis]
---

## Summary
Shopify's dynamic analysis approach to test selection in their 150,000+ test Rails monolith. Method-call logging during test execution builds call graphs mapping which files each test exercises. Result: 60% of tests needed per build, 99.94% recall rate, ~25% infrastructure cost reduction.

## Key takeaways
- Problem: 150,000+ tests, 30-40 min parallel, 20-30% annual growth
- Dynamic analysis: log method calls → build per-test call graphs → select only tests touching modified files
- Recall rate: 99.94% (8,355/8,360 failing tests detected)
- Selection rate: ~60% of tests; 40% of builds needed <20% of tests
- Infrastructure cost savings: ~25%
- Challenges: non-Ruby assets needed custom patches; metaprogramming needed glob-rule detection
- Fallback: run all modified-file tests + mapped tests (handles mapping lag)

## Connections
[[CI Pipeline Speed]] [[Test Budget — Time Constrained CI Feedback — Shopify]] [[Software Development]]
