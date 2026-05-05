# Turborepo Remote Cache: Accelerating CI to "Move Fast"

**Source:** https://engineering.mercari.com/en/blog/entry/20260216-turborepo-remote-cache-accelerating-ci-to-move-fast/
**Author:** Zuma
**Date:** February 17, 2026

## Problem

Slow CI as a bottleneck to rapid iteration. Turborepo's local caches can't be shared across ephemeral CI runners. Mercari doesn't use Vercel's managed Turborepo Remote Cache → needed self-hosted solution.

## Approaches Evaluated

**GKE Microservice:** Rejected — US CI cluster vs. Japan GKE cluster, $0.08/GiB data transfer, cache pollution risk.

**Serverless Cloud Run:** Too expensive per-repo instance, permission management issues.

**Custom GitHub Actions (Selected):** Most cost-efficient. Leverages existing Workload Identity on self-hosted runners.

## Two Implementation Patterns

**Background Process (standard builds):** Custom JavaScript action launches Node.js cache server as background process, auto-configures env vars and Workload Identity. Single workflow step addition.

**Sidecar Container (Docker builds):** Enhanced action launches cache server as sidecar container sharing network namespace — enables Docker builds to access cache.

## Results

On large, well-modularized repository:
- ~50% reduction in Turbo task duration
- ~30% reduction in total job duration

**Caveats:** Results depend heavily on number of changed applications/packages. Cache server startup (~10 seconds) negates benefit for shorter tasks. Minimal impact on large monolithic apps without internal package dependencies (but this motivated further modularization).

## Key Insight

Effective modularization is crucial for speed improvements. The tool works best when packages have clear dependency boundaries — which itself is good architectural practice.
