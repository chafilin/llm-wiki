---
title: SonarQube — Introduction to Quality Gates
type: source
raw: raw/articles/SonarQube — Introduction to Quality Gates.md
date_ingested: 2026-05-04
tags: [test-coverage, quality-gates, ci]
---

## Summary
SonarQube Cloud documentation for quality gates — sets of conditions (metric + operator + threshold) that determine whether code passes analysis. The recommended "Sonar way" gate focuses entirely on new code rather than the overall codebase.

## Key takeaways
- Conditions: metric + comparison + threshold (e.g., "Blocker issues > 0")
- Default "Sonar way" gate (6 conditions): no new bugs, no new vulnerabilities, no new tech debt, all security hotspots reviewed, ≥80% coverage on new code, ≤3% duplication in new code
- PRs and short-lived branches: only new code conditions apply (changes vs. target branch)
- Fudge factor: coverage/duplication ignored until ≥20 new lines (prevents disproportionate impact from tiny changes)
- "Sonar way for AI Code" variant available for AI-generated code

## Connections
[[Test Coverage]]
