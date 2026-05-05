---
title: Test Budget — Time Constrained CI Feedback — Shopify
type: source
raw: raw/articles/Test Budget — Time Constrained CI Feedback — Shopify.md
date_ingested: 2026-05-04
tags: [ci, test-selection, shopify]
---

## Summary
Shopify's research into smart test prioritization within their 170,000+ test suite. By reordering tests using historical data (failure rate, duration, churn, coverage, complexity), they can surface 80% of failures after running only 60% of selected tests.

## Key takeaways
- Two-part system: test selection (deterministic) + test prioritization (historical data ordering)
- Six criteria: failure rate, execution duration, code churn, coverage, complexity, random baseline
- Best criterion: failure_rate — detects 80% of failures after 60% of tests
- Overall: found failures after running only 70% of the test-selection suite
- Median Time to First Failure: under 5 minutes
- Insight: you don't need to run all tests to get confident feedback

## Connections
[[CI Pipeline Speed]] [[Spark Joy by Running Fewer Tests — Shopify]]
