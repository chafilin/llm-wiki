---
title: GitLab — Unit Test Reports
type: source
raw: raw/articles/GitLab — Unit Test Reports.md
date_ingested: 2026-05-04
tags: [ci, testing, gitlab, reporting]
---

## Summary
GitLab CI documentation for displaying test results in merge requests via JUnit XML. Shows passed/failed counts, newly failing tests, resolved failures — without affecting job exit status.

## Key takeaways
- Requires JUnit XML format; up to 30 MB/file, 100 MB/job
- Add `artifacts:reports:junit: rspec.xml` (use `when: always` to capture failures)
- MR test summary panel: passed/failed overview, "Copy failed tests" button, per-test drill-down
- Four result categories: newly failed, newly encountered errors, existing failures, resolved failures
- Important: reports don't affect job status — still need exit code to fail the job
- Screenshots: `[[ATTACHMENT|/path]]` syntax in `<system-out>` JUnit XML

## Connections
[[CI Pipeline Speed]] [[Developer Experience]]
