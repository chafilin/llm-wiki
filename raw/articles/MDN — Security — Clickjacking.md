# Clickjacking

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/Clickjacking

## Overview

**Clickjacking** is a security attack where an attacker tricks users into interacting with a target website in unintended ways. The attacker creates a decoy site that embeds the target site inside an invisible `<iframe>` element and aligns decoy UI elements to overlap with sensitive buttons or links on the target site. When users click what they think are harmless decoy elements, they're actually clicking on hidden elements from the target site.

## How Clickjacking Works: Example

Suppose a bank's website at `https://my-bank.example.com` has a sensitive "Transfer all my money?" button. An attacker creates a decoy page with:

**HTML (Attacker's Page):**
```html
<button id="fake-button">Click here for a free kitten!</button>
<iframe width="800" height="200" src="https://my-bank.example.com"></iframe>
```

**CSS (Attacker's Styling):**
```css
iframe {
  opacity: 0;  /* Hide the iframe */
}

#fake-button {
  position: absolute;
  top: 185px;
  left: 90px;  /* Position over the bank's button */
}
```

When users click the fake button, they're actually clicking the bank's transfer button. If they're logged in, the request includes their credentials and succeeds.

## Clickjacking Defenses

### 1. Restricting Embedding with frame-ancestors

The primary defense is preventing your site from being embedded in iframes on other domains. Use the `frame-ancestors` CSP directive:

```
Content-Security-Policy: frame-ancestors 'self';
```

This allows embedding only from the same origin.

### 2. X-Frame-Options Header

As a fallback for older browsers, use the `X-Frame-Options` header:

```
X-Frame-Options: DENY
X-Frame-Options: SAMEORIGIN
```

- `DENY`: Prevents embedding entirely
- `SAMEORIGIN`: Allows embedding only from the same origin

### 3. SameSite Cookie Attribute

Set the `SameSite` attribute for session cookies to `Lax` or `Strict`:

```
Set-Cookie: sessionid=abc123; SameSite=Lax
```

This prevents cookies from being sent with cross-site requests from embedded contexts, so requests from iframes won't include authentication credentials.

## Defense Summary Checklist

- ✅ Set the `frame-ancestors` CSP directive to prevent or strictly control iframe embedding
- ✅ Set the `X-Frame-Options` HTTP response header as a fallback
- ✅ Set the `SameSite` cookie attribute to `Lax` or `Strict` for session cookies
