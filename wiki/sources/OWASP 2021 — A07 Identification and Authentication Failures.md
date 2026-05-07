---
title: OWASP 2021 — A07 Identification and Authentication Failures
type: source
raw: raw/articles/OWASP 2021 — A07 Identification and Authentication Failures.md
date_ingested: 2026-05-07
tags: [owasp, authentication, session-management, mfa, credential-stuffing]
---

## Summary
OWASP Top 10 2021, category A07 (formerly "Broken Authentication"): weaknesses in user identity verification and session handling, affecting ~2.55% of applications on average across 22 mapped CWEs. The category covers credential attacks, weak password policies, inadequate MFA, and session mismanagement.

## Key takeaways
- MFA is the single most effective control — it defeats credential stuffing and brute force even when passwords are compromised.
- Weak password policies (default credentials, no strength requirements) remain widespread; test new passwords against known-bad lists and follow NIST 800-63b.
- Use identical error messages for all authentication outcomes to prevent account enumeration.
- Rate-limit failed login attempts to slow brute force attacks.
- Session IDs must be high-entropy, server-side managed, and invalidated on logout and timeout.
- Three primary attack patterns: credential stuffing, password-only authentication, and browser session timeout exploitation.

## Connections
Links to wiki pages this source touches: [[Web Security]]

## Quotes
> "Implement multi-factor authentication to prevent stuffing and brute force attacks."
