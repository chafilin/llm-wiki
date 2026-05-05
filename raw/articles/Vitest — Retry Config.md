# Vitest — Retry Configuration

**Source:** https://vitest.dev/config/retry

## Overview

The `retry` option allows tests to be automatically re-executed when they fail. Useful for flaky tests caused by temporary issues like network timeouts or resource unavailability.

## Configuration

**Type:** `number | { count?: number, delay?: number, condition?: RegExp }`
**Default:** `0`
**CLI:** `--retry <times>`, `--retry.count <times>`, `--retry.delay <ms>`, `--retry.condition <pattern>`

## Simple Setup

Specify retry count as a number to re-run failed tests up to that many times.

## Advanced Configuration (v4.1.0+)

**count** — How many times to retry (default: 0)

**delay** — Milliseconds to wait between retry attempts (useful for rate-limited APIs or resource recovery)

**condition** — RegExp or function determining whether an error should trigger retry. RegExp patterns tested against error messages; functions receive the error object and return boolean.

## Key Limitation

"When defining `condition` as a function, it must be done in a test file directly, not in a configuration file (configurations are serialized for worker threads)."
