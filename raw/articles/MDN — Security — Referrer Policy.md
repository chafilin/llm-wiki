# Referrer Policy Configuration

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Practical_implementation_guides/Referrer_policy

The `Referrer-Policy` header provides fine-grained control over how and when browsers transmit the `Referer` header.

## Problem

When a user navigates to a site via a hyperlink, or when a website loads an external resource, browsers inform the destination site of the origin of the requests via the HTTP `Referer` header. Although this can be useful, it poses a risk to user privacy — it may expose internal URLs or sensitive URL parameters.

## Solution

Use `Referrer-Policy` to limit the information available in the `Referer` header or stop it from being sent altogether.

### Recommended Directives (Strictest to Least Strict)

- **`no-referrer`**: Never send the `Referer` header.
- **`same-origin`**: Send the `Referrer` header only on same-origin requests.
- **`strict-origin`**: Send the `Referrer` header to all origins, but only include the URL without the path (e.g., `https://example.com/`).
- **`strict-origin-when-cross-origin`**: Send the full `Referrer` header on same-origin requests and only the URL without the path on cross-origin requests. **This is the default value.**

## Implementation Methods

### 1. HTTP Header
```http
Referrer-Policy: same-origin
```

### 2. Meta Element (Page-wide)
```html
<meta
  http-equiv="Referrer-Policy"
  content="no-referrer, strict-origin-when-cross-origin" />
```

### 3. HTML Element Attribute
```html
<a href="https://example.org/" referrerpolicy="no-referrer">
  My link
</a>
```

### 4. Fetch API
```javascript
fetch(url, { referrerPolicy: 'no-referrer' })
```

## Examples

**Send referrer only for same-origin requests:**
```http
Referrer-Policy: same-origin
```

**Send shortened referrer on cross-origin, full on same-origin:**
```http
Referrer-Policy: strict-origin-when-cross-origin
```

**Fallback for older browsers:**
```http
Referrer-Policy: no-referrer, strict-origin-when-cross-origin
```
