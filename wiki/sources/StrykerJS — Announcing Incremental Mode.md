---
title: StrykerJS — Announcing Incremental Mode
type: source
raw: raw/articles/StrykerJS — Announcing Incremental Mode.md
date_ingested: 2026-05-04
tags: [mutation-testing, strykerjs, performance]
---

## Summary
StrykerJS blog post announcing incremental mutation testing (v6.2). Only runs mutations on changed code; reuses prior results for unchanged code. In the example: 3,731 of 3,965 results reused — only 234 new runs needed.

## Key takeaways
- `--incremental` flag or `"incremental": true` in config
- Reuse conditions: killed mutant + culprit test unchanged; unkilled mutant + no new test coverage + no test changes
- Uses Google diff-match-patch library for file diffing
- First run generates baseline JSON; subsequent runs reference it
- `--force` to override incremental and rerun all in scope; combine with `--mutate` to target specific files/lines

## Connections
[[Mutation Testing]] [[StrykerJS — Incremental Mode Docs]] [[StrykerJS — Incremental Mode (GitHub)]]
