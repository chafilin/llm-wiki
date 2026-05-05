---
title: Turborepo Remote Cache — Mercari
type: source
raw: raw/articles/Turborepo Remote Cache — Mercari.md
date_ingested: 2026-05-04
tags: [remote-caching, turborepo, ci, monorepo]
---

## Summary
Mercari's self-hosted Turborepo remote cache implementation using custom GitHub Actions (background process or sidecar container), chosen over GKE microservice and Cloud Run alternatives for cost and operational simplicity.

## Key takeaways
- Problem: ephemeral CI runners can't share Turborepo's local cache; Mercari doesn't use Vercel managed cache
- Chosen approach: custom GitHub Action as background Node.js cache server (or sidecar container for Docker builds)
- Results: ~50% reduction in Turbo task duration, ~30% total job duration reduction
- Caveats: depends heavily on how many packages changed; ~10s startup negates benefit for short tasks; minimal impact on monolithic apps without package dependencies
- Key insight: effective modularization is prerequisite — cache works best when packages have clear dependency boundaries

## Connections
[[CI Pipeline Speed]] [[Nx — Run Only Tasks Affected by a PR]]
