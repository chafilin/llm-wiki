---
title: Software Development
type: entity
updated: 2026-05-07
sources: 31
---

## Overview
A collection of principles and hard-won instincts about how to build software that stays maintainable. The through-line: most problems come from complexity, and most good decisions are complexity-reduction decisions.

## Key claims
- [[Complexity]] is the apex predator. Everything else is downstream of controlling it. [[The Grug Brained Developer]]
- Say "no" to features and abstractions early — it's harder than it sounds because "yes" is the career-rewarding word. [[The Grug Brained Developer]]
- Don't factor code too early. Let the system's shape reveal the right cut points. Premature abstraction is worse than duplication. [[The Grug Brained Developer]]
- [[Locality of Behavior]] over Separation of Concerns for most product code. [[The Grug Brained Developer]]
- Integration tests are the testing sweet spot. See [[Testing Philosophy]]. [[The Grug Brained Developer]]
- [[Chesterton's Fence]]: understand before you delete. [[The Grug Brained Developer]]
- [[FOLD]] is a system problem, not a personal one. Senior devs naming complexity gives everyone else permission. [[The Grug Brained Developer]]
- Refactors should stay close to shore — system working throughout, steps small, end-to-end tests as safety net.
- Logging is underrated. Log all major branches. In distributed systems, use request IDs.
- Microservices: only make sense when the factoring problem is already solved.

## CI and merge discipline
- Measure CI bottlenecks before optimizing. Scatter plot: frequency × duration. Assumptions are usually wrong (Shopify's was disk I/O, not CPU). [[Keeping Developers Happy with a Fast CI]]
- The optimization hierarchy for CI speed: **skip > select > parallelize > cache > optimize infrastructure**. See [[CI Pipeline Speed]].
- Infrastructure is often the hidden bottleneck — PION achieved 70% pipeline reduction by switching executors, not changing test code. [[How We Reduced GitLab CI Pipeline Duration by 70% — PION]]
- Remote caching (Turborepo, Bazel) shares build outputs across ephemeral CI runners; modularization is a prerequisite. [[Turborepo Remote Cache — Mercari]]
- Test selection — running only tests mapped to changed files — is higher leverage than speeding up individual tests.
- At scale, "green on my branch" isn't enough. Use a [[Merge Queue]] to catch soft conflicts before they land on master.
- [[Flaky Tests]] need systematic treatment: mark, quarantine, score. Ignoring them destroys CI signal; deleting them loses coverage.

## Test quality
- [[Test Coverage]]: enforce patch coverage (new lines in a PR), not arbitrary project-wide thresholds. Direction matters more than position — celebrate teams improving, not just those high. [[Beyond Numbers — Test Coverage Culture at Apollo]]
- [[Mutation Testing]]: tests the tests. Use StrykerJS incrementally; run weekly, not per-PR. Mutation score diagnoses gaps but doesn't capture E2E/integration test quality. [[Mutation Testing Our JavaScript SDKs — Sentry]]
- [[Snapshot Testing]]: valid for error messages, AST, CSS-in-JS. Never for full component trees. Keep small and deterministic. [[The Case Against React Snapshot Testing — ezCater]]
- [[Test Linting]]: ESLint rules for structural test bugs (empty tests, conditional assertions, wrong query types). Tests can silently pass while asserting nothing.

## Test ownership and developer experience
- Each test suite should have a clear owning team. Test ownership drives accountability for reliability. [[Buildkite — Test Ownership Docs]] [[Pre-Submit UI Tests at Pinterest]]
- Apply SRE principles to CI: SLOs, SLIs, error budgets. Treat build systems as services. [[Buildkite — Applying SRE Principles to CI-CD]]
- Developer portals (Backstage, Compass) provide service catalogs and tech health visibility at org scale. [[Spotify Backstage — Software Catalog]]

## Frontend specifically
- SPA frameworks (React) add a second complexity demon on top of the backend. The tradeoff is real and often not made consciously.
- The alternative — htmx-style locality — keeps HTML as the source of truth and behavior attached to the element.
- Frontend is more fad-prone than backend. Most "revolutionary" ideas have been tried before.
- **SPA threshold** (Russell): build a SPA only if sessions average >10 min AND >10 updates to same data per session. Most sites fail both. [[Frontend Architecture]] [[Infrequently Noted — If Not React Then What]]
- **Rule of Least Client-Side Complexity**: server code runs in controlled conditions; client code runs on unknown hardware. Ship less JS. HTML and CSS degrade gracefully and compress better.
- "React is the industry standard" is a myth — no two React setups are identical. The claim conflates familiarity with necessity. [[Frontend Architecture]]

## Application architecture and deployment

- **Config in env vars** (Twelve-Factor III): never in code or config files. Test: can you open-source the repo without leaking secrets? [[Twelve-Factor App]]
- **Stateless processes** (VI): no in-memory state between requests, no sticky sessions. Persistent state → Redis or DB. This is the prerequisite for horizontal scaling. [[Twelve-Factor App]]
- **Dev/prod parity** (X): same backing services locally as in production. SQLite local + Postgres prod is the canonical violation — breaks in subtle ways. [[Twelve-Factor App]]
- **Logs as streams** (XI): write to stdout, let the platform route and store. Logfiles in containers are anti-patterns. [[Twelve-Factor App]]
- **Admin processes** (XII): migrations and scripts run as one-off processes against the same release as the running app — same deps, same config. [[Twelve-Factor App]]
- **Disposability** (IX): fast startup, graceful SIGTERM shutdown, jobs must be reentrant. [[Twelve-Factor App]]

## Technical debt

- Use Fowler's quadrant to classify debt: Reckless vs. Prudent × Deliberate vs. Inadvertent. Only Prudent-Deliberate debt is actually strategic. [[Technical Debt]]
- The central question before incurring debt: **will this feature persist?** Mission-critical = invest properly. Disposable = omega mess is fine. [[Typecraft — When Technical Debt is the Right Answer]]
- Three tiers by consequence: The Good (upgradeable shortcuts), The Bad (hidden friction that compounds), The Ugly (entrenching — business logic in wrong places). [[Technical Debt]]
- Document debt with rationale and a scheduled repayment — silent accumulation is what kills teams.

## Open questions
- Where does LoB break down at scale? Design systems, shared logic across many features?
- What's the right testing strategy for a frontend-heavy codebase specifically? (Partially addressed in [[Testing Philosophy]], [[Test Linting]], [[Snapshot Testing]])

## Connections
[[Complexity]] [[Locality of Behavior]] [[Chesterton's Fence]] [[FOLD]] [[Testing Philosophy]] [[Merge Queue]] [[Flaky Tests]] [[CI Pipeline Speed]] [[Test Coverage]] [[Mutation Testing]] [[Snapshot Testing]] [[Test Linting]] [[Developer Experience]] [[The Grug Brained Developer]] [[Successfully Merging the Work of 1000+ Developers]] [[Keeping Developers Happy with a Fast CI]] [[How We Reduced GitLab CI Pipeline Duration by 70% — PION]] [[Turborepo Remote Cache — Mercari]] [[Beyond Numbers — Test Coverage Culture at Apollo]]
