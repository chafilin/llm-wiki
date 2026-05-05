---
title: Merge Queue
type: concept
updated: 2026-05-04
---

## Definition
A system that serializes pull requests, merges them into a shadow ("predictive") branch, runs CI there, and only advances master after the merged state passes. Prevents soft conflicts — where two independently-green PRs fail when combined.

## Why it matters
At scale, "PR passed CI on its own branch" is not sufficient to guarantee master stays green. Two PRs can each pass independently but fail when merged together (soft conflict). A merge queue is the systematic answer to this, and it's the only way to maintain the invariant "master is always deployable" without slowing everyone down.

## The three invariants it protects (Shopify)
1. Master always green — deployable at any time
2. Master close to production — limits version drift risk
3. Emergency merges always fast — `/shipit --emergency` bypass exists

[[Successfully Merging the Work of 1000+ Developers]]

## Predictive branch pattern
PRs are merged into a shadow branch in queue order. CI runs on the merged state. Only after CI passes does master advance. This catches soft conflicts before they land. The shadow branch state is maintained with reconciliation (Shopify uses a Virtual DOM analogy: desired state vs. GitHub's actual state).

## Shopify's evolution
- v1 (2018): automated Shipit queue, >90% adoption, branch age + divergence thresholds [[Introducing the Merge Queue — Shopify]]
- v2 (2019): predictive branch, Virtual DOM reconciliation, batch sizes, concurrent batches [[Successfully Merging the Work of 1000+ Developers]]

## Stacked PRs: a different problem
Standard merge queues treat each PR independently. For stacked PRs (dependent PR chains), this is exponentially expensive: each PR needs a fresh rebase + CI run. A 5-PR stack through a standard queue could take 6× longer than necessary.

**Graphite's approach**: run CI once on the full stack head, merge atomically, bisect on failure. 74% faster merges at Ramp. [[Graphite — The First Stack-Aware Merge Queue]]

## Scale limitations of single-queue systems
GitHub's native merge queue: single sequential queue, all PRs wait regardless of independence, no batching, concurrency capped at 100. Becomes a bottleneck beyond 20-30 developers.

**Trunk's additions**: parallel queues (independent changes in separate lanes), batching (3 × 10-min tests → 1 × 10-min batch, 70% savings), optimistic merging, anti-flake protection, 4-tier priority. [[Trunk — Outgrowing GitHub Merge Queue]]

## Architectural correctness: temp branches
A subtle but critical requirement: the actual merge to main must be a normal merge identical to manual merging. Temp branches exist only for CI testing. In 2026, GitHub's merge queue had a regression where temp branches were built from the wrong base (original divergence point instead of current main tip), silently reverting commits that landed on main between the feature branch's creation and the merge. CI passed; the reviewed diff bore no relation to what actually merged. [[Trunk — What Happens If a Merge Queue Builds on the Wrong Commit]]

## Throughput vs. safety tradeoffs
- **Batch size:** more PRs per batch = higher throughput but larger blast radius when CI fails. Shopify settled on 8.
- **Concurrent batches:** running too many simultaneously wastes CI resources when the first batch fails and invalidates later ones. Shopify caps at 3.
- **Continuous CI:** queued PRs run CI continuously while waiting, so they're ready to land immediately when the queue unlocks.

## Flaky test handling
Flaky tests require a probabilistic threshold rather than single-failure ejection. Ejecting a PR from the queue on one failure when the test has a 25% flakiness rate causes constant false positives. Shopify requires 4 consecutive failures before ejection at 25% rate → false positive rate 0.097%. [[Flaky Tests]]

## UX matters
Browser extension → comment-based interface (`/shipit`). Compliance enforced by GitHub branch protection rather than trust. Small change, large impact on adoption.

## Connections
[[Testing Philosophy]] [[Flaky Tests]] [[Software Development]] [[CI Pipeline Speed]] [[Successfully Merging the Work of 1000+ Developers]] [[Keeping Developers Happy with a Fast CI]] [[Introducing the Merge Queue — Shopify]] [[Graphite — The First Stack-Aware Merge Queue]] [[Trunk — Outgrowing GitHub Merge Queue]] [[Trunk — What Happens If a Merge Queue Builds on the Wrong Commit]]
