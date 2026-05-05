---
title: How We Reduced GitLab CI Pipeline Duration by 70% — PION
type: source
raw: raw/articles/How We Reduced GitLab CI Pipeline Duration by 70% — PION.md
date_ingested: 2026-05-04
tags: [ci, kubernetes, gitlab, caching]
---

## Summary
PION (Student Beans) reduced average pipeline duration 70% across 90+ pipelines — saving 350+ hours/month — primarily by switching from docker+machine executor (3-minute EC2 startup per job) to Kubernetes executor.

## Key takeaways
- 70% pipeline duration reduction, 350+ hours/month saved
- **#1 win: Kubernetes executor** (from docker+machine with ~3 min EC2 startup per job) — startup latency was the hidden bottleneck, not test speed
- S3 distributed caching: persists build dependencies across ephemeral container jobs
- Kaniko for container image layer caching (Docker-in-Docker alternative with remote caching)
- Dockerfile optimization: copy stable files (package.json, Gemfile.lock) before app code for cache hits
- GitLab `parallel: 5` + Jest `--shard=$CI_NODE_INDEX/$CI_NODE_TOTAL` for test parallelism
- `needs` keyword: jobs execute immediately after dependencies complete (bypasses stage boundaries)
- `interruptible: true`: auto-cancels outdated pipelines during active development

## Connections
[[CI Pipeline Speed]] [[GitLab — CI-CD Analytics]]

## Quotes
> "Most of the win came from infrastructure (Kubernetes), not code changes."
