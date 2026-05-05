# Applying SRE Principles to CI/CD

**Source:** https://buildkite.com/resources/blog/applying-sre-principles-to-cicd/
**Author:** Mel Kaulfuss
**Date:** August 16, 2023

## Main Argument

Import SRE frameworks to CI/CD systems. Rather than pursuing perfect reliability, define acceptable reliability levels and use measurement-based approaches to maintain developer trust.

## Core Concepts Applied

**Service Level Objectives (SLOs)** — Target reliability guarantees. Example: "builds start within one minute."

**Service Level Indicators (SLIs)** — Measured actual performance against targets. Example: build wait times tracked over time.

**Error Budgets** — Acceptable failure tolerance before action is required. Example: "33 failed builds monthly." When depleted, shift focus to reliability work instead of features.

## Key Metrics

- Build startup latency
- Total build completion time
- Test suite reliability scores
- Developer feedback loop speed

## Process

1. Start with modest SLOs based on current performance
2. Establish shared stakeholder expectations
3. Measure continuously via SLIs
4. When error budget depletes: pause feature work, fix reliability

## Scale Reference

Buildkite users collectively spent **9,413 days** retrying failed steps in a single month — mostly due to flaky tests.
