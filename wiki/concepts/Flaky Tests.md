---
title: Flaky Tests
type: concept
updated: 2026-05-04
---

## Definition
Tests that produce non-deterministic results — passing and failing on the same code without any changes. The key property: the test, not the code, is the source of the signal noise.

## Why it matters
Flaky tests are a trust problem first, a time problem second. Once developers learn that CI failures might be noise, they start ignoring failures — which means real regressions slip through. The cost compounds: false positives waste debugging time, generate duplicate bug reports, and erode the value of the entire test suite.

At scale: Google data shows **84% of pass-to-fail transitions are caused by flakes** — most flagged failures are false alarms. [[TestDino — Flaky Test Benchmark Report 2026]]

## The spectrum, not binary
The key insight from Meta's approach: flakiness isn't "is/isn't" — it's a rate. A test that fails 0.1% of the time is categorically different from one that fails 25% of the time. Treating both as "flaky" obscures priority. [[Probabilistic Flakiness]] introduces the Probabilistic Flakiness Score (PFS) to make this quantitative.

## The cascade problem
A single-test flaky rate of 0.01% across 4,000 tests = 33% pipeline failure rate. At 0.03%, that's 70%. Even <1% flaky rate per suite × 60 suites = ~55% of PRs see failures (Slack's situation pre-fix). [[TestDino — Flaky Test Benchmark Report 2026]] [[Balancing Safety and Velocity in CI-CD at Slack]]

## Root causes (by frequency)
1. Async wait / missing explicit waits — **45%** (fixed sleeps instead of condition waiting)
2. Concurrency — 20%
3. Test order dependency — 12%
4. Resource leaks — 8%
5. Network dependencies — 5%
6. Time/date assumptions — 4%

Playwright's auto-wait targets root cause #1. RAFTs (Resource-Affected Flaky Tests): 46.5% of Playwright flaky tests fail due to CI infrastructure constraints, not code issues. [[TestDino — Playwright Flaky Tests]]

## Approaches by maturity

**Track and rerun (Google):** Mark known flaky tests; rerun automatically on failure instead of blocking. [[Flaky Tests at Google and How We Mitigate Them]]

**3-phase quarantine (Microsoft):** Detect via retry signals → auto-file bugs with auto-assigned owners → quarantine (suppress failures, keep running). Cultural lever: >10 open flaky bugs blocks your PRs. [[Improving Developer Productivity via Flaky Test Management]]

**Probabilistic scoring (Meta):** Bayesian inference on existing CI data yields a continuous score. Persistently flaky tests lose eligibility for predictive test selection. [[Probabilistic Flakiness]]

**Automated suppression (Slack):** Auto-create Jira + open PR to disable test + auto-merge. Main branch stability: 19.82% → 96%, test failures: 56.76% → 3.85%. [[Handling Flaky Tests at Scale — Slack]]

**Three-tier pipeline (Slack Webapp):** Pre-merge (<1% of E2E), post-merge (<10%), regression (rest, batch). Result: flakiness >90% decrease. [[Balancing Safety and Velocity in CI-CD at Slack]]

**Platformized tool (Atlassian):** Flakinator — 350M+ daily test executions, retry-based detection (81%) + Bayesian inference, auto-assigns owners. Recovered 22,000+ builds. [[Taming Test Flakiness — Atlassian]]

## The retry debate
Retries are not a substitute for fixing root causes, but they're unreasonably effective at improving pipeline reliability. Shopify: Android 31% → 90% pass rate with one retry per test. The math: 0.9995^100 × 20 pipelines = 35% pipeline pass rate; one retry raises it to 99.95%. [[The Unreasonable Effectiveness of Test Retries — Shopify]]

## Tooling landscape

Every major testing platform has flaky test support built in:
- **Cypress**: `detect-flake-and-pass-on-threshold` / `detect-flake-but-always-fail` strategies [[Cypress — Experimental Features]]
- **Playwright**: `--fail-on-flaky-tests` (v1.45+), `retries: N` in config [[TestDino — Playwright Flaky Tests]]
- **Vitest**: `retry: { count, delay, condition }` [[Vitest — Retry Config]]
- **Jest (Wix)**: `jest-retry-all-hooks` for beforeAll/afterAll retry support [[Wix — jest-retry-all-hooks]]
- **CircleCI**: Test Insights (14-day detection window), Chunk (AI-powered auto-fix agent) [[CircleCI — Test Insights]] [[CircleCI — Fix Flaky Tests with Chunk]]
- **Buildkite**: Test Engine — detect, assign ownership, configure per-type responses [[Buildkite Test Engine]]
- **Datadog**: Test Optimization — flaky/new flaky/known flaky tags, per-test metrics [[Datadog — Working with Flaky Tests]]
- **Bitbucket**: built-in score 0–100, auto-quarantine above threshold 80 [[Understand and Manage Flaky Tests in Bitbucket Pipelines]]
- **GitLab**: auto-MR via housekeeper bot when flakiness thresholds exceeded [[Quarantine a Flaky Test — GitLab MR]]

## In merge queues
Flaky tests need special handling at the queue level. Shopify's merge queue uses failure-tolerance thresholds: a test with 25% known flakiness requires 4 consecutive failures before being ejected from the queue, reducing false-positive ejections to 0.097%. [[Successfully Merging the Work of 1000+ Developers]]

## Key principle
Always run quarantined tests — only suppress their failures in the UI. Going blind is worse than noise. [[Improving Developer Productivity via Flaky Test Management]]

## Connections
[[Testing Philosophy]] [[Merge Queue]] [[Software Development]] [[CI Pipeline Speed]] [[Developer Experience]] [[Successfully Merging the Work of 1000+ Developers]] [[Keeping Developers Happy with a Fast CI]] [[Improving Developer Productivity via Flaky Test Management]] [[Probabilistic Flakiness]] [[Flaky Tests at Google and How We Mitigate Them]] [[Handling Flaky Tests at Scale — Slack]] [[Balancing Safety and Velocity in CI-CD at Slack]] [[Taming Test Flakiness — Atlassian]] [[The Unreasonable Effectiveness of Test Retries — Shopify]] [[TestDino — Flaky Test Benchmark Report 2026]] [[TestDino — Playwright Flaky Tests]]
