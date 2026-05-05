# How We Reduced Our GitLab CI Pipeline Duration by 70% at PION

**Source:** https://cpcwood.com/blog/6-how-we-reduced-our-gitlab-ci-pipeline-duration-by-70-at-student-beans
**Author:** Chris Wood
**Date:** October 22, 2022

## Result

70% reduction in average pipeline duration across 90+ pipelines. Saves over 350 hours/month. Teams went from docker+machine (3-min EC2 startup per job) to Kubernetes executor.

## Key Changes

### 1. Kubernetes Executor (from docker+machine)

Original: `docker+machine` → new AWS EC2 instance per job (~3 min startup). Migration to GitLab Runner Kubernetes executor:
- Reduced startup latency
- Better resource optimization via pod-level CPU/memory allocation

### 2. Distributed Caching (AWS S3)

Container jobs lose build dependencies on completion. S3 caching persists dependencies across runs.

### 3. Container Image Layer Caching (Kaniko)

Docker caches image layers locally — lost in ephemeral containers. Kaniko builds images without Docker-in-Docker, supports remote layer caching.

**Dockerfile optimization:** Copy stable files (package.json, Gemfile.lock) before application code — ensures cache hits when only app files change.

### 4. Parallelizing Large Jobs

GitLab `parallel` keyword with Jest's `--shard` option:
```yaml
parallel: 5
script: jest --shard=$CI_NODE_INDEX/$CI_NODE_TOTAL
```

### 5. `needs` Keyword for Fan-Out

Jobs execute immediately upon completing dependencies, bypassing stage boundaries. Independent builds proceed without waiting for all stage jobs.

## Additional Optimizations

**Shared CI Config:** `include` keyword extracts common steps → standardized across 100+ projects with single-point updates.

**Cancel Redundant Pipelines:** `interruptible: true` auto-cancels outdated pipelines during active development.

## Key Insight

Most of the win came from infrastructure (Kubernetes), not code changes. Startup time was the hidden bottleneck — not test speed.
