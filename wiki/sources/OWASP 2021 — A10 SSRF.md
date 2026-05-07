---
title: OWASP 2021 — A10 SSRF
type: source
raw: raw/articles/OWASP 2021 — A10 SSRF.md
date_ingested: 2026-05-07
tags: [owasp, ssrf, server-side-request-forgery, cloud-security, network-security]
---

## Summary
OWASP Top 10 2021, category A10: Server-Side Request Forgery, added based on community survey feedback. SSRF occurs when a web application fetches a remote resource without validating the user-supplied URL, allowing attackers to route requests through the server to bypass firewalls, VPNs, and network controls. Prevalence is growing as cloud infrastructure complexity increases.

## Key takeaways
- SSRF lets attackers use the server as a proxy to reach internal networks, cloud metadata endpoints, local files, or internal services.
- Four primary attack vectors: internal port scanning, local file access (e.g., `file:///etc/passwd`), cloud metadata extraction (e.g., `http://169.254.169.254/`), and internal service compromise enabling RCE or DoS.
- Deny lists and regex patterns are insufficient — attackers have known bypass techniques; use positive allow lists for URL schemas, ports, and destinations.
- Network controls: isolate remote resource access to separate networks; apply deny-by-default firewall rules; log all network flows.
- Application controls: validate all client input, use allow lists, avoid sending raw responses to clients, disable HTTP redirections.
- Watch for DNS rebinding and race condition attacks as SSRF bypass vectors.

## Connections
Links to wiki pages this source touches: [[Web Security]]

## Quotes
> "SSRF flaws occur whenever a web application is fetching a remote resource without validating the user-supplied URL. This vulnerability allows attackers to manipulate applications into sending requests to unintended destinations, bypassing network protections like firewalls and VPNs."
