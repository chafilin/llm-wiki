---
title: Handling Flaky Tests at Scale — Slack
type: source
raw: raw/articles/Handling Flaky Tests at Scale — Slack.md
date_ingested: 2026-05-04
tags: [flaky-tests, ci, mobile, automation]
---

## Summary
Slack's Mobile Developer Experience team describes two generations of flaky test automation across 120+ developers, 550+ PRs/week, and ~27,000 Android/iOS tests. The first approach filtered results; the second suppressed execution entirely — auto-creating Jira tickets, opening PRs to disable tests, and auto-merging them.

## Key takeaways
- Before automation: main branch stability was 19.82%, test job failures at 56.76%
- Two flaky test types: independent (fail anywhere) vs. systemic (fail only in suites from shared state)
- First approach: suppress flaky results above threshold → 71% → 88% PR stability, but new tests had no history and real failures could be hidden
- Second approach: auto-create Jira, open PR to disable test (rename or `@Ignore`), auto-merge it, notify team
- After ~1 year: main branch stability 19.82% → **96%**, test job failures 56.76% → **3.85%**
- Saved ~553 hours of manual triage; 64% fewer PR reruns
- Future direction: auto-re-enable tests once they pass consistently in quarantine

## Connections
[[Flaky Tests]] [[Testing Philosophy]] [[Software Development]]

## Quotes
> "A slightly slower build is preferable over manual retries" — but notify developers when tests pass only after retries
