---
title: MDN — Security — Session Management
type: source
raw: raw/articles/MDN — Security — Session Management.md
date_ingested: 2026-05-07
tags: []
---

## Summary
Session management bridges HTTP's statelessness by associating a series of requests with persistent server-side state via a session ID, or alternatively via signed client-side tokens (JWTs). The article covers the two main models (centralized vs. decentralized), the main attack vectors (session hijacking and session fixation), and the full set of best practices for session ID generation, cookie attributes, lifetime policies, and invalidation triggers.

## Key takeaways
- Centralized (server-stored) sessions are simpler and recommended when architecture allows; JWT-based sessions are popular for distributed systems but introduce additional attack surface.
- Session IDs must have at least 64 bits of entropy and must be regenerated on every login (prevents session fixation).
- Store session ID in a cookie with `HttpOnly` (blocks JS access) and `Secure` (blocks HTTP transmission) attributes.
- Set `SameSite=Lax` or `Strict` to defend against CSRF, supplemented by CSRF tokens and fetch metadata.
- Define idle, absolute, and renewal timeouts server-side; never rely on client-side enforcement.
- For JWTs: always validate signatures (some libraries historically accepted unsigned tokens), use short-lived access tokens with longer-lived refresh tokens for revocation control.

## Connections
Links to wiki pages this source touches: [[Web Security]]

## Quotes
> "The server must always generate a new session ID and invalidate any existing value when the user signs in."
