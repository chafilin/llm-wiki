---
title: Buildkite — Applying SRE Principles to CI/CD
type: source
raw: raw/articles/Buildkite — Applying SRE Principles to CI-CD.md
date_ingested: 2026-05-04
tags: [ci, sre, reliability, developer-experience]
---

## Summary
Argument for applying SRE's SLOs/SLIs/error budgets to CI/CD systems. Treat build systems as services with defined reliability targets. When error budget depletes, pause feature work and fix reliability.

## Key takeaways
- SLOs: define acceptable reliability (e.g., "builds start within one minute")
- SLIs: measure actual performance against SLOs
- Error budgets: quantify acceptable failures before action required (e.g., "33 failed builds monthly")
- Key metrics: build startup latency, total build completion time, test suite reliability scores, feedback loop speed
- Start with modest SLOs based on current performance; refine over time
- Buildkite users spent **9,413 days** collectively retrying failed steps in a single month

## Connections
[[Developer Experience]] [[CI Pipeline Speed]]

## Quotes
> Buildkite users collectively spent 9,413 days retrying failed steps in a single month.
