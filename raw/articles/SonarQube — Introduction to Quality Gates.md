# SonarQube Cloud — Introduction to Quality Gates

**Source:** https://docs.sonarsource.com/sonarqube-cloud/standards/managing-quality-gates/introduction-to-quality-gates

## Overview

Quality gates evaluate code during analysis using conditions. Each condition tests a metric against a threshold. Determines whether code passes or fails and whether to proceed with fixes or merges.

## Key Concepts

**Status Display:** Results appear on main branch analyses, other branches, and PR pages — "Passed" or "Failed."

**Default Gates:**
- "Sonar way" — standard default
- "Sonar way for AI Code" — recommended for AI-generated code projects

## Quality Gate Composition

Conditions combine:
- A metric (bugs, vulnerabilities, coverage, complexity, etc.)
- Comparison operator
- Error threshold

Example: "Blocker issues > 0" → fail if any blocker issues exist.

## Recommended "Sonar Way" Gate (6 conditions)

1. No new bugs (Reliability rating A)
2. No new vulnerabilities (Security rating A)
3. Limited technical debt (Maintainability rating A)
4. All new Security Hotspots reviewed
5. ≥80% test coverage on new code
6. ≤3% duplication in new code

## Branch vs. PR Behavior

**Main/Long-lived branches:** Apply both overall code and new code conditions.

**Short-lived branches/PRs:** Only new code conditions apply (new code = changes relative to target branch).

**Fudge Factor:** Coverage and duplication conditions ignored until ≥20 new lines exist — prevents disproportionate impact from minor changes.
