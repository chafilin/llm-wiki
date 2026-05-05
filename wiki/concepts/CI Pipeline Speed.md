---
title: CI Pipeline Speed
type: concept
updated: 2026-05-04
---

## Definition
The set of practices for reducing CI feedback time — from commit to green/red signal. Not a single technique but a hierarchy of interventions, each with different leverage.

## The Optimization Hierarchy

**1. Skip** — don't run work at all when nothing relevant changed.
Test selection (run only tests touching modified files) and affected commands (build/lint/test only changed projects). Shopify's dynamic analysis achieved 99.94% recall running only 60% of tests. [[Spark Joy by Running Fewer Tests — Shopify]]

**2. Select** — filter which tests run based on change impact.
Nx affected: git diff → project graph → dependency traversal. [[Nx — Run Only Tasks Affected by a PR]] [[Speeding Up CircleCI for Nx Monorepo Using Nx Affected]]

**3. Parallelize** — distribute work across concurrent runners.
Split test files by historical timing: CircleCI `--split-by=timings`, Playwright `--shard`, Knapsack Pro queue mode, GitLab `parallel` keyword, Jest `--shard`. [[CircleCI — Boost Build Time with Test Parallelism]] [[Playwright — Test Sharding]] [[How GitLab Used Parallel CI-CD Jobs to Increase Productivity]]

**4. Cache** — persist artifacts across runs.
Remote caching (Turborepo, Bazel, Nx) shares build outputs across ephemeral CI runners. Vercel: 80% publish time reduction. Mercari: 50% task duration reduction. [[Turborepo Remote Cache — Mercari]] [[How Remote Caching Decreased Publish Times by 80% — Vercel]]

**5. Optimize infrastructure** — reduce startup and execution overhead.
PION: switching from docker+machine (3-min EC2 startup per job) to Kubernetes executor was the source of 70% pipeline duration reduction — not code changes. Infrastructure is often the hidden bottleneck. [[How We Reduced GitLab CI Pipeline Duration by 70% — PION]]

## Measure First

Before optimizing: identify the actual bottleneck. Use CI analytics (GitLab, CircleCI Test Insights) to find frequency × duration hotspots. Shopify's assumption was wrong — the bottleneck was disk I/O, not CPU. [[GitLab — CI-CD Analytics]] [[Keeping Developers Happy with a Fast CI]]

## Test Prioritization

Within a selected test set, running failure-prone tests first reduces median time to first failure. Shopify's failure_rate criterion detected 80% of failures after 60% of tests. [[Test Budget — Time Constrained CI Feedback — Shopify]]

## Build Systems at Scale

Bazel and Turborepo provide reproducible, cacheable, incremental builds across large monorepos. Effective modularization (clear package dependency boundaries) is a prerequisite — the cache hit rate is only as good as the graph structure. [[Lessons Learned Migrating to Bazel — Wix]] [[Bazel — Who's Using Bazel]]

## Open questions
- What's the right threshold for enabling test selection vs. full-suite runs?
- How to handle non-deterministic cache keys (env vars, timestamps)?

## Connections
[[Software Development]] [[Testing Philosophy]] [[Merge Queue]] [[Nx — Run Only Tasks Affected by a PR]] [[Spark Joy by Running Fewer Tests — Shopify]] [[Test Budget — Time Constrained CI Feedback — Shopify]] [[Turborepo Remote Cache — Mercari]] [[How Remote Caching Decreased Publish Times by 80% — Vercel]] [[How We Reduced GitLab CI Pipeline Duration by 70% — PION]] [[CircleCI — Boost Build Time with Test Parallelism]] [[Playwright — Test Sharding]] [[Buildkite Test Engine]] [[Buildkite — Case Studies]]
