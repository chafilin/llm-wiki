---
title: Mutation Testing Our JavaScript SDKs — Sentry
type: source
raw: raw/articles/Mutation Testing Our JavaScript SDKs — Sentry.md
date_ingested: 2026-05-04
tags: [mutation-testing, strykerjs, testing-quality]
---

## Summary
Sentry's experiment applying StrykerJS mutation testing to their JavaScript SDK monorepo. Achieved a 0.62 mutation score for the core SDK; discovered that the incomplete picture (no Playwright/E2E support) matters as much as the score itself.

## Key takeaways
- Core SDK mutation score: 0.62 — ~50% surviving mutants from untested edge cases, ~50% from uncovered paths
- Higher-level packages scored lower despite more E2E/integration tests — light unit coverage there
- StrykerJS incremental mode: jest→vitest migration reduced core SDK run from 60→25 min
- Weekly scheduled runs (not per-PR) due to 35-45 min runtime; track trends via dashboards
- Critical insight: mutation testing doesn't capture E2E/integration test quality — score understates total protection
- Tool is good at identifying specific gaps, not proving overall quality

## Connections
[[Mutation Testing]] [[Testing Philosophy]]
