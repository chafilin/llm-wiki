# Code-Coverage and Carryforward Flags

**Source:** https://medium.com/compass-true-north/code-coverage-and-carryforward-flags-a6ed006864c1
**Author:** Daniel Straus
**Date:** June 16, 2020
**Publication:** Compass True North

## The Problem

Compass manages multiple large monorepos with 70+ applications and 200+ packages. Traditional codecov.io behavior: each upload overwrites previous coverage data. With partial test suites, this made complete tracking impractical. Generating complete coverage for every commit was too expensive.

## Carryforward Flags Solution

Codecov.io feature allowing selective coverage uploads. "We can now upload coverage for any application/package. It will not overwrite any of the coverage numbers already in codecov.io for any application(s)/package(s) other than the one your PR makes changes to."

Compass automated YAML generation to manage their numerous applications.

## Results

- Faster CI pipeline (partial coverage uploads only)
- GitHub checks blocking PRs when coverage drops below thresholds
- Better developer visibility into coverage progress
- Protection against regression in production deployments

## Key Pattern

Define flags in codecov YAML → upload only the flag for the changed application/package → Codecov carries forward unchanged flags from the last upload. Total coverage picture maintained without full reruns.
