---
title: CircleCI — Boost Build Time with Test Parallelism
type: source
raw: raw/articles/CircleCI — Boost Build Time with Test Parallelism.md
date_ingested: 2026-05-04
tags: [ci, circleci, parallelism, test-splitting]
---

## Summary
Amio's account of reducing integration test time from ~15 min to ~9 min using CircleCI's `parallelism` key and `--split-by=timings`. The tool distributes test files across containers using historical timing data.

## Key takeaways
- `parallelism: N` alone runs ALL tests on each container — must combine with splitting
- `circleci tests glob "src/integration-test/**/*.groovy" | circleci tests split --split-by=timings`
- `--split-by=timings` uses CircleCI's historical timing data; container indexing is automatic
- Gradle integration: pass split results as `testFilter` property; filter `.class` files from `.groovy` paths
- Result: ~15 min → ~9 min

## Connections
[[CI Pipeline Speed]]
