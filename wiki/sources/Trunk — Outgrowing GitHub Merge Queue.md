---
title: Trunk — Outgrowing GitHub Merge Queue
type: source
raw: raw/articles/Trunk — Outgrowing GitHub Merge Queue.md
date_ingested: 2026-05-04
tags: [merge-queue, github, ci]
---

## Summary
Trunk's comparison of GitHub's native merge queue vs. Trunk's enterprise-grade alternative. GitHub's queue works for small teams but hits fundamental limitations at scale: single sequential queue, no batching, 100-concurrency cap.

## Key takeaways
- GitHub MQ problems at scale: all PRs wait sequentially regardless of independence; CI runs twice (branch + merge group) with no batching; concurrency capped at 100
- Trunk additions: parallel queues (route independent changes through separate lanes), batching (3 10-min tests → 1 10-min test, 70% savings), optimistic merging, anti-flake protection
- Priority system: 4 tiers (urgent interrupts running jobs)
- Bottom line: "GitHub merge queue was a great first step" but a bottleneck beyond 20-30 developers

## Connections
[[Merge Queue]]
