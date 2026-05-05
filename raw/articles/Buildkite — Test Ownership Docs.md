# Buildkite — Test Ownership

**Source:** https://buildkite.com/docs/test-engine/test-ownership

## Overview

Assigns accountability for test suites to specific teams. Teams can be responsible for keeping tests fast, reliable, and trustworthy.

## Configuration: TESTOWNERS File

Uses Buildkite team slugs in kebab-case format. Syntax similar to `.gitignore`.

```
# All tests default owner
*                          my-team

# Specific file patterns
*_spec.rb                  backend-team
/spec/packages/            platform-team
**/test-engine             infra-team
```

**Key rule:** First-listed team is the default owner (receives notifications). Additional teams are co-owners without notification privileges.

## Setup

Teams must have explicit access to the test suite before ownership records are created. Upload via API with authentication.

One active TESTOWNERS file per test suite; same file can apply to multiple suites.

## Visibility

Ownership data surfaced in **Test Suite Settings → Test ownership** page.

## Important Limitation

Unlike `.gitignore`/`CODEOWNERS`, Buildkite TESTOWNERS does not support assigning zero teams to patterns — unspecified patterns inherit parent directory ownership.
