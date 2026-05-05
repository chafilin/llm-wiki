# Successfully Merging the Work of 1000+ Developers

**Source:** https://shopify.engineering/successfully-merging-work-1000-developers  
**Published:** Nov 14, 2019  
**Author:** Jack Li

## Overview

Shopify manages a monolithic codebase with over 1000 developers, deploying approximately 40 changes daily through around 400 commits to the master branch. The organization implemented a Merge Queue system to maintain three critical deployment safety principles while scaling development operations.

## Three Essential Rules for Safe Deployment

1. **Master must always be green (passing CI)** — enables deployment from master at any time
2. **Master must stay close to production** — reduces risk from excessive version drift
3. **Emergency merges must be fast** — critical for incident response

## Merge Queue v1

Introduced two years prior, the initial merge queue prevented master from drifting too far from production by queuing pull requests instead of merging directly. It controlled batch sizes and prevented merging when too many undeployed pull requests existed on master.

**Key limitations:**
- No CI execution while pull requests waited in queue
- Soft conflicts (failures when merging independent passing changes) weren't caught
- Browser extension requirement created poor user experience and accidental direct merges

## Merge Queue v2

The upgraded system addresses previous shortcomings through several innovations.

### User Experience Improvements

Replaced the browser extension with a comment-based interface inspired by Atlantis. Developers use `/shipit` commands to initiate merges, with `/shipit --emergency` for urgent fixes that bypass queue checks. GitHub branch protection prevents direct master merges, ensuring queue compliance.

### Keeping Master Green

Implemented a "predictive branch" where pull requests merge and CI runs before reaching master. Uses a "Virtual DOM" pattern with reconciliation algorithms to maintain consistency between desired state and GitHub's actual state, managing merge commits through two steps: discarding obsolete commits and creating missing ones.

**Handling flaky tests:** Established failure-tolerance thresholds based on flakiness rates. With a 25% flakiness rate, requiring four successive failures before removal reduces false positives to 0.097%.

### Maximizing Throughput

- **Continuous CI execution** for queued pull requests ensures ready deployments when queue unlocks
- **Batch optimization** with 8 pull requests per deployment balances throughput against risk
- **Limited CI scope** runs only 3 batches worth of pull requests simultaneously, reducing resource costs

## Conclusion

The enhanced merge queue improved user experience, deployment safety, and throughput. The organization anticipates future iterations as scale continues growing.
