---
title: Compass — Code Coverage and Carryforward Flags
type: source
raw: raw/articles/Compass — Code Coverage and Carryforward Flags.md
date_ingested: 2026-05-04
tags: [test-coverage, monorepo, ci, codecov]
---

## Summary
Compass's use of Codecov's carryforward flags to maintain accurate overall coverage in a monorepo (70+ apps, 200+ packages) without running full coverage on every commit. Each PR uploads coverage only for its changed application/package; others carry forward from previous uploads.

## Key takeaways
- Problem: traditional coverage upload overwrites all previous data; generating full coverage per commit is too expensive at monorepo scale
- Carryforward flags: upload coverage for one app/package; others persist from previous upload
- Automated YAML generation to manage 200+ application flags
- Result: faster CI, per-component GitHub checks, regression protection

## Connections
[[Test Coverage]] [[Codecov — Commit Status Checks]]
