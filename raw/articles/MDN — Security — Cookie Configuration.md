# Secure Cookie Configuration

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Practical_implementation_guides/Cookies

## Problem

Cookies often contain session identifiers or other sensitive information. Unauthorized access to cookies can cause privacy issues, clickjacking attacks, cross-site request forgery (CSRF) attacks, and more.

## Solution

To minimize cookie vulnerabilities, limit access to cookies by including the following attributes in the `Set-Cookie` response header:

### Name
Prepend cookie names with either `__Secure-` or `__Host-` to prevent cookies from being overwritten by insecure sources.

- Use `__Host-` for cookies needed only on a specific domain (no subdomains) where `Path` is set to `/`
- Use `__Secure-` for all other cookies

### Secure
Always set the `Secure` attribute, indicating that the cookie should only be sent over HTTPS.

### HttpOnly
Set the `HttpOnly` attribute on all cookies that don't require access from JavaScript (via `Document.cookie`). This is especially important for session identifier cookies to help prevent XSS attacks from stealing session identifiers.

### Expires and Max-Age
Cookies should expire as soon as they are no longer needed. Session identifiers in particular should expire quickly.

- **Expires**: Sets an absolute expiration date
- **Max-Age**: Sets a relative expiration date (preferred over Expires as it's less error-prone)

If neither is set, the cookie is kept until the user closes their browser.

### Domain
Set the `Domain` attribute only if the cookie needs to be accessible on other domains, using the most restrictive domain possible.

### Path
Set the most restrictive `Path` possible.

### SameSite
Set the `SameSite` attribute to `Strict` or `Lax` to restrict cookie transmission in requests from different sites. This provides partial defense against CSRF, clickjacking, and cross-site leak attacks.

## Examples

**Session identifier cookie (current host only, expires on browser close):**
```
Set-Cookie: MOZSESSIONID=980e5da39d4b472b9f504cac9; Path=/; Secure; HttpOnly
```

**Session identifier for all example.org sites (30-day expiration, Lax SameSite):**
```
Set-Cookie: __Secure-MOZSESSIONID=7307d70a86bd4ab5a00499762; Max-Age=2592000; Domain=example.org; Path=/; Secure; HttpOnly; SameSite=Lax
```

**Long-lived cookie for terms of service acceptance:**
```
Set-Cookie: __Host-ACCEPTEDTOS=true; Expires=Fri, 31 Dec 9999 23:59:59 GMT; Path=/; Secure; SameSite=Lax
```

**Session identifier with Strict SameSite (most restrictive):**
```
Set-Cookie: __Host-BMOSESSIONID=YnVnemlsbGE=; Max-Age=2592000; Path=/; Secure; HttpOnly; SameSite=Strict
```
