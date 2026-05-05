---
title: Playwright — Test Sharding
type: source
raw: raw/articles/Playwright — Test Sharding.md
date_ingested: 2026-05-04
tags: [playwright, testing-tools, ci, parallelism]
---

## Summary
Playwright's built-in sharding documentation. `--shard=x/y` distributes tests across parallel CI machines; blob reporter merges results. Four shards reduce runtime ~75%.

## Key takeaways
- `npx playwright test --shard=1/4` — each shard runs independently
- With `fullyParallel: true`: individual tests distribute evenly across shards (optimal)
- Without `fullyParallel`: entire files assign to shards — requires consistently-sized test files
- Blob reporter: each shard outputs blob, then merge with `npx playwright merge-reports --reporter html ./all-blob-reports`
- GitHub Actions matrices automate shard orchestration

## Connections
[[CI Pipeline Speed]] [[Flaky Tests]]
