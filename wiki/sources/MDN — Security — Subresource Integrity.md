---
title: MDN — Security — Subresource Integrity
type: source
raw: raw/articles/MDN — Security — Subresource Integrity.md
date_ingested: 2026-05-07
tags: []
---

## Summary
Subresource Integrity (SRI) lets browsers verify that CDN-hosted resources haven't been tampered with by checking them against a cryptographic hash embedded in the HTML. It applies to `<script>` and `<link>` elements, supports SHA-256, SHA-384, and SHA-512 hash algorithms, and requires the resource to be served with CORS headers. SRI is a defense against supply chain attacks where an attacker compromises a third-party host.

## Key takeaways
- SRI mitigates supply chain attacks: if a CDN is compromised and serves a modified file, the browser rejects it.
- The `integrity` attribute on `<script>` or `<link>` holds one or more `sha256-`, `sha384-`, or `sha512-` prefixed hashes.
- The browser picks the strongest hash present, computes it against the downloaded resource, and blocks on mismatch.
- Cross-origin resources using SRI must also include `crossorigin="anonymous"` and the server must send `Access-Control-Allow-Origin`.
- Hashes can be generated with `openssl dgst`, `shasum`, or the online tool at srihash.org.

## Connections
Links to wiki pages this source touches: [[Web Security]], [[Software Development]]

## Quotes
> "If an attacker gains control of the third-party host, they can inject malicious content or replace files entirely. This is called a supply chain attack."
