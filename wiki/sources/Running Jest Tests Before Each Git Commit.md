---
title: Running Jest Tests Before Each Git Commit
type: source
raw: raw/articles/Running Jest Tests Before Each Git Commit.md
date_ingested: 2026-05-04
tags: [jest, pre-commit, git-hooks, testing-tools]
---

## Summary
Ben McCormick's 2017 guide to running Jest tests on staged files before committing. Key: `--findRelatedTests` flag runs tests related to staged files (unlike `--onlyChanged` which ignores staged files or `--lastCommit` which needs an existing commit).

## Key takeaways
- `--findRelatedTests $STAGED_FILES` is the right flag for pre-commit: tests affected by staged files
- `--bail` stops on first failure (fast feedback)
- `lint-staged` package: declarative config in package.json, runs automatically
- `lint-staged` config: `"*.js": ["eslint --fix", "git add", "jest --bail --findRelatedTests"]`
- Repository-wide consistency without per-user setup

## Connections
[[Testing Philosophy]] [[CI Pipeline Speed]]
