---
title: OWASP 2021 — A08 Software and Data Integrity Failures
type: source
raw: raw/articles/OWASP 2021 — A08 Software and Data Integrity Failures.md
date_ingested: 2026-05-07
tags: [owasp, supply-chain, ci-cd, deserialization, integrity, solarwinds]
---

## Summary
OWASP Top 10 2021, category A08: vulnerabilities from failing to verify integrity of software, updates, and data throughout the development pipeline. Encompasses 10 CWEs with a max incidence rate of 16.67%. Covers three distinct risk areas: untrusted dependencies, insecure CI/CD pipelines, and unsafe auto-update mechanisms, plus insecure deserialization.

## Key takeaways
- Use digital signatures to verify all software and data before trusting it — applies to libraries, updates, and serialized data sent to/from clients.
- Only consume libraries from trusted, verified repositories; use OWASP Dependency Check for supply chain visibility.
- CI/CD pipelines need proper segregation, access controls, and code review before integration — they are high-value attack targets.
- Insecure deserialization of untrusted data can enable remote code execution (Java serialization exploits as a canonical example).
- Real-world examples illustrate scale: SolarWinds distributed malicious updates to 18,000+ organizations; unsigned firmware leaves device fleets permanently vulnerable.

## Connections
Links to wiki pages this source touches: [[Web Security]], [[Software Development]]

## Quotes
> "SolarWinds Attack: Nation-states attacking update mechanisms, distributing malicious updates to over 18,000 organizations."
