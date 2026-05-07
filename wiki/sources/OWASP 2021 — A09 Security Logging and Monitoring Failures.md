---
title: OWASP 2021 — A09 Security Logging and Monitoring Failures
type: source
raw: raw/articles/OWASP 2021 — A09 Security Logging and Monitoring Failures.md
date_ingested: 2026-05-07
tags: [owasp, logging, monitoring, incident-response, audit-trail]
---

## Summary
OWASP Top 10 2021, category A09: failures in security logging and monitoring that prevent organizations from detecting and responding to active breaches. Moved from #10 in 2017 to this edition based on community survey prominence. Covers 4 CWEs with an average incidence rate of 6.51% across 53,615 observed instances.

## Key takeaways
- Insufficient logging means breaches go undetected for extended periods — one example saw seven years of undetected exposure at a children's health plan.
- Log all authentication events, failed attempts, and high-value transactions with sufficient context to identify suspicious patterns.
- Logs stored only locally are insufficient; centralized log management is required for effective monitoring.
- Logs themselves must be protected: use append-only audit trails for high-value transactions, and encode log data to prevent log injection.
- Establish alert thresholds, escalation procedures, and incident response frameworks (NIST 800-61r2).
- Tooling: ModSecurity Core Rule Set and ELK stack for visibility; generate logs in formats compatible with log management solutions.

## Connections
Links to wiki pages this source touches: [[Web Security]], [[Software Development]]

## Quotes
> "This category helps organizations detect, escalate, and respond to active security breaches through proper logging infrastructure and monitoring practices."
