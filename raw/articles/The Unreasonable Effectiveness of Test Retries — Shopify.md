# The Unreasonable Effectiveness of Test Retries: An Android Monorepo Case Study

**Source:** https://shopify.engineering/unreasonable-effectiveness-test-retries-android-monorepo-case-study
**Author:** Alejandro Rodriguez Salamanca
**Published:** January 8, 2019

## The Problem

After migrating Android apps to a monorepo and expanding the team, full test suite pass rate dropped dramatically. With 99.95% individual test reliability across 100-test pipelines and 20 such pipelines, overall pass rate falls to ~35%.

## Strategic Retries

Rather than treating retries as failure, the team embraced them as a reliability tool. One retry: theoretical pass rate improves from 35% → 99.95%.

**Three failure categories:**

- **Retriable Failures:** Environment setup (Docker, dependencies, git) — retried within same job
- **Fatal Failures:** Full environment reload needed — slower but faster than manual retry
- **Test Failures:** Flaky tests retried up to 3 times; screenshot tests identified as particularly unreliable

## Results

- Android pipeline pass rate: 31% → ~90%
- iOS repository: 67% → 97%

## Best Practices Beyond Retries

- Reduce dependence on unreliable components
- Enhance component reliability through investigation and fixes
- Implement caching to minimize external service interactions

**Key principle:** "A slightly slower build is preferable over manual retries" — but notify developers when tests pass only after retries to encourage addressing root causes.
