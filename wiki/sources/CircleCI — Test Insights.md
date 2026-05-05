---
title: CircleCI — Test Insights
type: source
raw: raw/articles/CircleCI — Test Insights.md
date_ingested: 2026-05-04
tags: [flaky-tests, ci, circleci, tooling]
---

## Summary
CircleCI Test Insights documentation. Surfaces flaky test detection, failure patterns, and slowest tests across the 100 most recent pipeline runs. Uses a 14-day window to identify tests that both passed and failed on the same commit.

## Key takeaways
- Detection: tests that pass and fail on the same commit within a 14-day window → labeled `FLAKY`
- Surfaces: most failed tests (100 by lowest success rate), slowest tests (100 by longest runtime)
- Per-run view: test count, skipped count, success rate on hover
- Requires OAuth authentication (GitHub, Bitbucket)

## Connections
[[Flaky Tests]] [[CI Pipeline Speed]]
