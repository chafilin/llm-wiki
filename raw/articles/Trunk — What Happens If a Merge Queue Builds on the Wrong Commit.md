# Trunk — What Happens If a Merge Queue Builds on the Wrong Commit

**Source:** https://trunk.io/blog/what-happens-if-a-merge-queue-builds-on-the-wrong-commit
**Author:** Phil Vendola
**Date:** April 24, 2026

## The Incident

On April 23, 2026, GitHub's merge queue experienced a regression where it "started silently reverting code on customers' main branches." In some cases, thousands of lines of code disappeared without warning or error.

## Technical Root Cause

GitHub's merge queue constructed temporary test branches from the wrong starting point — branching from where the feature branch originally diverged from main, not from the current tip of main. Result: merging silently removed all commits that landed on main between the feature branch's creation and the merge.

"Silently removed those 50 commits of other people's work as a side effect of landing yours."

The process appeared successful because:
- CI passed (temp branch was internally consistent)
- The reviewed diff (+29/-34) didn't match what actually merged (+245/-1,137)
- No merge conflict surfaced, no check failed

## Why It Was Especially Bad

1. **Deceptive UI** — diff shown during review bore no relation to actual merge outcome
2. **Silent failure** — "No merge conflicts surfaced, no check failed, no banner went up"
3. **Scaled damage** — busier repos experienced worse impact

## Trunk's Architectural Safeguard

Temp branches exist only for CI testing. The actual merge to `main` remains a normal merge identical to manual merging. Tools with `main` write access cannot diverge from expected behavior.
