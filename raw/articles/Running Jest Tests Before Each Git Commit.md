# Running Jest Tests Before Each Git Commit

**Source:** https://benmccormick.org/2017/02/26/running-jest-tests-before-each-git-commit/
**Author:** Ben McCormick
**Date:** February 26, 2017

## Problem

Running a full test suite (10-20 seconds, growing) on every commit adds overhead. Not all changes need full suite runs. Naive pre-commit hooks don't handle "affected tests" — only changed files.

## Key Flag: `--findRelatedTests`

Unlike `--onlyChanged` (ignores staged files) or `--lastCommit` (requires existing commit), `--findRelatedTests` identifies and runs all tests related to staged files.

```bash
jest --bail --findRelatedTests $STAGED_FILES
```

## Recommended: lint-staged

The `lint-staged` npm package streamlines the whole flow via package.json:

```json
"lint-staged": {
  "*.js": [
    "eslint --fix",
    "git add",
    "jest --bail --findRelatedTests"
  ]
}
```

Benefits:
- Runs only on staged files
- Chains linting + testing in one step
- Repository-wide consistency without per-user setup
