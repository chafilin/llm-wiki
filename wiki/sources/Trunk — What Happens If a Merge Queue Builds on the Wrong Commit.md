---
title: Trunk — What Happens If a Merge Queue Builds on the Wrong Commit
type: source
raw: raw/articles/Trunk — What Happens If a Merge Queue Builds on the Wrong Commit.md
date_ingested: 2026-05-04
tags: [merge-queue, github, incidents]
---

## Summary
Analysis of a 2026 GitHub merge queue regression where it silently reverted commits from main branches. The bug: temp branches were built from the feature branch's original divergence point rather than the current main tip — silently removing intervening work.

## Key takeaways
- Bug: temp branch started from where feature branch diverged from main (weeks ago), not from current main tip
- Effect: merging silently removed all commits that landed on main in between
- Silent failure: CI passed (temp branch was internally consistent), reviewed diff (+29/-34) bore no relation to actual merge (+245/-1,137)
- No merge conflict, no error, no banner — undetectable until you looked at main
- Trunk's safeguard: temp branches only for CI; actual merge to main is a normal merge identical to manual merging

## Connections
[[Merge Queue]]

## Quotes
> "Silently removed those 50 commits of other people's work as a side effect of landing yours."
