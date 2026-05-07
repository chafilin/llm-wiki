---
title: "MDN — Security — Subdomain Takeover"
type: source
raw: raw/articles/MDN — Security — Subdomain Takeover.md
date_ingested: 2026-05-07
tags: [security, subdomain-takeover, dns, infrastructure, web-attacks]
---

## Summary
Subdomain takeover occurs when a DNS CNAME record points to a hosting provider where no virtual host is currently claimed, allowing an attacker to register that virtual host and serve content under the legitimate subdomain. It can happen during provisioning (attacker races to claim the host first) or deprovisioning (DNS record is left dangling after the host is removed). An attacker who controls a subdomain can read cookies, run XSS, or bypass CSP on that subdomain.

## Key takeaways
- The root cause is a CNAME record that points somewhere real without a corresponding claimed virtual host — "dangling DNS."
- During provisioning, create the virtual host before publishing DNS records; during deprovisioning, remove DNS records before taking down the virtual host.
- Maintain an inventory of all subdomains and their hosting providers to catch dangling records as infrastructure changes.
- Hosting providers vary in how they verify virtual-host ownership — pressure vendors to implement domain verification before allowing a host to be claimed.
- Consequences are severe: an attacker subdomain shares the parent domain's cookie scope and can perform XSS or CSP bypasses.

## Connections
[[Web Security]]

## Quotes
> "Start provisioning by claiming the virtual host; create DNS records last. Start deprovisioning by removing DNS records first."
