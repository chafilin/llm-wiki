# Vitest — Coverage Configuration

**Source:** https://vitest.dev/config/coverage

## Overview

Supports three coverage providers: `v8`, `istanbul`, or custom. Configure via CLI using dot notation (must specify `--coverage.enabled` not just `--coverage`).

## Core Settings

**coverage.provider** — `'v8'` | `'istanbul'` | `'custom'` (default: `'v8'`)

**coverage.enabled** — boolean, default `false`. Activates coverage; override via CLI.

**coverage.include** — glob patterns for files to measure

**coverage.exclude** — glob patterns to remove from analysis

## Reporting and Output

**coverage.reportsDirectory** — output location (default: `'./coverage'`), deleted before tests if `clean` enabled

**coverage.reporter** — default: `['text', 'html', 'clover', 'json']`. Supports custom reporters.

## Thresholds and Quality Gates

**coverage.thresholds** — Positive numbers = minimum % required. Negative numbers = maximum uncovered items allowed (e.g., `-10` = max 10 uncovered lines).

**coverage.thresholds.perFile** — enforce thresholds per file (default: false — applies globally)

**coverage.thresholds.autoUpdate** — auto-updates config when current coverage exceeds thresholds

## Advanced Options

**coverage.clean** (default: `true`) — removes previous coverage before tests

**coverage.skipFull** (default: `false`) — excludes fully-covered files from reports

**coverage.changed** — collect coverage only for files modified since a commit or branch

**coverage.watermarks** — default `[50, 80]` — low/high thresholds for visual reporting

**coverage.processingConcurrency** — default: min(20, available CPUs)
