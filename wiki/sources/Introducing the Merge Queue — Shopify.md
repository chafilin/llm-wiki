---
title: Introducing the Merge Queue — Shopify
type: source
raw: raw/articles/Introducing the Merge Queue — Shopify.md
date_ingested: 2026-05-04
tags: [merge-queue, ci, shopify]
---

## Summary
Shopify's 2018 account of introducing the first version of their merge queue. Describes the problem (developers competing to merge in narrow windows), the automated Shipit queue solution, and unsafe commit management via manual flagging + automatic revert detection.

## Key takeaways
- Context: 600,000+ merchants, trunk-based development, competitive pressure to merge
- Solution: automated queue in Shipit; developers enqueue PRs without leaving GitHub; >90% adoption
- Queue enforces: branch age thresholds, commit divergence limits, waits for CI before merging
- Unsafe commits: manually flagged or auto-detected via revert detection
- This is v1 — the simpler predecessor to the predictive branch approach from 2019
- See [[Successfully Merging the Work of 1000+ Developers]] for the evolved architecture

## Connections
[[Merge Queue]] [[Successfully Merging the Work of 1000+ Developers]] [[Software Development]]
