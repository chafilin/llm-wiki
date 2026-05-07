---
title: "MDN — Security — SSRF"
type: source
raw: raw/articles/MDN — Security — SSRF.md
date_ingested: 2026-05-07
tags: [security, ssrf, server-side, web-attacks, network]
---

## Summary
Server-Side Request Forgery (SSRF) lets an attacker make a server issue HTTP (or other protocol) requests to arbitrary destinations, including internal networks the attacker cannot reach directly. The canonical example is a URL-fetching endpoint that doesn't validate the supplied URL, allowing access to intranet services or local files via `file://`. Even without response bodies, SSRF enables DoS and timing-based information leakage.

## Key takeaways
- SSRF is dangerous because servers typically have broader network access than external clients — an attacker can pivot into internal infrastructure through a vulnerable server-side fetch.
- The `file://` protocol is an often-overlooked attack vector when URL schemes aren't restricted.
- Attackers use redirect chains to evade naive URL validation; defenses must also validate post-redirect destinations.
- Primary defenses: input validation with an allowlist of permitted domains, and blocking all URL schemes except `https://`.
- Apply least-privilege networking: services that fetch external resources should not have unrestricted access to internal networks.
- Log and monitor outbound requests from services — unusual internal-network traffic is a key indicator of SSRF exploitation.

## Connections
[[Web Security]]

## Quotes
> "Although the client could not access http://localhost:443/ directly, the server can, and the server relays the response to the client."
