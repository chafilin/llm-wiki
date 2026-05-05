---
title: StrykerJS — TypeScript Checker
type: source
raw: raw/articles/StrykerJS — TypeScript Checker.md
date_ingested: 2026-05-04
tags: [mutation-testing, strykerjs, typescript]
---

## Summary
Plugin that validates mutants against TypeScript's type system before running tests. Marks TypeScript-invalid mutations as `CompileError` — eliminating wasted test cycles on structurally impossible code.

## Key takeaways
- `"checkers": ["typescript"]` in Stryker config
- `prioritizePerformanceOverAccuracy: true` (default): fastest, occasional false negatives; `false`: complete accuracy, slower
- In-memory type checking — no disk side effects
- Supports project references (`--build` mode)
- Prevents test waste on mutations that TypeScript itself would reject

## Connections
[[Mutation Testing]]
