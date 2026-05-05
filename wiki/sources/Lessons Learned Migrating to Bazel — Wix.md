---
title: Lessons Learned Migrating to Bazel — Wix
type: source
raw: raw/articles/Lessons Learned Migrating to Bazel — Wix.md
date_ingested: 2026-05-04
tags: [bazel, build-systems, ci, monorepo]
---

## Summary
Wix's BazelCon 2019 summary covering migration from Maven/TeamCity to Bazel across ~10 million lines of JVM code. After reducing CI build times to ~7 minutes, artifact publishing at ~10 minutes became the new bottleneck.

## Key takeaways
- Bazel reduced CI build times to ~7 min; then artifact publishing (~10 min) became bottleneck
- Solution: parallel, async artifact publishing (runs concurrently with E2E testing, doesn't block build)
- Zero-downtime migration strategy: gradual cutover from Maven/TeamCity
- Local development tooling requires explicit investment alongside build system
- Modularization is a prerequisite — Bazel works best with clear dependency boundaries

## Connections
[[CI Pipeline Speed]] [[Bazel — Who's Using Bazel]]
