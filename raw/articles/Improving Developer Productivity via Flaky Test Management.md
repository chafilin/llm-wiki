# Improving Developer Productivity via Flaky Test Management

**Source:** https://devblogs.microsoft.com/engineering-at-microsoft/improving-developer-productivity-via-flaky-test-management/  
**Author:** Microsoft Engineering at Microsoft

## Overview

Microsoft developed a comprehensive flaky test management system to address issues with non-deterministic test failures. The system is integrated into CloudBuild (Microsoft's distributed build service) and CloudTest (their verification service).

## Key Problems Addressed

Flaky tests—those that "pass and fail non-deterministically on the same code in the same environment"—waste developer time by producing misleading signals about code changes. Developers may investigate failures unrelated to their actual modifications.

## System Components

**Three Major Phases:**

### 1. Inference

Identifies flaky tests by monitoring execution telemetry. The default approach uses CloudTest's retry mechanism—when a test fails initially but passes on retry, it's marked as flaky. Teams can implement custom detection logic tailored to their needs.

### 2. Reporting

Files bugs for identified flaky tests and assigns them to owners. When no explicit owner exists, the system identifies the developer who made recent frequent changes to that test. Bug reports include detailed failure information and session data.

### 3. Mitigation

Suppresses failures from quarantined tests and explicitly labels them as flaky in user interfaces. Notably, "we always run all the tests and only suppress the results of the quarantined tests," enabling ongoing monitoring. When bugs are closed, tests automatically exit quarantine.

## Impact

The system is currently deployed across more than 100 Microsoft product teams, having identified approximately 49,000 flaky tests and prevented 160,000 session failures. Microsoft also leverages the system culturally—some teams enforce policies blocking pull requests for developers with more than 10 assigned flaky test bugs.
