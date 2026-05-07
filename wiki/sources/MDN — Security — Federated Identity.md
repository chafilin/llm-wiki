---
title: MDN — Security — Federated Identity
type: source
raw: raw/articles/MDN — Security — Federated Identity.md
date_ingested: 2026-05-07
tags: []
---

## Summary
Federated identity lets a website (Relying Party) delegate authentication to a trusted third-party Identity Provider (IdP), typically via OpenID Connect built on OAuth 2.0. The recommended flow is the authorization code flow with PKCE, which keeps tokens off the front-end and defends against CSRF and code injection. Browser-native FedCM API is the emerging alternative that avoids dependence on third-party cookies, which browsers are phasing out.

## Key takeaways
- The two roles are Identity Provider (IdP, holds credentials) and Relying Party (RP, trusts the IdP's assertions).
- OIDC authorization code flow is two-step: get an authorization code, then exchange it for tokens at a back-end endpoint.
- PKCE (Proof Key for Code Exchange) ties the code exchange to the original request, blocking CSRF and authorization code injection.
- The ID token is a signed JWT identifying the user; the access token grants resource access.
- Third-party cookie deprecation breaks many existing federated identity implementations — avoid building new ones on that dependency.
- FedCM (`navigator.credentials.get({ identity: ... })`) is the browser-native replacement that works without third-party cookies.
- Weaknesses: dominated by a few large IdPs, still vulnerable to phishing, requires a fallback auth method, and users must trust the IdP.

## Connections
Links to wiki pages this source touches: [[Web Security]]

## Quotes
> "Federated identity is an architecture where a website delegates authentication to a third party rather than managing credentials directly."
