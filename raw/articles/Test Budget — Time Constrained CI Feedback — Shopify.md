# Test Budget: Time Constrained CI Feedback

**Source:** https://shopify.engineering/test-budget-time-constrained-ci-feedback
**Author:** Apostolis Stergiou
**Published:** March 7, 2022

## The Challenge

Shopify: 170,000+ tests in core monolith. As team grew, CI feedback times became unpredictable (under 10 minutes to significantly longer), causing frequent developer context switches.

## Two-Part System

1. **Test Selection** — Deterministically identifies tests corresponding to code changes
2. **Test Prioritization** — Reorders tests using historical data to surface failures quickly

**Six prioritization criteria:** failure rate, execution duration, code churn, coverage, complexity, and random baseline.

## Core Findings

**Key result:** "We were able to find failures after we had run only 70% of the test-selection suite."

- Median Time to First Failure (TTFF): under 5 minutes across all criteria
- Best performing criterion: **failure_rate** — detected 80% of failures after running 60% of selected tests
- Average Percentage of Faults Detected (APFD): measures how early failures surface
- Convergence Index: indicates reliability of fault detection within time constraints

## Implication

You don't need to run all tests to get confident feedback. With smart prioritization, most failures surface in the first 60–70% of the queue.
