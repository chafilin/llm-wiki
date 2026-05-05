---
title: Vitest — Retry Config
type: source
raw: raw/articles/Vitest — Retry Config.md
date_ingested: 2026-05-04
tags: [vitest, flaky-tests, testing-tools]
---

## Summary
Vitest's `retry` configuration option documentation. Supports simple count-based retries and, since v4.1.0, advanced configuration with delay between attempts and conditional retry logic based on error type.

## Key takeaways
- Default: `0` (no retries); CLI: `--retry <times>`
- Advanced (v4.1.0+): `{ count, delay, condition }` — condition can be RegExp (matched against error message) or function
- `delay`: ms between retry attempts (useful for rate-limited APIs or resource recovery)
- Limitation: `condition` as function must be defined in test files, not config files (configs are serialized for worker threads)

## Connections
[[Flaky Tests]] [[Vitest — Features]]
