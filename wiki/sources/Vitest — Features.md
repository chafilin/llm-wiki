---
title: Vitest — Features
type: source
raw: raw/articles/Vitest — Features.md
date_ingested: 2026-05-04
tags: [vitest, testing-tools, vite]
---

## Summary
Overview of Vitest's feature set. Vite-native test runner with Jest-compatible API, HMR-like watch mode, built-in coverage (v8/Istanbul), sharding, in-source testing, and browser mode.

## Key takeaways
- Reuses Vite config, transformers, resolvers, plugins — no separate test config
- Watch mode: "smart & instant watch mode, like HMR for tests" — only reruns related tests
- Parallelism: multiple processes by default; `--pool=threads` for worker threads; `.concurrent` annotation
- Jest-compatible: `expect`, `vi` mock object, snapshot API
- Coverage: native v8 and Istanbul via `--coverage` / `--coverage.enabled`
- Sharding: `--shard=x/y` for distributed CI execution
- In-source testing: tests colocated with implementation code
- Browser mode: real browser execution for component tests
- Type testing with `expect-type`; benchmarking via Tinybench

## Connections
[[Testing Philosophy]] [[Test Coverage]] [[CI Pipeline Speed]] [[Vitest — Coverage Config]] [[Vitest — Retry Config]]
