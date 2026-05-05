# Graphite — The First Stack-Aware Merge Queue

**Source:** https://graphite.com/blog/the-first-stack-aware-merge-queue
**Author:** Greg Foster
**Date:** June 2, 2025

## Core Problem

Conventional merge queues treat each PR independently, ignoring dependency chains (stacks). Processing a 5-PR stack through standard infrastructure:
- Each PR requires individual rebasing and CI testing
- Failed tests force eviction of all dependent PRs
- A stack taking 30 min of CI should take 3 hours total with serial processing

## Stack-Aware Solution

Three innovations:

1. **Unified testing** — Run CI once on the complete stack's head, not per-PR
2. **Atomic merging** — Execute all PRs in dependency order after validation passes
3. **Intelligent failure handling** — Binary search (bisection) to isolate problematic changes without evicting unaffected PRs

## Technical Infrastructure

- Distributed locking to prevent concurrent queue corruption
- Speculative execution on temporary branches with parallel CI
- Topology-aware bisection respecting dependency chains
- Partitioned queues for horizontal scaling across monorepos
- Full observability instrumented at every phase

## Reported Results

- 74% faster merges at Ramp
- 7 weekly hours saved per engineer at Asana
- 21% increase in code shipping velocity
