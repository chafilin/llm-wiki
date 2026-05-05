---
title: Vitest — Coverage Config
type: source
raw: raw/articles/Vitest — Coverage Config.md
date_ingested: 2026-05-04
tags: [vitest, test-coverage, ci]
---

## Summary
Vitest coverage configuration reference. Supports v8, Istanbul, and custom providers. Rich threshold system with per-file enforcement and auto-update capability.

## Key takeaways
- Providers: `v8` (default), `istanbul`, `custom`
- `coverage.enabled: false` by default — must set explicitly
- Thresholds: positive numbers = minimum %, negative = maximum uncovered items allowed
- `thresholds.perFile: true` — enforce thresholds on each file individually
- `thresholds.autoUpdate: true` — auto-updates config when current coverage exceeds thresholds
- `coverage.changed` — collect coverage only for files changed since a commit/branch
- `watermarks: [50, 80]` — low/high for visual reporting

## Connections
[[Test Coverage]] [[Vitest — Features]]
