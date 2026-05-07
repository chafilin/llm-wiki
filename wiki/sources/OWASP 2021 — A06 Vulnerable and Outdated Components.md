---
title: OWASP 2021 — A06 Vulnerable and Outdated Components
type: source
raw: raw/articles/OWASP 2021 — A06 Vulnerable and Outdated Components.md
date_ingested: 2026-05-07
tags: [owasp, dependencies, supply-chain, patch-management, sca]
---

## Summary
OWASP Top 10 2021, category A06: risks from using components with known vulnerabilities or no active maintenance. Ranked #2 in the community survey with an average incidence rate of 8.77% across 30,457 observed instances. The core problem is lack of visibility into the full dependency tree combined with deferred patching.

## Key takeaways
- Organizations are vulnerable when they lack inventory of all components including nested (transitive) dependencies.
- Deploying unsupported or unpatched software across any layer — OS, frameworks, databases, runtimes — creates exposure.
- Prevention requires automated tooling: OWASP Dependency Check and retire.js for continuous inventory and CVE/NVD monitoring.
- Only obtain components from official, verified sources with signature validation.
- Unmaintained libraries need virtual patches or replacement; the goal is ongoing monitoring, not point-in-time audits.
- Real-world example: CVE-2017-5638 (Apache Struts 2 RCE) — one vulnerable component enabled a catastrophic breach because it ran with application-level privileges.

## Connections
Links to wiki pages this source touches: [[Web Security]], [[Software Development]]

## Quotes
> "The CVE-2017-5638 Struts 2 vulnerability enabling remote code execution demonstrates how component flaws can facilitate severe breaches when components operate with application-level privileges."
