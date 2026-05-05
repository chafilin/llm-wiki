---
title: Nx — Run Only Tasks Affected by a PR
type: source
raw: raw/articles/Nx — Run Only Tasks Affected by a PR.md
date_ingested: 2026-05-04
tags: [ci, nx, monorepo, affected, test-selection]
---

## Summary
Nx's official documentation for the `affected` command. Identifies projects impacted by PR changes via git diff → project graph traversal → dependency expansion, then runs tasks only on those projects.

## Key takeaways
- Three-step process: git identifies modified files → project graph finds containing projects → traversal finds dependents
- Basic: `nx affected -t test` / `nx affected -t build`
- CI: `nx affected -t build --base=origin/main --head=$PR_BRANCH_NAME` or via `NX_BASE`/`NX_HEAD` env vars
- `.nxignore` and `.gitignore` patterns excluded from affected analysis
- `--files` flag for non-git scenarios
- `projectsAffectedByDependencyUpdates: "auto"` in nx.json for package dependency changes

## Connections
[[CI Pipeline Speed]] [[Speeding Up CircleCI for Nx Monorepo Using Nx Affected]]
