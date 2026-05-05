# Handling Flaky Tests at Scale: Auto Detection & Suppression

**Source:** https://slack.engineering/handling-flaky-tests-at-scale-auto-detection-suppression/
**Author:** Arpita Patel, Staff Software Engineer
**Date:** April 5, 2022

## Overview

Slack's Mobile Developer Experience Team addresses CI stability across 120+ developers, 550+ PRs weekly, 16,000+ Android tests, and 11,000+ iOS tests. Before automation, main branch pass rate was 20%, with 57% of failures from flaky/failing automated tests.

## Two Flaky Test Types

- **Independent flaky tests** — fail regardless of context; easier to debug
- **Systemic flaky tests** — fail only within suites (shared state, CI environment); harder to diagnose

## First Approach: Filtering Results

Calculated flakiness percentages from history; suppressed above threshold. Boosted PR stability 71% → 88% and main branch 61% → 90%.

**Problems:** New tests lacked history (real failures hidden), developers couldn't distinguish fixed from suppressed, single point of failure on backend.

## Second Approach: Suppressing Execution

Three components: detection, suppression, notifications.

**Detection:** Identified failing tests, excluded infra failures/crashes/API issues.

**Suppression automatically:**
- Created Jira tickets assigned to owning teams
- Opened PRs disabling problematic tests (rename on iOS, `@Ignore` on Android with Jira reference)
- Auto-approved and merged those PRs
- Notified teams

## Impact (after ~1 year)

- Main branch stability: 19.82% → 96%
- Test job failures: 56.76% → 3.85%
- ~553 hours of manual triage work saved (28 min per failure previously)
- 74% of developers reported positive impact; 64% fewer PR reruns

## Future Direction

Automatic re-enabling of suppressed tests via quarantine rerunning — tests must pass consistently before restoration.
