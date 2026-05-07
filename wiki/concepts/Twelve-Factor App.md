---
title: Twelve-Factor App
type: concept
updated: 2026-05-07
---

## Definition

A methodology by Adam Wiggins (Heroku) for building SaaS applications that are portable, deployable on modern cloud platforms, and horizontally scalable. Twelve principles covering the full app lifecycle. Predates Docker but containers naturally satisfy most of them.

## Why it matters

These principles are the baseline expectation for any cloud-deployed application. Violating them — hardcoded config, stateful processes, dev/prod divergence — creates the exact failure modes that cause production incidents and make deployments unpredictable.

## The twelve factors at a glance

| # | Factor | Core rule |
|---|--------|-----------|
| I | Codebase | One repo, many deploys. Shared code → libraries |
| II | Dependencies | Explicit declaration + isolation. No implicit system packages |
| III | Config | In environment variables, not code or files |
| IV | Backing services | Local DB and cloud DB are interchangeable attached resources |
| V | Build/release/run | Strict separation. Releases are immutable |
| VI | Processes | Stateless, share-nothing. Persistent state → backing service |
| VII | Port binding | App includes its own webserver, binds to a port |
| VIII | Concurrency | Scale out via process model, not threads |
| IX | Disposability | Fast startup, graceful shutdown, crash-only design |
| X | Dev/prod parity | Same services, same people, hours not weeks between deploys |
| XI | Logs | Write to stdout. Never manage logfiles |
| XII | Admin processes | Migrations and scripts run as one-off processes against same release |

## Most practically relevant today

**III — Config in env vars**: the most violated factor. Secrets in source code, `.env` files committed to repos, environment-specific config files checked in. Practical test: could you open-source the repo right now without leaking credentials?

**VI — Stateless processes**: foundation of horizontal scaling and zero-downtime deploys. If your app stores user state in process memory (sessions, caches), you can't add a second instance. Sticky sessions are a code smell. Use Redis or the DB.

**X — Dev/prod parity**: SQLite locally + Postgres in production is the canonical bad example. Type differences, query behavior differences, migration behavior differences — all invisible until production. Use Docker to run the real stack locally.

**XI — Logs as streams**: write to stdout, let the platform collect. This is how containerized apps naturally work. Logfiles in containers are anti-patterns — they don't survive container restarts.

## Disposability detail (IX)

Workers must be reentrant — if killed mid-job, the job must be safe to re-run. Achieve this via:
- Idempotent operations
- Transaction wrapping
- Returning job to queue on SIGTERM (RabbitMQ NACK, Beanstalkd auto-return)

## Admin processes (XII)

Database migrations (`rake db:migrate`, `manage.py migrate`) must run against the same release as the app — same codebase, same config, same dependency isolation. Never run migrations from a different environment or version than the deployed app.

## Examples

- A Rails app that reads `DATABASE_URL` from env → follows III. One that has `config/database.yml` with hardcoded credentials → violates III
- A Node app that stores the current user's cart in process memory → violates VI; fails silently when behind a load balancer
- A team that uses SQLite locally and Postgres in production → violates X; has found out the hard way at least once
- A background worker that logs to a file in `/var/log/app/` → violates XI; logs disappear on container restart

## Connections

[[Software Development]] [[Frontend Architecture]] [[12factor.net — The Twelve-Factor App]]
