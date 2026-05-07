---
title: "MDN — Security — Supply Chain Attacks"
type: source
raw: raw/articles/MDN — Security — Supply Chain Attacks.md
date_ingested: 2026-05-07
tags: [security, supply-chain, dependencies, npm, sbom, sri]
---

## Summary
Supply chain attacks compromise a software product by targeting its dependencies, build tools, CDN-hosted scripts, or development environment rather than the product's own code. Because modern applications depend on hundreds of third-party packages, a single compromised dependency can affect many downstream products. Defenses span dependency management, development environment hardening, and browser-level integrity checks.

## Key takeaways
- Attack surface includes npm packages, code editors/plugins, CI/CD systems, version control, and externally hosted CDN scripts — not just runtime application code.
- Lockfiles (`package-lock.json`) and `npm ci` pin exact dependency versions; without them, `npm install` silently picks up a newly published malicious version within a semver range.
- Subresource Integrity (SRI) hashes on `<script>` and `<link>` tags cause browsers to refuse loading CDN assets if their content has been tampered with.
- A Software Bill of Materials (SBOM) in CycloneDX or SPDX format enables automated vulnerability scanning (e.g., Dependency-Track) and integrity verification across all dependencies.
- Development environment hygiene matters: require MFA, signed commits, code review + CI checks on PRs, and apply least-privilege to all team permissions.
- Before adding a new dependency, evaluate maintenance status, security disclosure process, and whether the feature could reasonably be implemented in-house.

## Connections
[[Web Security]], [[Software Development]]

## Quotes
> "Without a lockfile, npm install automatically fetches the latest version matching a range. If an attacker compromises the package author's account and releases a malicious version, it gets installed automatically."
