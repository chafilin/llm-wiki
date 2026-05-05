# Keeping Developers Happy with a Fast CI

**Source:** https://shopify.engineering/faster-shopify-ci  
**Published:** February 24, 2021  
**Author:** Christian Bruckmayer

## Overview

The Test Infrastructure team at Shopify undertook a project to improve CI speed for their core monolith. Their ambitious goal was to reduce the 95th percentile build time from 45 minutes to under 10 minutes—ultimately achieving 18 minutes.

## Architecture Overview

Shopify's CI runs on Buildkite, which allows them to operate CI servers in their own cloud infrastructure. This provides advantages including aggressive scaling, support for different architectures, and custom instrumentation capabilities.

The system works through pipelines (templates of steps), which create builds when run. Each build's steps become jobs distributed to agents on CI servers. Servers run multiple agents simultaneously and scale based on demand.

## Setting Priorities With Data Driven Development

Rather than making assumptions about bottlenecks, the team invested in comprehensive instrumentation. They created a scatter plot mapping execution time against execution frequency for every command, revealing that "the dots in the top right corner are the commands that take the most time and get executed the most (our top priority)."

Three priority areas emerged: preparing agents, building dependencies, and executing tests.

## Improving Docker Start Time by Reducing I/O Bottlenecks

Docker container startup was taking up to 2 minutes. Initial assumptions about underprovisioned machines proved incorrect. Root cause analysis revealed disk I/O was the actual bottleneck—cached directories exceeding 10GB were creating memory pressure.

Solutions implemented:
- Increased disk size
- Mounted most caches as read-only (allowing sharing between agents)
- Result: p95 container startup improved from 90 to 25 seconds (nearly 4× faster)

## The Fastest Code Is the Code That Doesn't Run

Building dependencies like asset compilation, database migration, and bundle install consumed 37% of CI time. Rather than optimizing these operations, the team implemented smart skipping:

- **Database migrations:** MD5 hash comparison of structure.sql and migration folders prevents unnecessary runs
- **Asset compilation:** Similar hash-based approach
- **Parallelization:** Ran these steps concurrently
- **Result:** Reduced this phase from 5 minutes to approximately 3 minutes

## The 80/20 Rule Applies to Tests Too

Shopify Core contains over 170,000 tests growing 20-30% annually. Rather than optimizing individual tests, the team refined their test selection system to run only tests related to code changes.

Key improvements:
- Extended test mapping to non-Ruby files (JSON, YAML)
- Added ActiveRecord fixture mapping using ActiveSupport notifications to identify which fixtures affect which tests
- Increased percentage of builds avoiding full test runs from 45% to over 60%
- Test stability improved from 88% to 97%

The team also applied the Pareto principle, discovering that a small percentage of slow tests disproportionately affected build times. Fixing or disabling problematic tests (like one that frequently hung) contributed significant gains.

## Results

The Test Infrastructure team successfully reduced the p95 CI time from 45 minutes to 18 minutes through:
- Systematic measurement and instrumentation
- Root cause analysis rather than symptom treatment
- Eliminating unnecessary work
- Focusing on high-impact bottlenecks

The article emphasizes that sustained CI performance requires ongoing investment in monitoring and optimization, not one-time fixes.
