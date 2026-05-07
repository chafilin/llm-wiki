# The Twelve-Factor App: III. Config

Source: https://12factor.net/config

## Store config in the environment

An application's configuration encompasses everything that differs across deployment environments (staging, production, development, etc.), including:

- Database and backing service connections (Memcached, etc.)
- External service credentials (Amazon S3, Twitter, etc.)
- Per-deployment values like canonical hostnames

## The Problem with Hardcoded Config

The twelve-factor methodology mandates **strict separation between configuration and code**. When applications embed configuration as code constants, this violates the principle because "config varies substantially across deploys, code does not."

A practical test: could the codebase be made publicly available without exposing sensitive credentials?

## What Isn't Config

Internal application structure doesn't count as "config" in this context — elements like Rails routing files or Spring dependency wiring remain in code since they don't vary between deployments.

## Why Not Config Files?

While superior to hardcoded constants, untracked configuration files (like `config/database.yml`) present risks: accidental commits, scattered locations, inconsistent formats, and framework-specific limitations.

## The Solution: Environment Variables

The twelve-factor app stores configuration in environment variables because they:

- Change between deployments without code modifications
- Resist accidental repository commits
- Work across languages and operating systems

## Avoiding Config Grouping Problems

Rather than organizing variables into named environment groups (`development`, `production`, `staging`), treat each variable as independent. This scales cleanly as applications expand without creating combinatorial complexity.
