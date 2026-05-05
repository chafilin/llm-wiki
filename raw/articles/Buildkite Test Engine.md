# Buildkite Test Engine

**Source:** https://buildkite.com/platform/test-engine/

## Overview

Buildkite Test Engine accelerates builds using real-time flaky test management and intelligent test splitting. Works with any CI/CD tool: Buildkite Pipelines, GitHub Actions, Jenkins, CircleCI, and more.

## Flaky Tests Management

**Detect with precision:** Multiple detection heuristics identifying intermittent failures and flaky patterns. Automatically categorizes and quarantines problematic tests.

**Assign team ownership:** Maps tests to teams, auto-assigns ownership when problematic tests surface.

**Customize responses:** Configure workflows per test type or team. Granular control — separate monitoring strategies for feature tests, unit tests, specific environments. Custom notifications via webhooks, Slack, or Linear.

**Definition:** "Flaky tests are automated tests that produce inconsistent or unreliable results, despite being run on the same code and environment." Default detection: same test on same commit SHA with different results.

## Test Performance Analysis

**Find slowest tests:** Identify which tests slow builds, ranked by timing data from all runs.

**Use timing data to split work:** Group tests into parallel jobs using timing data. Built-in intelligent sorting or custom distribution rules.

- Before: 10m, 3m, 2m, 1m (bottlenecked on slowest node)
- After: 4m, 4m, 4m, 4m

## Deep Tracing

Automatic tracing for test visibility. View why tests are slow or behaving differently between executions. Span timeline visualization, slowest SQL queries and HTTP requests tracked.

## Supported Test Frameworks

RSpec, Jest, Cypress, pytest, Swift, and others. Also accepts JUnit XML format.

## Billing

P90 method for managed tests — measures managed tests executed at least once daily, discards top 10% at month's end. Free plan available. Pro/Enterprise plans unlock all features.

## Notable Case Studies

- **Intercom:** 25min → 3min (85% reduction), 150 daily deployments
- **Shopify:** 8,000 active pipelines, 300M jobs/year, builds <5 min
- **Elastic:** 3hr → 55min pipeline, cloud spend reduced ~75%
