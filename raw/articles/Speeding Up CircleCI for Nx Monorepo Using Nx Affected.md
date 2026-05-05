# Speeding Up the CircleCI Pipeline for a Nx Monorepo Using Nx Affected

**Source:** https://medium.com/@beccahallam/speeding-up-the-circleci-pipeline-for-nx-monorepo-using-nx-affected-140c7d72e4e6
**Author:** Becca Hallam
**Date:** June 19, 2023

## Problem

Naive CircleCI monorepo setups build and deploy each app sequentially — slow, and failures in one app block others, even when changes only affect one application.

## Nx Affected Solution

"Nx affected looks at files you changed in your PR, determines what exactly you updated, and identifies workspace projects that can be affected by this change."

Modify App 1 → only App 1 rebuilds. Modify Library 1 (shared by App 1 and App 3) → only App 1 and App 3 rebuild.

Local: `nx print-affected --select=projects`

## Setting SHAs

`nrwl/nx-set-shas` GitHub Action sets base/head SHAs. Base = last successfully completed workflow on main. Head = PR branch. Ensures comparisons use production-ready code.

## CircleCI Configuration

**Initial config.yml:**
1. Call `nx/set-shas`
2. Run `nx print-affected --select=projects`
3. Generate booleans for each project
4. Write to `.circleci/continuation-params.json`
5. Call `continuation/continue`

**Continuation.yml:**
Receives boolean parameters. Each workflow has a condition — runs only when its parameter is true. Jobs accept custom parameters passing app names to commands like `nx run app_name`.

## Key Outcome

Only changed projects build, in parallel. Failures in one project don't block unrelated projects. Single failure no longer cascades across the entire repo.
