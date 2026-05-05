---
title: Speeding Up CircleCI for Nx Monorepo Using Nx Affected
type: source
raw: raw/articles/Speeding Up CircleCI for Nx Monorepo Using Nx Affected.md
date_ingested: 2026-05-04
tags: [ci, circleci, nx, monorepo, affected]
---

## Summary
How to combine Nx Affected with CircleCI's continuation API to run only the pipelines for applications affected by a PR. Modified apps trigger their own workflows; unrelated apps skip entirely.

## Key takeaways
- `nx print-affected --select=projects` identifies affected projects from SHAs
- Config flow: call nx/set-shas → run nx print-affected → generate booleans per project → write to continuation-params.json → call continuation/continue
- Continuation.yml: each workflow has a condition checking its boolean parameter
- Parallel execution: unrelated project failures don't block each other
- `nrwl/nx-set-shas`: base = last successful workflow on main, head = PR branch

## Connections
[[CI Pipeline Speed]] [[Nx — Run Only Tasks Affected by a PR]]
