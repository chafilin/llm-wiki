# Taming Test Flakiness: How We Built a Scalable Tool to Detect and Manage Flaky Tests

**Source:** https://www.atlassian.com/blog/atlassian-engineering/taming-test-flakiness-how-we-built-a-scalable-tool-to-detect-and-manage-flaky-tests
**Author:** Nitish Malik, Senior Engineering Manager
**Date:** December 8, 2025

## Scale of the Problem

- Flaky tests caused 21% of master build failures in Jira Frontend repository
- ~15% of Jira backend failures
- Wasting over 150,000 developer hours annually
- (Reference: Microsoft Research found 13% of test failures flaky; Google found 16%)

## Flakinator

Atlassian built **Flakinator** — a platformized tool replacing a manual file-based system.

**Capabilities:** detection algorithms + ML, quarantine mechanisms, trend analysis dashboards, root cause analysis, custom team thresholds, Jira/Slack integration, CI/CD integration.

**Scale:** Handles 350M+ test executions daily, 3TB+ storage.

## Detection Algorithms

**RETRY Detection:** Reruns failing tests in same build. If test fails then passes, it's marked flaky. CLI checks whether failing tests are already flagged before retrying. Circuit breaking at first flip signal. Achieves 81% detection rate for certain products.

**Bayesian Inference:** Moving window over test run data. Multiple signal distributions (duration variability, environment consistency, result patterns, retry frequency). Outputs scores 0–1.

## Lifecycle

1. Detect → 2. Find owner via code ownership → 3. Create Jira ticket with deadline → 4. Slack notification → 5. Collect signals from quarantined tests via branch builds + scheduled jobs → 6. Calculate test health → 7. Remove from quarantine when health target reached → 8. Track volumes

## Results

Used by 12+ Atlassian products:
- Recovered 22,000+ builds
- Identified 7,000 unique flaky tests
- Reduced CI resource consumption

## Lessons Learned

1. Data quality matters — inconsistent metadata → inaccurate detection
2. Iterate on algorithms — no single method works universally; combine heuristics, stats, ML
3. Prioritize developer experience — adoption depends on smooth UI and workflow integration
