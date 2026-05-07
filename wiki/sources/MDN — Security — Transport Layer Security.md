---
title: MDN — Security — Transport Layer Security
type: source
raw: raw/articles/MDN — Security — Transport Layer Security.md
date_ingested: 2026-05-07
tags: []
---

## Summary
TLS secures network connections by providing encryption, integrity, and server authentication, and is the foundation of HTTPS. A TLS handshake negotiates the protocol version, cipher suite, and shared session key before any data is exchanged. Proper deployment requires a valid digital certificate, enforcing HTTPS redirects, and sending HSTS headers to prevent SSL stripping; TLS 1.3 is the current recommended version.

## Key takeaways
- TLS provides three guarantees: encryption (confidentiality), integrity (tamper detection), and authentication (server identity).
- HTTPS is the primary defense against MITM attacks on the web.
- TLS 1.3 is current; TLS 1.2 is still acceptable; TLS 1.1 and 1.0 should not be used.
- Server authentication requires a digital certificate binding the public key to a domain name.
- Let's Encrypt issues free TLS certificates.
- Sites should redirect HTTP to HTTPS with a `301 Moved Permanently` response.
- `Strict-Transport-Security` (HSTS) prevents SSL stripping on subsequent visits; the HSTS preload list covers first visits.
- All subresources (scripts, images, fonts) must also be served over HTTPS.

## Connections
Links to wiki pages this source touches: [[Web Security]]

## Quotes
> "All websites should serve all their pages and subresources over HTTPS, and implement server authentication."
