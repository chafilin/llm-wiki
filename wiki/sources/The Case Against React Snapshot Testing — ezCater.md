---
title: The Case Against React Snapshot Testing — ezCater
type: source
raw: raw/articles/The Case Against React Snapshot Testing — ezCater.md
date_ingested: 2026-05-04
tags: [snapshots, testing, react]
---

## Summary
ezCater replaced nearly all snapshot tests with focused unit tests after 6 months. Core finding: snapshot tests obscure what actually failed, and developers learn to approve diffs without reviewing them.

## Key takeaways
- Three problems: unclear assertions (entire component rendered), developer negligence (approve without reviewing), maintenance burden (constant unrelated failures)
- Replacements: "it renders" tests → remove them (linting/build suffices); text assertions → target specific content; conditional markup → assert specific component presence
- "A more focused and explicit unit test is a much better choice"
- Tests should document — failures should guide developers to the problem, not to a wall of diff

## Connections
[[Snapshot Testing]]
