# Turbocharging Next.js: How Remote Caching Decreased Publish Times by 80%

**Source:** https://vercel.com/blog/turborepo-remote-cache-nextjs-publish-times-80-percent
**Authors:** JJ Kasper, Anthony Shew
**Published:** December 22, 2022

## Context

Next.js: 4M+ npm downloads in 2022, 2,400+ contributors. Integration of Rust into Next.js core extended CI times — compiling Rust binaries across Windows, Mac, and Linux is resource-intensive.

## Failed Approaches

1. Committed compiled SWC binaries to repo → bloated repository, slow git operations
2. Switched to faster dev builds → unsatisfying
3. Cached dev builds in CI → frequent cache misses (storage restrictions), occasional platform-inconsistency failures

## Turborepo's Three Advantages

**Task Isolation:** Caches tasks using isolated inputs (source code, dependencies, env vars). Platform-specific flags ensure correct cache retrieval during canary publishing.

**Persistent Storage:** Hash-based system maintains caches indefinitely — no purges.

**Proactive Cache Population:** GitHub Action automatically builds SWC binaries when source changes. Non-blocking; catches failures earlier than production publishing would.

## Result

**80% drop in publish times** with Turborepo Remote Cache hit.

Custom scripts handled edge cases: FreeBSD support, version-only change handling.
