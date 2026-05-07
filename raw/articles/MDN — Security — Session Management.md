# Session Management

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Authentication/Session_management

## Overview

HTTP is a stateless protocol that lacks built-in mechanisms to correlate a series of individual HTTP requests. Session management solves this by treating a series of requests from a single client as representing a _session_, associating it with persistent state.

## Two Main Models

### 1. Centralized Session Management (Recommended)

The user's session state is stored on the server:

- Server authenticates user and generates a **session ID**
- Server associates the session ID with stored session state
- Client stores and includes the session ID in requests
- Server uses the session ID to look up user's session state

### 2. Decentralized Session Management (JWT-based)

Session state is maintained as a digitally signed object in the client:

- Server creates and signs a token representing session state
- Client stores the signed token
- Client presents token with requests
- Server verifies signature without needing direct database lookup

Decentralized is popular for distributed applications but more complex and introduces additional vulnerabilities.

## Main Attack Types

### Session Hijacking

An attacker takes over a legitimate user's session by accessing their session ID.

**Interception via MITM Attack**
- Defense: Serve site over TLS

**Predicting the Session ID**
- Defense: Ensure session IDs are sufficiently long and random (≥64 bits entropy)

**Attacking the Client (XSS)**
- If session ID stored in local storage, attacker can steal it
- Defense: Implement XSS protections; use HttpOnly cookies

### Session Fixation

Attacker chooses a session ID and convinces the website to use it for the target user.

**Key Defense**: Server must always generate a new session ID and invalidate any existing value when the user signs in.

## Session ID Best Practices

### Values

- **Entropy**: At least 64 bits of entropy to resist guessing/prediction
- **Meaningless**: Should not contain user information or account details
- **Generation**: Use reputable web frameworks/libraries

### Storage

**Cookies (Recommended)**
- Set `HttpOnly` attribute to prevent JavaScript access
- Protects against XSS-based session hijacking

**Local Storage**
- Less secure; accessible to JavaScript in XSS attacks

### Transmission

**Secure Attribute**
- Prevents transmission over unencrypted connections (MITM protection)

**Domain & Path Attributes**
- Set to most restrictive values possible

**CSRF Protection**
- Set `SameSite` attribute to `Lax` or `Strict`
- Implement CSRF tokens and fetch metadata defenses

## Session Lifetime Management

### Timeouts

1. **Idle Timeout**: Times out after period of inactivity
2. **Absolute Timeout**: Times out after specific period regardless of activity
3. **Renewal Timeout**: Shorter than absolute timeout; server generates new session ID without requiring reauthentication

**Important**: All timeouts must be calculated and enforced on the server.

### Invalidation Events

Invalidate and require reauthentication when:

- User changes credentials or initiates account recovery
- Server suspects session ID theft (e.g., sign-in from new IP/device)

## Decentralized Session Management Considerations

### Token Verification

**Common Vulnerability**: Some JWT libraries have accepted unsigned tokens

```
// Vulnerable pattern - library might accept tokens without signatures
{
  "header": {...},
  "payload": {...},
  "signature": null  // No signature!
}
```

**Defense**: Ensure JWT library always validates token signatures

### Session Invalidation (Token Revocation)

With client-maintained tokens, revocation is difficult. Common solution:

1. **Access Tokens**: Short validity period (minutes/hours)
2. **Refresh Tokens**: Longer lifetime; used to obtain new access tokens
3. **Refresh Endpoint**: Centralized place to enforce session invalidation

When session should be revoked, server refuses to issue new access tokens.

## Session Management Checklist

- ✅ Choose centralized model if architecture allows
- ✅ Store session ID in cookie with `Secure` and `HttpOnly` attributes
- ✅ Implement CSRF defenses (`SameSite`, tokens, fetch metadata)
- ✅ Define session expiry policy (idle, absolute, renewal timeouts)
- ✅ Invalidate sessions on high-risk operations
- ✅ For decentralized tokens: validate signatures, use refresh tokens with short-lived access tokens
- ✅ Use well-regarded framework/library rather than custom implementation
