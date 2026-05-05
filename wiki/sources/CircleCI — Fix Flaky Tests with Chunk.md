---
title: CircleCI — Fix Flaky Tests with Chunk
type: source
raw: raw/articles/CircleCI — Fix Flaky Tests with Chunk.md
date_ingested: 2026-05-04
tags: [flaky-tests, ci, ai, automation]
---

## Summary
Chunk is CircleCI's autonomous AI agent that identifies flaky tests, determines root causes, and opens PRs with verified fixes — replacing "rerun until green" with scheduled background repair.

## Key takeaways
- BYOK model: requires API key from OpenAI or Anthropic
- Scheduled runs: daily (Sun–Thu 22:00 UTC), weekly, or monthly
- Configurable limits: max tests/run, solutions/test, validation runs/test, max concurrent PRs
- Each fix PR contains: issue overview, root cause explanation, code changes, verification results
- Setup: separate `.circleci/cci-agent-setup.yml` for environment (not test execution), optional `claude.md`/`fix-flaky-test.md` guidance files
- GitHub App with admin privileges required

## Connections
[[Flaky Tests]]

## Quotes
> "No more 'rerun until green' or late-night debugging. With Chunk fixing flaky tests in the background, you can start your day with verified PRs waiting for review."
