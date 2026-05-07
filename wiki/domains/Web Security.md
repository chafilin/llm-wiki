---
title: Web Security
type: entity
updated: 2026-05-07
sources: 35
---

## Overview

Web security is the practice of protecting web applications, their users, and underlying infrastructure from attacks. The threat landscape divides cleanly into what attackers do (attacks), what browsers enforce (defenses), how users prove identity (authentication), and what headers developers set (practical hardening). The OWASP Top 10 provides a prioritized risk framework for web apps. Most vulnerabilities come down to trusting user-supplied data without validation and failing to isolate contexts that should stay separate.

## Key claims

- **XSS is the most prevalent attack class**: injecting scripts into pages that execute in victims' browsers. Defense requires output encoding by context, Content Security Policy with nonces/hashes, and Trusted Types for DOM sinks. [[MDN — Security — XSS]]
- **CSRF exploits ambient credentials**: attacker tricks the browser into sending authenticated requests. Defense is CSRF tokens or Fetch Metadata (`Sec-Fetch-*` headers) + SameSite cookies. [[MDN — Security — CSRF]]
- **Clickjacking**: framing a site to capture clicks. Prevented by `Content-Security-Policy: frame-ancestors 'none'` or `X-Frame-Options`. [[MDN — Security — Clickjacking]]
- **IDOR** (Insecure Direct Object References): failing to verify authorization when accessing resources by ID. Use UUIDs over sequential IDs and enforce server-side access checks. [[MDN — Security — IDOR]]
- **Prototype Pollution**: attacker modifies `Object.prototype`, affecting all objects. Defenses: `Object.create(null)`, `Object.freeze(Object.prototype)`, schema validation, `--disable-proto` in Node. [[MDN — Security — Prototype Pollution]]
- **SSRF** lets attackers route server requests to internal services. Defense requires allow-listing outbound destinations, blocking internal IP ranges, disabling redirects. [[MDN — Security — SSRF]] [[OWASP 2021 — A10 SSRF]]
- **Supply chain attacks** compromise dependencies or build pipelines (SolarWinds). Defense: lockfiles, SRI for CDN assets, SBOM (CycloneDX/SPDX), signed packages. [[MDN — Security — Supply Chain Attacks]] [[OWASP 2021 — A08 Software and Data Integrity Failures]]
- **Same-Origin Policy** is the browser's primary isolation mechanism: same scheme + host + port. CORS is the controlled exception. [[MDN — Security — Same-Origin Policy]]
- **TLS** provides confidentiality, integrity, and authentication at the transport layer. HSTS (`max-age`, `includeSubDomains`, `preload`) enforces HTTPS. [[MDN — Security — Transport Layer Security]]
- **Subresource Integrity** blocks CDN-delivered tampered scripts via `integrity="sha384-..."` attribute. [[MDN — Security — Subresource Integrity]]
- **Passkeys (WebAuthn)** are the strongest auth mechanism: public/private key pairs tied to origin, phishing-resistant by design, no shared secret. Superior to passwords + MFA. [[MDN — Security — Passkeys]]
- **Password storage**: Argon2id is the recommended algorithm; bcrypt/scrypt are acceptable. Never encrypt passwords (key theft problem). Always salt; pepper adds a layer. [[MDN — Security — Passwords]]
- **Session management**: HttpOnly + Secure + SameSite cookies for centralized sessions. JWTs shift state to client but require careful signature validation — "none" algorithm attack is real. [[MDN — Security — Session Management]]
- **CSP strict mode**: `strict-dynamic` with nonce/hash eliminates the need for allowlisted domains, which are too easy to bypass. Report-Only mode for iterative rollout. [[MDN — Security — CSP Implementation]]
- **CORS minimum-origins principle**: never use `*` with credentials; only echo back explicitly trusted origins. [[MDN — Security — CORS Configuration]]
- **Cookie prefixes**: `__Host-` is the strongest (no Domain, Path must be `/`, Secure required). `__Secure-` less restrictive but still requires Secure flag. [[MDN — Security — Cookie Configuration]]
- **OWASP A06** (Vulnerable Components): max incidence 27.96%. Patch management process + OWASP Dependency Check + retire.js + CVE/NVD monitoring. [[OWASP 2021 — A06 Vulnerable and Outdated Components]]
- **OWASP A07** (Auth Failures): permit credential stuffing, weak passwords, missing MFA. Follow NIST 800-63b; use identical messaging for all auth outcomes to prevent enumeration. [[OWASP 2021 — A07 Identification and Authentication Failures]]
- **OWASP A09** (Logging Failures): no logging of auth events means breaches go undetected for years (7-year example). Append-only audit trails for high-value transactions. [[OWASP 2021 — A09 Security Logging and Monitoring Failures]]
- **Threat modeling** starts with four questions: What are we building? What can go wrong? What will we do about it? Did we do a good job? ERTA framework: Enumerate assets, Rank threats, mitigate, Assess. [[MDN — Security — Threat Modeling]]
- **Deny lists and regex are insufficient** for SSRF and injection prevention. Attackers have too many bypass techniques. Use allow lists. [[OWASP 2021 — A10 SSRF]]

## Open questions

- What does a practical CSP rollout look like for a React SPA with many third-party scripts?
- How do you audit OWASP A01-A05 (access control, crypto failures, injection, insecure design, security misconfiguration)? Those articles weren't captured.
- When does OWASP 2025 ship and what changes vs 2021?

## Connections

[[Software Development]] [[Core Web Vitals]]
