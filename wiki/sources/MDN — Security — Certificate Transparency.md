---
title: MDN — Security — Certificate Transparency
type: source
raw: raw/articles/MDN — Security — Certificate Transparency.md
date_ingested: 2026-05-07
tags: []
---

## Summary
Certificate Transparency (CT) is a public logging framework that requires newly issued TLS certificates to be recorded in append-only, cryptographically verifiable logs built on Merkle trees. When a certificate is logged, the log issues a Signed Certificate Timestamp (SCT) that must be presented to browsers during the TLS handshake. Major browsers now mandate CT compliance, making it possible to detect mis-issued or rogue certificates far more quickly than before.

## Key takeaways
- CT logs are append-only and use Merkle trees, making tampering detectable.
- When a certificate is submitted to a CT log, a Signed Certificate Timestamp (SCT) is returned as proof.
- Servers must deliver SCTs to clients, via a certificate extension, a TLS extension, or OCSP stapling.
- Chrome 107+ and Firefox 135+ require CT compliance for all certificates; non-compliant sites are blocked.
- CT enables rapid detection and revocation of mis-issued certificates, increasing accountability for Certificate Authorities.

## Connections
Links to wiki pages this source touches: [[Web Security]]

## Quotes
> "Certificate Transparency is an open framework designed to protect against and monitor for certificate mis-issuances."
