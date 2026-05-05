---
title: How GitLab Used Parallel CI/CD Jobs to Increase Productivity
type: source
raw: raw/articles/How GitLab Used Parallel CI-CD Jobs to Increase Productivity.md
date_ingested: 2026-05-04
tags: [ci, parallelism, gitlab]
---

## Summary
GitLab's use of the `parallel` keyword and Knapsack gem to reduce a 20-minute frontend-fixtures job. Demonstrates measuring first, then applying targeted parallelization.

## Key takeaways
- Bottleneck: `frontend-fixtures` job (20 min) generating RSpec mock data for frontend tests
- Solution: `parallel: 2` on the fixture job → 20 min → ~17 min for longest-running instance
- Additional 3.5 min saved via Knapsack gem (distributes files by historical timing)
- Total: ~6.5 minutes saved per pipeline
- Process: measure first → identify slow jobs → assess independence → implement + monitor
- Scale: 90+ CI jobs, 500 MR pipelines/day; avg successful MR was 53.8 min in Dec 2020

## Connections
[[CI Pipeline Speed]] [[GitLab — CI-CD Analytics]]
