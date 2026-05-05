# Introducing the Merge Queue

**Source:** https://shopify.engineering/blogs/engineering/introducing-the-merge-queue
**Author:** Darren Worrall
**Published:** June 8, 2018

## Context

Shopify's monolithic Rails app serving 600,000+ merchants. Trunk-based development with frequent master commits. Developers used a Shipit browser extension showing stack conditions (clear, locked, backlogged). As development accelerated, competitive pressure to merge during narrow windows caused frustration.

## The Merge Queue Solution

Automated queue integrated into Shipit:
- Allows developers to enqueue PRs without leaving GitHub
- Automatically merges when master reaches a safe state
- De-emphasizes default merge button (over 90% adoption achieved)
- Enforces configurable branch age and commit divergence thresholds
- Waits for pending CI before merging (doesn't eject)

## Unsafe Commits Management

**Manual marking:** Developers flag commits as unsafe for isolated deployment.

**Automatic revert detection:** Shipit identifies reverted commits and marks them + intermediate commits as unsafe. Prevents manual intervention when rolling back problematic changes.

## Impact

Faster, safer deployments while freeing developers from merge coordination overhead.

## Historical Note

This is the v1 merge queue — predecessor to the more sophisticated predictive branch / Virtual DOM approach described in "Successfully Merging the Work of 1000+ Developers" (2019).
