---
title: StrykerJS — Incremental Mode Docs
type: source
raw: raw/articles/StrykerJS — Incremental Mode Docs.md
date_ingested: 2026-05-04
tags: [mutation-testing, strykerjs, performance]
---

## Summary
Official StrykerJS documentation for incremental mode. Covers configuration options, test runner support levels, limitations, and when to force reruns.

## Key takeaways
- Config: `--incremental`, `--incrementalFile` (default: reports/stryker-incremental.json), `--force`
- Limitations: doesn't detect env changes, dep updates, `.snap` file changes, non-mutated file changes
- Test runner support: Jest/CucumberJS = full; Mocha/Vitest/Tap = per-file (no location); Jasmine/Karma = names only; Command = nothing
- Dry run always required (test discovery, validation)
- Targeted reruns: `--force --mutate src/app.js:5-7`

## Connections
[[Mutation Testing]] [[StrykerJS — Announcing Incremental Mode]]
