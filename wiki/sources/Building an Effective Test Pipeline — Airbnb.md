---
title: Building an Effective Test Pipeline — Airbnb
type: source
raw: raw/articles/Building an Effective Test Pipeline — Airbnb.md
date_ingested: 2026-05-04
tags: [ci, testing-architecture, soa]
---

## Summary
Airbnb's transition from monolithic deep integration tests to a two-phase CI/CD pipeline after SOA migration. CI handles fast unit + shallow integration tests; CD handles deep integration tests via Spinnaker with Automatic Canary Analysis.

## Key takeaways
- Old approach failed: long runtimes, high flakiness from complex dependencies, violated test pyramid
- New two phases: CI (unit + shallow integration, fast) and CD (deep integration, reduced scope)
- Test pyramid levels: unit (business logic), shallow integration (mocked dependencies via YAML), deep integration (real multi-service)
- "If a higher-level test spots an error and there's no lower-level test failing, you need to write a lower-level test"
- Each service maintains its own pipeline → independent parallel testing

## Connections
[[CI Pipeline Speed]] [[Testing Philosophy]] [[Software Development]]
