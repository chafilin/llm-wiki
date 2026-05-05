# Knapsack Pro — Cypress E2E Test Parallelization

**Source:** https://docs.knapsackpro.com/2018/run-javascript-e2e-tests-faster-with-cypress-on-parallel-ci-nodes
**Author:** Artur Trzop (Founder of Knapsack Pro)
**Date:** November 17, 2018

## Overview

Knapsack Pro orchestrates Cypress test distribution across parallel CI nodes via an API-backed queue system.

## Queue Mode Concept

Pull-based approach: "Your parallel CI nodes connect with the Queue and fetch set of test files to run them on CI node." Tests are dynamically assigned rather than pre-allocated statically.

## Dynamic Test Allocation

The system tracks historical test execution times and rebalances assignments to prevent bottlenecks. Handles CI infrastructure variability (AWS preemptions, boot time differences). If a node dies, only its in-progress tests need retry.

## Setup

Single command executed on all parallel CI nodes:

```bash
npx @knapsack-pro/cypress
```

`@knapsack-pro/cypress` integrates with most CI providers out of the box.

## Key Benefits

- Optimal load distribution based on historical timing data
- Resilient against infrastructure interruptions
- Reduces total build completion time
- Minimizes redundant test reruns
