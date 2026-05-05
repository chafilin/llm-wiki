# Lessons-Learned from Migrating Our Build System to Bazel

**Source:** https://medium.com/wix-engineering/lessons-learned-from-migrating-our-build-system-to-bazel-ea656726d6d8
**Author:** Wix Engineering
**Date:** June 23, 2020

## Summary

BazelCon 2019 presentation summary — Wix migrated from Maven/TeamCity to Bazel across ~10 million lines of JVM code.

## Key Topics

### 1. Parallel and Asynchronous Artifact Publishing (Liron Tal)

Migration to Bazel reduced CI build times to ~7 minutes. Artifact publishing became new bottleneck at ~10 minutes. Solution:
- Handles parallel builds on master while maintaining correct publishing order
- History builds run without publishing outputs
- Asynchronous — publishing doesn't block the build
- Publishing runs concurrently with E2E testing

### 2. Local Development Improvements (Ittai Zeidman)

Tools built to enhance local development velocity. Planned open-source contributions. Current development workflows and future initiatives.

### 3. Gradual Migration Without Downtime (Or Shachar)

Transformed backend CI from Maven/TeamCity to Bazel:
- Zero downtime migration
- Significantly faster builds across all codebases
- Internal tools developed (some open-sourced)
- Guiding principles for the transition

## Key Takeaway

Bazel enables fast, reproducible builds at scale — but migration requires handling artifact publishing pipelines separately, and local development tooling needs explicit investment.
