# Trunk — Outgrowing GitHub Merge Queue

**Source:** https://trunk.io/blog/outgrowing-github-merge-queue
**Author:** Sam Gutentag
**Date:** September 3, 2025

## Problems with GitHub Merge Queue at Scale

1. **Single queue bottleneck** — All PRs wait sequentially regardless of independence. "A documentation fix waits behind a complex backend refactor."
2. **CI cost inefficiency** — PRs run tests twice (branch + merge group) with no batching, doubling costs.
3. **Limited visibility** — No clear transparency into concurrent operations or failure attribution.
4. **Configuration constraints** — Build concurrency capped at 100; limited merge strategies.

## What Trunk Offers

### Parallel Queues
Dynamic queue splitting analyzes impacted targets to route independent changes through separate lanes simultaneously.

### Batching
Groups compatible PRs for single test runs. Three 10-minute tests become one 10-minute batch (70% savings). Auto-bisection identifies problematic PRs on batch failure.

### Optimistic Merging
Ready PRs merge immediately without waiting for earlier PRs still in testing, provided they've been tested against anticipated main-branch state.

### Anti-Flake Protection
Auto-detects and quarantines flaky tests with intelligent retry logic.

### Priority System
Four tiers (urgent/high/medium/low) — urgent interrupts running jobs; others reorder without full rebuilds.

## Feature Comparison

| Feature | GitHub | Trunk |
|---------|--------|-------|
| Queue structure | Single sequential | Multiple parallel |
| Testing model | One PR per test | Batch multiple PRs |
| Failure handling | Full rebuild | Auto bisection |
| Concurrency limit | 100 | Configurable |
| Flaky test handling | Manual | Auto-detect & quarantine |

## Bottom Line

"GitHub's merge queue was a great first step" but becomes a bottleneck beyond 20-30 developers.
