---
title: Successfully Merging the Work of 1000+ Developers
type: source
raw: raw/articles/Successfully Merging the Work of 1000+ Developers.md
date_ingested: 2026-05-04
tags: [ci, merge-queue, monolith, scale, shopify, flaky-tests]
---

## Summary
Shopify's account of building a merge queue for 1000+ developers on a monolith. The core problem: at scale, PRs that individually pass CI can fail when merged together ("soft conflicts"), and the naive solution of just batching makes master drift too far from production. The solution is a predictive branch that runs CI on the merged state before anything touches master.

## Key takeaways
- Three non-negotiable invariants: master always green, master close to prod, emergency merges always fast.
- "Predictive branch" pattern: PRs are merged into a shadow branch first; CI runs there; only after passing does master advance.
- Queue state managed with a Virtual DOM-style reconciliation — desired state vs. GitHub's actual state.
- Flaky tests handled probabilistically: with 25% known flakiness, require 4 consecutive failures before ejecting from queue → false positive rate drops to 0.097%.
- Batching sweet spot: 8 PRs per deployment; only 3 batch windows run CI simultaneously to cap cost.
- `/shipit` comment interface > browser extension — branch protection enforces compliance.

## Connections
[[Merge Queue]] [[Flaky Tests]] [[Testing Philosophy]] [[Software Development]]

## Quotes
> "Master must always be green, master must stay close to production, emergency merges must be fast."
