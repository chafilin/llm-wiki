# Codecov — Commit Status Checks

**Source:** https://docs.codecov.com/v5.0/docs/commit-status

## Overview

Status checks enforce coverage standards by blocking pull requests that don't meet specified thresholds.

## Three Status Types

**Project Status:** Measures overall repository coverage vs. base commit. Config: `target` (minimum ratio), `threshold` (allowable drop), `flags`, `paths`.

**Patch Status:** Evaluates only lines modified in the PR. Shows whether new code is properly tested, independent of overall project coverage.

**Changes Status:** Detects unexpected coverage fluctuations not reflected in the diff — flags potential issues.

## `removed_code_behavior` Option

Handles coverage drops from code deletions:
- `fully_covered_patch` (default): passes if new code is 100% covered
- `adjust_base`: recalculates baseline by removing deleted lines first
- `removals_only`: passes for code-deletion-only commits

## `flag_coverage_not_uploaded_behavior`

For monorepo scenarios — controls what happens when specific flags lack coverage uploads: exclude, include, or auto-pass.

## Customization

- Disable default statuses
- Create component-specific checks using path filtering
- Apply global behaviors via `default_rules` without repeating config
