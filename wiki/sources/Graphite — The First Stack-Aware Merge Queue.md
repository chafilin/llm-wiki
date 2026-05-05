---
title: Graphite — The First Stack-Aware Merge Queue
type: source
raw: raw/articles/Graphite — The First Stack-Aware Merge Queue.md
date_ingested: 2026-05-04
tags: [merge-queue, stacked-prs, ci]
---

## Summary
Graphite's blog post announcing the first merge queue designed for stacked pull requests (dependent PR chains). Standard merge queues treat each PR independently; processing a 5-PR stack this way takes ~6× longer than necessary. Graphite tests CI once on the complete stack head and merges atomically.

## Key takeaways
- Standard queues process each PR of a stack independently: fresh rebase + CI per PR → exponential delays
- Three innovations: unified CI on full stack head, atomic sequential merge, binary-search bisection on failure
- Infrastructure: distributed locking, speculative execution on temp branches, topology-aware bisection, partitioned queues for monorepos
- Results: 74% faster merges at Ramp, 7 hrs/week/engineer saved at Asana, 21% more code shipped

## Connections
[[Merge Queue]]
