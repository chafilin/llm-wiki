---
title: Beyond Numbers — Test Coverage Culture at Apollo
type: source
raw: raw/articles/Beyond Numbers — Test Coverage Culture at Apollo.md
date_ingested: 2026-05-04
tags: [test-coverage, culture, ci, vitest, playwright]
---

## Summary
Apollo's account of growing frontend unit test coverage from 24% to ~50% across 30+ squads over 6 months, with a 35% reduction in high-severity incidents. Key approach: visibility over mandates, direction (delta) over position (absolute number).

## Key takeaways
- Started at 24% declining; problem: coverage as lagging indicator, no team-level visibility
- Track coverage **delta** (weekly/monthly changes), not absolute — a team at 35% trending up outperforms one at 55% declining
- Grafana dashboard: nightly CI → every team's frontend unit, E2E, backend coverage, green/red by week
- Missing coverage report: zero-coverage files grouped by team and directory
- PR enforcement: any coverage >0% passes (not 80%); escape hatches: `code-coverage-ignore` comment, PR label
- Progressive rollout: informational → opt-in → company-wide
- Dead code removal (Knip): single cleanup → 4,000+ lines removed → ~5% coverage increase
- Results: 24% → 50%; 60% of teams declining → 8%; 35% fewer high-severity incidents

## Connections
[[Test Coverage]] [[Testing Philosophy]] [[Software Development]]

## Quotes
> "A team at 35% trending upward outperforms one at 55% declining by 4 points."
