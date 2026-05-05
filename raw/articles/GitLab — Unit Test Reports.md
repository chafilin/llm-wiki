# GitLab — Unit Test Reports

**Source:** https://docs.gitlab.com/ci/testing/unit_test_reports/

## Overview

Displays test results directly in merge requests and pipeline details. Requires JUnit XML format. Available across Free/Premium/Ultimate on GitLab.com.

**Important:** Unit test reports don't affect job status — jobs must exit with non-zero status to fail when tests fail.

## File Format Requirements

- JUnit XML format, `.xml` extension
- Max 30 MB per file, 100 MB total per job
- Duplicate test names: only first is used

## Setup

1. Configure test job to output JUnit XML
2. Add `artifacts:reports:junit` to `.gitlab-ci.yml`
3. Specify file paths

```yaml
ruby:
  stage: test
  script:
    - bundle exec rspec --format RspecJunitFormatter --out rspec.xml
  artifacts:
    when: always
    paths:
      - rspec.xml
    reports:
      junit: rspec.xml
```

## Viewing in Merge Requests

**Test summary panel** shows:
- Overview of passed/failed tests
- Expandable details
- "Copy failed tests" button (space-separated, requires `<file>` attributes)
- "Full report" link to pipeline Tests tab

## Test Result Types

- **Newly failed:** Passed on target, failed on source
- **Newly encountered errors:** Passed on target, had errors on source
- **Existing failures:** Failed on both
- **Resolved failures:** Failed on target, passed on source

## Screenshots

Add attachment tags in JUnit XML:
```xml
<system-out>[[ATTACHMENT|/path/to/screenshot.png]]</system-out>
```

Configure artifacts to include screenshot paths.

## Troubleshooting

**Empty summary panel:** Report artifacts expired or files exceed size limits.
**Missing results:** Duplicate test names in JUnit XML.
**No comparison in MR:** Target branch has no test data — run pipeline on target branch first.
