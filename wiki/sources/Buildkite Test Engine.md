---
title: Buildkite Test Engine
type: source
raw: raw/articles/Buildkite Test Engine.md
date_ingested: 2026-05-04
tags: [flaky-tests, ci, buildkite, tooling, test-splitting]
---

## Summary
Buildkite Test Engine (formerly Test Analytics) combines flaky test detection/quarantine with intelligent test splitting. Works with any CI tool, supports most major test frameworks, and provides deep tracing (SQL queries, HTTP requests).

## Key takeaways
- Flaky tests: detect with multiple heuristics → auto-categorize → assign team ownership → configure per-type responses (webhooks, Slack, Linear)
- Test splitting: uses timing data to split work evenly across parallel jobs; example 10/3/2/1 min → 4/4/4/4 min
- Deep tracing: span timeline visualization, slowest SQL queries and HTTP requests
- Case studies: Intercom 25→3 min (85%), Shopify <5 min builds, Elastic 3hr→55 min (70%)
- Billing: P90 method (discard top 10% of daily usage at month end)
- Test state management (muting): Enterprise only

## Connections
[[Flaky Tests]] [[CI Pipeline Speed]] [[Buildkite — Case Studies]]
