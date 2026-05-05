# Fix Flaky Tests in Your Sleep with Chunk by CircleCI

**Source:** https://circleci.com/blog/fix-flaky-tests-with-chunk/
**Author:** Sebastian Lerner, Director of Product Management
**Date:** October 23, 2025

## Overview

Chunk is CircleCI's autonomous validation agent that automatically identifies and fixes flaky tests. Instead of "rerun until green," Chunk analyzes test history, determines root causes, and opens PRs with verified solutions.

## Requirements

- CircleCI account
- `store_test_results` step configured
- API key from OpenAI or Anthropic (bring-your-own-key model)

## Setup

1. Enable Chunk in CircleCI web app under Chunk Tasks
2. Verify GitHub App installation (admin privileges required)
3. Select AI model provider (Anthropic or OpenAI)
4. Enter API key
5. Creates `circleci-agents` context for secure key storage

## Configuration

**Run Frequency:** Daily (Sun–Thu at 22:00 UTC), Weekly (Sun), or Monthly (1st of month).

**Operational Limits:** Max tests per run, solutions to try per test, validation runs per test, max concurrent open PRs.

**Test Environment:** Create `.circleci/cci-agent-setup.yml` focused on environment prep (install deps, setup DBs, configure services — NOT test execution).

**Optional Guidance Files:** `claude.md`/`agents.md` for general instructions, `.circleci/fix-flaky-test.md` for flaky-test-specific guidance.

## PR Output

Each fix PR contains:
- Run summary with issue overview
- Root cause explanation
- Proposed code changes
- Verification results from test reruns

## Key Takeaway

"No more 'rerun until green' or late-night debugging. With Chunk fixing flaky tests in the background, you can start your day with verified PRs waiting for review."
