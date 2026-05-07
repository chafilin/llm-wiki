---
title: "MDN — Security — MITM"
type: source
raw: raw/articles/MDN — Security — MITM.md
date_ingested: 2026-05-07
tags: [security, mitm, https, tls, web-attacks]
---

## Summary
A Manipulator in the Middle (MITM) attack inserts an attacker between a user's browser and a server, allowing them to read and modify HTTP traffic. A common vector is a rogue Wi-Fi access point in public spaces. HTTPS (HTTP over TLS) is the definitive defense, as it prevents both eavesdropping and predictable traffic modification.

## Key takeaways
- MITM is most commonly executed via rogue wireless access points; the attacker can read and modify any unencrypted HTTP traffic passing through.
- HTTPS over TLS is the primary and sufficient defense — it encrypts traffic and authenticates the server, preventing both snooping and tampering.
- HTTPS must cover all resources on the page (scripts, stylesheets, images, fonts), not just the HTML document — mixed content creates attack surface.
- HTTP-to-HTTPS redirects should be paired with HTTP Strict Transport Security (HSTS) to prevent attackers from stripping the redirect itself.

## Connections
[[Web Security]]

## Quotes
> "You should serve all pages over HTTPS, not just pages that you consider especially sensitive."
