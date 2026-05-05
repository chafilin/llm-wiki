---
title: Flaky Tests at Google and How We Mitigate Them
type: source
raw: raw/articles/Flaky Tests at Google and How We Mitigate Them.md
date_ingested: 2026-05-04
tags: [flaky-tests, google, ci, mitigation]
---

## Summary
Google's 2016 overview of how they approach flaky tests at scale. The core stance: don't block on flaky tests, but don't dismiss them either — track them, mark them, rerun them automatically, and work on root causes. The earliest of the three industry flaky-test articles; the Microsoft and Meta approaches are more sophisticated evolutions of these ideas.

## Key takeaways
- Systematic identification and tracking is the prerequisite — you can't fix what you don't measure.
- Once marked flaky, tests are rerun automatically rather than blocking commits. Preserves signal without blocking developers.
- Root cause analysis matters: flakiness is often a symptom of test design problems (too much shared state, timing dependencies, UI test brittleness).
- Google acknowledged at time of writing they didn't have precise cost metrics — the problem was real but unquantified.
- Community patterns: "Reservoir" systems to validate tests before CI integration; test pyramid principles to reduce UI flakiness.

## Connections
[[Flaky Tests]] [[Testing Philosophy]] [[Software Development]]
