# How We Used Parallel CI/CD Jobs to Increase Our Productivity

**Source:** https://about.gitlab.com/blog/2021/01/20/using-run-parallel-jobs/
**Author:** Miguel Rincon
**Published:** January 20, 2021

## The Challenge

GitLab: 90+ CI jobs, 500 merge request pipelines/day. Successful MR pipelines averaged 53.8 minutes in December 2020.

## Bottleneck: `frontend-fixtures` Job

Generated RSpec mock data files required by frontend tests. Typically 20 minutes — but each fixture could be generated independently.

## Solution: `parallel` Keyword

```yaml
# After
rspec-ee frontend_fixture:
  extends:
    - .frontend-fixtures-base
    - .frontend:rules:default-frontend-jobs
  parallel: 2
```

Two parallel instances running concurrently.

## Results

- Execution time: 20 min → ~17 min for longest-running instance (3 min saved from parallelization)
- Additional 3.5 min saved via Knapsack gem (distributes test files evenly)
- Total: ~6.5 minutes saved per pipeline

## Key Recommendations

1. **Measure first** — identify slow jobs causing delays
2. **Assess independence** — can the job be parallelized or batched? (automated tests typically qualify)
3. **Implement and monitor** — add `parallel` keyword, track improvements across multiple pipeline runs

## Knapsack Gem

Distributes test files evenly across parallel instances based on historical timing data. Prevents load imbalance where one shard takes much longer than others.
