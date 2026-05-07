---
title: The Twelve-Factor App
type: source
raw: raw/articles/12factor.net — The Twelve-Factor App.md
date_ingested: 2026-05-07
tags: []
---

## Summary

Adam Wiggins' methodology for building SaaS applications that are portable, deployable on modern cloud platforms, and scalable without architectural changes. Twelve principles organized around the full app lifecycle — from codebase through processes to admin tasks. Predates containers but containers embody most of it. The most practically relevant factors today are III (config in env vars), VI (stateless processes), X (dev/prod parity), and XI (logs as streams).

## Key takeaways

- **I Codebase**: one repo, many deploys. Shared code → libraries via dependency management, not shared repos
- **II Dependencies**: explicit declaration + isolation. Never rely on system-wide packages. New dev should be able to run one command and have everything
- **III Config**: store in environment variables, not code or config files. Test: can you open-source the repo without leaking credentials?
- **IV Backing services**: local MySQL and Amazon RDS are interchangeable — both are attached resources accessed via URL in config. No distinction in code
- **V Build/release/run**: strict separation. Releases are immutable and versioned. Can't change code at runtime without a new build
- **VI Processes**: stateless and share-nothing. No sticky sessions, no in-memory state between requests. Persistent state goes to a backing service (Redis, DB)
- **VII Port binding**: apps are self-contained — they include their own webserver and bind to a port. No Apache/Tomcat container required
- **VIII Concurrency**: scale out via process model (web workers, job workers). Rely on external process manager (systemd, Foreman), not daemonization
- **IX Disposability**: fast startup (seconds), graceful SIGTERM shutdown, crash-only design. Workers must return jobs to queue on shutdown. Jobs must be reentrant
- **X Dev/prod parity**: close the time gap (deploy hours not weeks), personnel gap (devs deploy), and tools gap (same backing services locally as in prod — no SQLite local + Postgres prod)
- **XI Logs**: write to stdout, never manage logfiles. Platform captures, routes, and stores. Enables Splunk/ELK/alerting without app changes
- **XII Admin processes**: migrations and one-off scripts run as one-off processes against the same release, same codebase, same config as the app

## Connections

[[Twelve-Factor App]] [[Software Development]] [[Frontend Architecture]]

## Quotes

> "A twelve-factor app never concerns itself with routing or storage of its output stream."

> "The twelve-factor app stores config in environment variables… [they] cannot be accidentally checked into the repo."
