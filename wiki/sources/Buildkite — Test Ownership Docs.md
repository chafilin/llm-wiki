---
title: Buildkite — Test Ownership Docs
type: source
raw: raw/articles/Buildkite — Test Ownership Docs.md
date_ingested: 2026-05-04
tags: [test-ownership, buildkite, developer-experience]
---

## Summary
Buildkite's TESTOWNERS file system for assigning teams to test file patterns. Similar syntax to .gitignore/CODEOWNERS but uses Buildkite team slugs.

## Key takeaways
- TESTOWNERS file uses Buildkite team slugs (kebab-case)
- First-listed team = default owner (gets notifications); additional teams = co-owners (no notifications)
- Pattern syntax like `.gitignore`: `*`, `*_spec.rb`, `/spec/packages/`, `**/test-engine`
- Upload via API; one active TESTOWNERS per test suite
- Visible in Test Suite Settings → Test ownership
- Limitation: cannot assign zero teams (unspecified patterns inherit parent ownership)

## Connections
[[Developer Experience]] [[Flaky Tests]]
