---
title: Buildkite — Speed Up Builds with bktec
type: source
raw: raw/articles/Buildkite — Speed Up Builds with bktec.md
date_ingested: 2026-05-04
tags: [ci, buildkite, test-splitting, test-state]
---

## Summary
Buildkite Test Engine Client (bktec) documentation. CLI tool that uses Test Engine historical data to split tests across parallel jobs and optionally mute/skip flaky tests.

## Key takeaways
- Test splitting: distributes tests by historical timing, auto-rebalances; example 10 min → ~4 min
- Test state management: mute (execute but ignore result) or skip (don't execute) — Enterprise only
- Pro and above: test splitting; Enterprise only: test state management
- Example: job duration 10/3/2/1 min (bottlenecked) → 4/4/4/4 min (balanced)

## Connections
[[CI Pipeline Speed]] [[Buildkite Test Engine]]
