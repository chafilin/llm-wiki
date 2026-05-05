---
title: Codecov — Commit Status Checks
type: source
raw: raw/articles/Codecov — Commit Status Checks.md
date_ingested: 2026-05-04
tags: [test-coverage, codecov, ci, quality-gates]
---

## Summary
Codecov's three status check types (project, patch, changes) for blocking PRs based on coverage thresholds. Provides fine-grained control over what triggers a failure.

## Key takeaways
- **Project status**: overall repo coverage vs. base commit; configurable target, threshold, flags, paths
- **Patch status**: lines modified in the PR — are new lines tested?
- **Changes status**: unexpected coverage fluctuations not in the diff
- `removed_code_behavior`: handles coverage drops from deletions (fully_covered_patch, adjust_base, removals_only)
- `flag_coverage_not_uploaded_behavior`: monorepo handling when specific flags lack uploads
- Path filtering enables component-specific checks

## Connections
[[Test Coverage]] [[Codecov — Why Patch Coverage Matters More]]
